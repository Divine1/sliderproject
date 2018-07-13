<template>
  <div id="mainapp">
    <Slider :images="images" :intervalDuration="slideDuration"/>
  </div>
</template>

<script>
import Slider from "./slider/Slider.vue";
export default {
  components :{
    Slider
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
      slideDuration : 4000
    }
  }
}
</script>

<style>
 body{
   margin:0;
 }
</style>
