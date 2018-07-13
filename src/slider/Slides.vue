<template>
        <transition-group name="fade" mode="out-in" tag="div" id="slides">
            <div class="slideParent" :key="image.id">
                <div class="slideImage" :style="setBackgroundImage">
                    <div class="slideTitle">
                        {{image.title}}
                    </div>
                </div>
            </div>
        </transition-group>
</template>

<script>
export default {
    props: ["image"],
    computed:{
        setBackgroundImage(){
            return {backgroundImage : "url("+this.image.url+")"};
        }
    }
}
</script>

<style lang="scss">
$color-slidetext : Red;
$animation-zoom-duration : 6s;
$fontsize-slidetext : 40px;

#slides{
    .slideParent{
        height:100vh;
        width: 100%;

        .slideImage{
            height:100vh;
            width: 100%;
            background-position:center;
            background-repeat: no-repeat;
            background-size: cover;
            animation-fill-mode: forwards;
            animation-name:zoom;
            animation-duration: $animation-zoom-duration;
            animation-iteration-count: 1; 
            .slideTitle{
                color:$color-slidetext;
                font-weight:bold;
                font-size: $fontsize-slidetext;
                height:100vh;
                display:flex;
                justify-content: center;
                align-items:center;
            }
        }
    }
}
.fade-enter-active{
    animation-name:fadeEnter;
    animation-duration: 1s;
    animation-iteration-count: 1;
}
.fade-move{
    transition: all 1s;
}
.fade-leave-active{
    animation-name:fadeLeave;
    animation-duration: 1s;
    animation-iteration-count: 1;
    position:absolute;
}
@keyframes zoom{
    from{
        transform: scale(1);
    }
    to{
        transform: scale(1.1);
    }
}
@keyframes fadeEnter{
    from{
        opacity:0;
    }
    to{
        opacity:1;
    }
}
@keyframes fadeLeave{
    from{
        opacity:1;
    }
    to{
        opacity:0;
    }
}
</style>