# sliderproject

> A Vue.js project

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build
```

For detailed explanation on how things work, consult the [docs for vue-loader](http://vuejs.github.io/vue-loader).



##Update - 2018-07-13


i have made this project more generic.

###Below are the details of the changes

####Change 1:
You can now integrate this slider component into your project by just copying the slider folder into your project.

You should pass 2 inputs to this slider component
    1. images
        - Array of JSON object
        - You can pass 'n' number of objects to this.
        - Please note that the `id` object inside the images array must start with 0 and it has to      increment from there
        - Below is the sample array
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
                }
            ]
    2. slideDuration
        - Specify the value in millisecond (4000 is 4s, 5000 is 5s)
        - Amount of time after which the slider has to move to the next slide automatically


To understand what is happening , you can dowload this project and run it to understand how it works.

####Change 2
i have added SCSS package for development.

i have provided scss variables, so that you can make changes to font-size,background-color,font-color,height,width ...etc according to your project need.

i have made size calculation based on pixels, you can see it in the scss variables. 
If you need it change it to rem or em, you can just make changes in the scss variables, i have tried to make the code to adapt to changes in sizes. if you face any issue while making these changes , let me know.

Below is the npm command to install scss compiler into vuejs
```
    npm install sass-loader node-sass style-loader --save
```

##Change 3
i have introduced pause and play controls in image slider

`&#9658;` - unicode symbol which denotes Play slider

`&#10074;` -  unicode symbol which denotes Pause slider

This unicode may not work in some browsers, You could face browser compatibility issues.

In `Slider.vue` file there are two classes already defined.
```
.play{
    color: brown;
}
.pause{
    color: #580843;
}
```
You can introduce any icons or images into it. i will leave it to you.

i would've missed something here, but that is all i remember for now. 

if you have any queries or need any support on your project kindly raise an issue or contact me on twitter


You can find me on twitter @divine_rw
