<template>
  <div id="slider">
    <div title="previous image" class="arrowLeft" @click="arrowLeft()"></div>
    <Slides :image="images[chosenImage]"/>
    <div title="next image" class="arrowRight" @click="arrowRight()"></div>
    <div class="controls">
        <div class="squares">
            <div 
                @click="squares(image.id)" 
                v-for="image in images" 
                :key="image.id" 
                :title="'Goto image '+(image.id+1)"
                :class="{'active' : (image.id == chosenImage) ? true : false}">
                {{image.id+1}}
            </div>
        </div>
        <div class="pauseplay">
            <div title="play" class="play" @click="pauseplay('play')" v-if="pauseplayToggle">&#9658;</div>
            <div title="pause" class="pause" @click="pauseplay('pause')" v-else>&#10074;&#10074;</div>
        </div>
    </div>
    
  </div>
</template>

<script>
import Slides from './Slides.vue';
export default {
    components : {
        Slides
    },
    props:[
        "images","intervalDuration"
    ],
    data(){
        return{
            chosenImage : 0,
            intervalObject : null,
            pauseplayToggle : false //false - play, true - pause
        }
    },
    methods :{
        squares(id){
            this.chosenImage = id;
            clearInterval(this.intervalObject);
            this.setIntervalSlider('right');
            this.pauseplayToggle = false;
        },
        arrowLeft(){
            clearInterval(this.intervalObject);
            this.moveLeft();
            this.setIntervalSlider('left');
        },
        arrowRight(){
            clearInterval(this.intervalObject);
            this.moveRight();
            this.setIntervalSlider('right');
        },
        moveLeft(){
            var flag = this.chosenImage;
            flag--;
            if(flag< 0){
                flag= (this.images.length -1);
            }
            this.chosenImage = flag;
            this.pauseplayToggle = false;
        },
        moveRight(){
            var flag = this.chosenImage;
            flag++;
            if(flag>= this.images.length){
                flag=0;
            }
            this.chosenImage = flag;
            this.pauseplayToggle = false;
        },
        pauseplay(action){
            console.log("in pauseplay method ", action);
            if(action == 'play'){
                this.arrowRight();
                this.pauseplayToggle = false;
            }
            else if(action == 'pause'){
                clearInterval(this.intervalObject);
                this.pauseplayToggle = true;
            }
        },
        setIntervalSlider(direction){
            var self= this;
            this.intervalObject = setInterval(()=>{
                if(direction == "right"){
                    self.moveRight();
                }
                else if(direction == "left"){
                    self.moveLeft();
                }
            },this.intervalDuration);
        }
    },
    created(){
        this.setIntervalSlider('right');
    }
}
</script>

<style lang="scss">

$color-arrow : #f37115;
$color-slideindicator : yellow;
$color-playbutton : brown;
$color-pausebutton : #580843;
$controls-height-width : 20px;
$controls-innerchild-right-margin: 15px;
$controls-pauseplay-topdown-margin: 10px;
$controls-pauseplay-font-size:20px;
$controls-squares-font-size:15px;
$controls-squares-active-backgroundcolor : #58584f;
$controls-squares-active-font-color:white;
#slider {
    position: relative;
    overflow: hidden;
    height: inherit;
    width: inherit;
    .arrowLeft,.arrowRight{
        position: absolute;
        top: 50%;
        transform: translateY(-50%);
        border: 20px solid transparent;
        cursor: pointer;
    }
    .arrowLeft{
        border-right-color: $color-arrow;    
        z-index: 1;
    }
    .arrowRight{
        right:0;
        border-left-color: $color-arrow;
    }
    .controls{
        position: absolute;
        bottom: 0;
        left:50%;
        transform: translateX(-50%);
        font-weight: bold;
        .squares{
            div{
                height:$controls-height-width;
                width:$controls-height-width;
                line-height: $controls-height-width;
                text-align: center;
                margin-right: $controls-innerchild-right-margin;
                display: inline-block;
                background-color: $color-slideindicator;
                border-radius:50%;
                cursor: pointer;
                font-size: $controls-squares-font-size;
            }
            .active{
                background-color:$controls-squares-active-backgroundcolor;
                color:$controls-squares-active-font-color;
            }
        }
        .pauseplay{
            display:flex;
            justify-content: center;
            margin: $controls-pauseplay-topdown-margin 0;
            font-size: $controls-pauseplay-font-size;
            div{
                display: inline-block;
                height: $controls-height-width;
                line-height: $controls-height-width;
                width: $controls-height-width;
                text-align: center;
                border-radius: 50%;
                cursor: pointer;
                margin-right: $controls-innerchild-right-margin;
            }
            .play{
                color: $color-playbutton;
            }
            .pause{
                color: $color-pausebutton;
            }
        }
    }
}
</style>
