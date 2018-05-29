<template>
  <div id="slider">
    <div class="arrowLeft" @click="arrowLeft()"></div>
    <Slides :image="images[chosenImage]"/>
    <div class="arrowRight" @click="arrowRight()"></div>
    <div class="squares">
        <div @click="squares(image.id)" v-for="image in images" :key="image.id"></div>
    </div>
  </div>
</template>

<script>
import Slides from './Slides.vue';
export default {
    components : {
        Slides
    },
    data(){
        return{
            images : [
                {
                    id: 0,
                    url : "/images/image1.jpg",
                    title: "Lightning"
                },
                 {
                    id: 1,
                    url : "/images/image2.jpg",
                    title: "Batman on the roof"
                },
                {
                    id: 2,
                    url : "/images/image3.jpg",
                    title: "Suicide Squad"
                },
                {
                    id: 3,
                    url : "/images/image4.jpg",
                    title: "Flash & Reverse Flash"
                },
                {
                    id: 4,
                    url : "/images/image5.jpg",
                    title: "Batman Red"
                }
            ],
            chosenImage : 0,
            intervalObject : null
        }
    },
    methods :{
        squares(id){
            this.chosenImage = id;
             clearInterval(this.intervalObject);
            var self= this;
            this.intervalObject = setInterval(()=>{
                self.moveRight();
            },4000);
        },
        arrowLeft(){
            clearInterval(this.intervalObject);
            this.moveLeft();
            var self= this;
            this.intervalObject = setInterval(()=>{
                self.moveLeft();
            },4000);
        },
        arrowRight(){
            clearInterval(this.intervalObject);
            this.moveRight();
            var self= this;
            this.intervalObject = setInterval(()=>{
                self.moveRight();
            },4000);
        },
        moveLeft(){
            var flag = this.chosenImage;
            flag--;
            if(flag< 0){
                flag= (this.images.length -1);
            }
            this.chosenImage = flag;
        },
        moveRight(){
            var flag = this.chosenImage;
            flag++;
            if(flag>= this.images.length){
                flag=0;
            }
            this.chosenImage = flag;
        }
    },
    created(){
        var self= this;
        this.intervalObject = setInterval(()=>{
            self.moveLeft();
        },4000);
    }
}
</script>

<style>
#slider{
    position: relative;
    overflow: hidden;
}

#slider .arrowLeft,#slider .arrowRight{
    position: absolute;
    top: 50%;
    border: 20px solid transparent;
}
#slider .arrowLeft{
    border-right-color: green;    
    z-index: 1;
}
#slider .arrowRight{
    right:0;
    border-left-color: green;
}
#slider .squares{
    position: absolute;
    bottom: 0;
    left: calc( 50% - 75px);
}
#slider .squares div{
    height:20px;
    width:20px;
    margin-right: 10px;
    display: inline-block;
    background-color:yellow;
    border-radius:50%;
}
</style>
