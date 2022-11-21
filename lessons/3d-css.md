# CSS in 3D

CSS provides a set of 3D transformations. These allow you to position and animat objects along the x, y, and z axese. 

3D transformations benefit from using hardware acceleration. This means that the browser will draw elements using 3d transforms more efficiently. The take away here is that using a 3d transfrom even when performing a 2d transformation will be more performant! 

## What's 3d? 

3d stands for 3 dimensional. When something is 2 dimensional, or 2d, it can be transformed along two axese. Imagine a peice of paper or other flat surface. Objects that move along the surface of the paper are moving in two dimensions. 

We give each axis a name. The x axis runs horizontally left and right, and y axis runs vertically top to bottom. 

Adding a 3rd dimension we add the z axis. The z axis cross the x and y axis at 90 degrees. Imagine your object moving backward or forward in space. 

As objects move forward in space they appear to be larger, and as the move backward in space they get smaller with greater distance from the picture plane. 

## CSS in 3d

To transform an object in 3d you need do the following:

Use one of the 3d transforms. These are: 

- rotateX()
- rotateY()
- rotateZ()
- rotate3d()
- translateX()
- translateY()
- translateZ()
- translate3d()
- scaleX()
- scaleY()
- scaleZ()
- scale3d()
- matrix3d()

You also must set the persepctive. 

- perspective()

Here's a simple example:

```CSS
div {
  background-color: tomato;
  height: 100px;
  width: 100px;

  transform: perspective(400px) rotateY(45deg);
}
```

## What is perspective doing? 

When things are drawn in 3d there is some foreshortening. You see this when things get smaller the further they move into the distance. The amount of foreshortening is determined by the perspective value. 

- https://developer.mozilla.org/en-US/docs/Web/CSS/perspective
- https://css-tricks.com/almanac/properties/p/perspective/

Smaller numbers for perspective will make the foreshortening more extreme and larger numbers will make the effect more mild. 

## Other 3d properties

**backface-visibility**

This determines what happens when an object is rotated so that you are seeing the back side. You can set this to hidden and the object will not be visible from the back, you will opnly be able to see from the front!

Why do this? If you want to create an animation that flips something over revealing the another item you can make two elements, position them back to back, then flip one 180 degrees. See the example below: 

```HTML
<!-- Outer box with border -->
<div class="container">
  <div class="box"><!-- Inner container -->
    <div>Front</div><!-- front face -->
    <div>Back</div><!-- backface -->
  </div>
</div>

<style>

  .container {
    width: 200px;
    height: 200px;
    display: flex;
    justify-content: center;
    align-items: center;
    border: 1px solid;
  } 

  .box {
    /* This is a red box that rotates on the y axis */
    width: 120px;
    height: 120px;
    background-color: tomato;
    position: relative;
    /* This property determines whether children of the element
    are flattened or transformed in 3d. See: https://developer.mozilla.org/en-US/docs/Web/CSS/transform-style */
    transform-style: preserve-3d;
    -webkit-transform-style: preserve-3d;
    /* Apply the animation below */
    animation-name: spin;
    animation-duration: 4000ms;
    animation-iteration-count: infinite;
    animation-timing-function: linear;
  }

  .box > div {
    /* This is a circle with the word front or back */
    width: 100px;
    height: 100px;
    background-color: wheat;
    font-size: 24px;
    text-align: center;
    line-height: 100px;
    border-radius: 50%;
    position: absolute;
    left: 10px;
    top: 10px;
    backface-visibility: hidden;
    -webkit-backface-visibility: hidden;
  }

  .box > div:last-child {
    /* The back circle is flipped 180deg */
    transform: rotateY(180deg);
  }

  /* Notice we're animating the rotateY property! */
  @keyframes spin {
    0% {
      transform: perspective(400px) rotateY(0);
    }

    100% {
      transform: perspective(400px) rotateY(360deg);
    }
  }

  body, html {
    heigh: 100%;
  }

  body {
    display: flex;
    justify-content: center;
    align-items: center;
  }

</style>
```

Here the inner div .box is rotating. It has two inner divs. These children rotate with their parent. 

The two divs inside of .box are positioned back to back and they are backface hidden. This means when they flip over the front face of one is facing us and the backside of the other. 

**Lets make that interactive!**

```HTML
<div class="container">
  <div class="box">
    <div>Front</div>
    <div>Back</div>
  </div>
</div>

<style>
  .container {
    width: 200px;
    height: 200px;
    display: flex;
    justify-content: center;
    align-items: center;
    border: 1px solid;
  }

  .box {
    width: 120px;
    height: 120px;
    background-color: tomato;
    position: relative;
    /* Required to preserve 3d transformations on children
    This property determines whether children of the element
    are flattened or transformed in 3d. See: https://developer.mozilla.org/en-US/docs/Web/CSS/transform-style */
    transform-style: preserve-3d;
    /* For browser support and compatibility */
    -webkit-transform-style: preserve-3d;
    animation-name: spin;
    animation-duration: 4000ms;
    animation-iteration-count: infinite;
    animation-timing-function: linear;

    transform: perspective(400px) rotateY(0);
    transition: 1000ms;
  }

  .container:hover>.box {
    transform: perspective(400px) rotateY(180deg);
  }

  .box > div {
    width: 100px;
    height: 100px;
    background-color: wheat;
    font-size: 24px;
    text-align: center;
    line-height: 100px;
    border-radius: 50%;
    position: absolute;
    left: 10px;
    top: 10px;
    /* Hides the back side of 3d elements */
    backface-visibility: hidden;
    -webkit-backface-visibility: hidden;
  }

  .box>div:last-child {
    /* Flip the back side element */
    transform: translateZ(-1px) rotateY(180deg);
  }

  body,
  html {
    height: 100%;
  }

  body {
    display: flex;
    justify-content: center;
    align-items: center;
  }
</style>
```

Notice here that hovering over the container cause the rotation on .box to transition to 180deg. 

## More ideas

Here are some more ideas for using animation: 

```HTML

<!-- Topics

  This page contains some examples and ideas that you can borrow 
  ideas from. Use to review the concepts from the previous classes.

  1. transitions
    What is a transition? Change in value from one value to another

  2. Easing 
    What is easing? Easing how changes are applied. 
    https://matthewlein.com/tools/ceaser
    https://developer.mozilla.org/en-US/docs/Web/CSS/easing-function
    https://easings.net
    https://css-tricks.com/ease-out-in-ease-in-out/

  3. Keyframes 
    Key frames are the significant points in an animation. 
    You can think of these often as the extremes. Something is all the way to left or the right
  
  4. In betweens, tweens, tweening, and transitions
    Are the process of creating the images that fall between the key frames. 
    The number of inbetween frames is dtermined by the duration of the transition. 

  5. Transitions 


-->


<!-- Continuous animations 

  Use key frame animation to 
-->

<div class="container">


  <!-- ***************************************** -->
  <!-- Circle Spin -->
  <div class="example">
    <div class="box-1"></div>
    <style>
      .box-1 {
        width: 100px;
        height: 100px;
        border-radius: 50%;
        border-left: 18px solid gold;
        border-top: 18px solid cornflowerblue;
        border-right: 18px solid crimson;
        border-bottom: 18px solid;
        /* Use a key frame animation */
        animation-name: spin; /* Set the name of the animation it's defined below */
        animation-duration: 2000ms; /* Set the the duration of the animation */
        animation-iteration-count: infinite; /* Set the number of times the animation will repeat */
        animation-timing-function: linear; /* Set the timing function. */
      }

      /* Define some keyframes */
      /* The name of this animation is spin */
      @keyframes spin {
        /* Define the values at the beginning */
        0% { 
          transform: rotateZ(0);
        }
        /* Define the values at the end */
        100% {
          transform: rotateZ(360deg);
        }
      }
    </style>
  </div>


  <!-- **************************************************** -->
  <!-- Circle Spin 2 -->
  <div class="example">
    <div class="box-2"></div>
    <style>
      .box-2 {
        width: 100px;
        height: 100px;
        border-radius: 50%;
        border-left: 18px solid gold;
        border-top: 18px solid cornflowerblue;
        border-right: 18px solid crimson;
        border-bottom: 18px solid transparent;
        animation-name: spin; /* We can reuse the spin animation here */
        animation-duration: 3000ms;
        animation-timing-function: linear;
        animation-iteration-count: infinite;
      }
    </style>
  </div>


  <!-- **************************************************** -->
  <!-- Arrow Spin -->
  <div class="example">
    <div class="box-3">
      <div></div>
      <div></div>
    </div>

    <style>
      .box-3 {
        /* border: 1px solid; */
        width: 100px;
        height: 100px;
        animation-name: spin;
        animation-duration: 3000ms;
        animation-timing-function: linear;
        animation-iteration-count: infinite;
      }

      .box-3 > div:first-child {
        position: absolute;
        transform: translate(0, 0);
        width: 64px;
        height: 64px;
        border-radius: 50%;
        border-left: 18px solid;
        border-top: 18px solid;
        border-right: 18px solid;
        border-bottom: 18px solid transparent;
      }

      .box-3 > div:last-child {
        width: 20px;
        height: 20px;
        border-left: 18px solid;
        border-top: 18px solid;
        position: absolute;
        transform: translate(60px, 57px) rotate(-90deg);
      }
    </style>
  </div>


  <!-- **************************************************** -->
  <div class="example">
    <div class="boxes">
      <div></div>
      <div></div>
      <div></div>
    </div>

    <style>
      .boxes {
        width: 100px;
        height: 100px;
        position: relative;
      }
      /* These styles apply to all child divs */
      .boxes > div {
        position: absolute;
        width: 100px;
        height: 100px;
        border-radius: 50%;
        border-width: 18px;
        border-style: solid;
        border-color: transparent;
        animation-name: spin; /* We can reuse the spin animation here */
        animation-timing-function: linear;
        animation-iteration-count: infinite;
      }

      /* For each div use a different color and duration */
      .boxes > div:nth-child(1) {
        border-left-color: gold;
        animation-duration: 2000ms;
      }

      .boxes > div:nth-child(2) {
        border-left-color: crimson;
        animation-duration: 1500ms;
      }

      .boxes > div:nth-child(3) {
        border-left-color: cornflowerblue;
        animation-duration: 2500ms;
      }

    </style>
  </div>


  <!-- **************************************************** -->
  <div class="example">
    <div class="leaves">
      <div></div>
      <div></div>
      <div></div>
      <div></div>
    </div>

    <style>
      .leaves {
        width: 100px;
        height: 100px;
        position: relative;
      }
      /* These styles apply to all child divs */
      .leaves > div {
        position: absolute;
        width: 100px;
        height: 100px;
        border-radius: 0 50% 50% 50%;
        border-width: 18px;
        border-style: solid;
        border-color: rgba(153, 205, 50, 0.484);
        /* Set the animation name and duration for each leaf below */
        animation-timing-function: linear;
        animation-iteration-count: infinite;
        animation-direction: alternate; /* Use this to play the animation forward and reverse */
      }

      /* For each div use a different color and duration */
      .leaves > div:nth-child(1) {
        animation-name: open-cw;
        animation-duration: 4000ms;
      }

      .leaves > div:nth-child(2) {
        animation-name: open-cw;
        animation-duration: 6000ms;
      }

      .leaves > div:nth-child(3) {
        animation-name: open-ccw;
        animation-duration: 4000ms;
      }

      .leaves > div:nth-child(4) {
        animation-name: open-ccw;
        animation-duration: 6000ms;
      }

      @keyframes open-cw {
        0% {
          transform: rotate(45deg);
        }

        100% {
          transform: rotate(135deg);
        }
      }

      @keyframes open-ccw {
        0% {
          transform: rotate(45deg);
        }

        100% {
          transform: rotate(-45deg);
        }
      }

    </style>
  </div>




  <!-- **************************************************** -->
  <div class="example">
    <div class="clock">
      <div></div>
      <div></div>
      <div></div>
    </div>

    <style>
      .clock {
        width: 100px;
        height: 100px;
        position: relative;
        border: 1px solid;
        border-radius: 50%;
      }
      /* These styles apply to all child divs */
      .clock > div {
        width: 4px;
        height: 50px;
        position: absolute;
        left: 48px;
        background-color: teal;
        transform-origin: 50% 100%;

        animation-name: spin;
        animation-timing-function: linear;
        animation-iteration-count: infinite;
      }

      /* second hand */
      .clock > div:nth-child(1) {
        background-color: tomato;
        animation-duration: 600ms;
      }

      /* minute hand */
      .clock > div:nth-child(2) {
        animation-duration: 36000ms;
      }

      /* hour hand */
      .clock > div:nth-child(3) {
        animation-duration: 216000ms;
      }

    </style>
  </div>


  <!-- **************************************************** -->
  <!-- Eye -->
  <div class="example">
    <div class="eye">
      <div>
        <div></div>
      </div>
    </div>
    <style>
      .eye {
        width: 100px;
        height: 100px;
        border-radius: 0 50% 0 50%;
        border: 1px solid;
        transform: rotate(-45deg);
        position: relative;
        overflow: hidden;
        animation-name: blink;
        animation-duration: 1000ms;
        animation-iteration-count: infinite;
      }

      .eye > div {
        position: absolute;
        background-color: chocolate;
        width: 80px;
        height: 80px;
        border-radius: 50%;
        transform: translate(10px, 10px);
        animation-name: look;
        animation-duration: 5000ms;
        animation-iteration-count: infinite;
      }

      .eye > div > div {
        position: absolute;
        background-color: black;
        width: 40px;
        height: 40px;
        border-radius: 50%;
        transform: translate(20px, 20px)
      }

      /* Here the animation is broken down into several steps */
      @keyframes look {
        0% {
          transform: translate(10px, 10px);
        }

        25% {
          transform: translate(10px, 10px);
        }

        30% {
          transform: translate(-20px, -15px);
        }

        50% {
          transform: translate(-20px, -15px);
        }

        55% {
          transform: translate(10px, 10px);
        }

        70% {
          transform: translate(10px, 10px);
        }

        75% {
          transform: translate(40px, 35px);
        }

        90% {
          transform: translate(40px, 35px);
        }

        100% {
          transform: translate(10px, 10px);
        }
      }
    </style>
  </div>

  <!-- Battery -->
  <!-- <div class="example">
    <div class="box-4">
      <div></div>
    </div>
  </div> -->

  <!-- M Spin -->
  <!-- <div class="example">
    <div class="box-5">
      <div>
        <div>M</div>
      </div>
    </div>
  </div> -->

  <!-- MH Spin -->
  <!-- <div class="example">
    <div class="box-9">
      <div>
        <div>M</div>
        <div>E</div>
      </div>
    </div>
  </div> -->
  
  <!-- ****************************************** -->
  <!-- Buttons -->

  <!-- Simple Button 1 -->
  <div class="example">
    <button class="button-1">Hello</button>
    <style>
      .button-1 {
        padding: 1rem;
        border-radius: 0.5rem;
        background-color:rgb(0, 143, 190);
        color: #fff;
        border: 1px solid;
        font-size: 20px;
        transition: 350ms; /* Set the transition time */
      }

      /* Change the color and background color */
      .button-1:hover {
        color:rgb(0, 143, 190);
        background-color: #fff;
      }
    </style>
  </div>




  <!-- Simple button 2 -->
  <div class="example">
    <button class="button-2">Hello</button>
    <style>
      .button-2 {
        padding: 1rem;
        color: rgb(0, 143, 190);
        border: none;
        border-top: 4px solid transparent;
        border-bottom: 4px solid transparent;
        font-size: 20px;
        background-color: #fff;
        transition: 300ms; /* Set the time for the animation */
      }

      /* Animate the borders and letter spacing */
      .button-2:hover {
        border-top: 4px solid rgb(0, 143, 190);
        border-bottom: 4px solid rgb(0, 143, 190);
        letter-spacing: 0.25rem;
      }

    </style>
  </div>




  <!-- Another button -->
  <div class="example">
    <button class="button-3">Hello</button>
    <style>
      .button-3 {
        font-size: 20px;
        padding: 1rem;
        border-radius: 0.5rem;
        border: 1px solid;
        color:rgb(0, 143, 190);
        background-color: #fff;
        transition: 350ms;
      }

      .button-3:hover {
        background-color:rgb(0, 143, 190);
        color: #fff;
      }
    </style>
  </div>




    <!-- ******************************************* -->
    <!-- Hamburger X 2 -->
    <div class="example">
      <div class="l">
        <div></div>
        <div></div>
        <div></div>
      </div>
      <span>Hamburger 2</span>
    </div>
    <!-- Styles for Hamburger X 2 -->
    <style>
      /* Make a Hamburger menu with three horizontal bars */
      
      .l {
        border: solid 1px black;
        width: 100px;
        height: 100px;
        transition: 200ms;
      }
      
      .l>div {
        width: 60px;
        height: 10px;
        background-color: black;
        position: absolute;
      }
      
      .l>div:nth-child(1) {
        transform: translate(20px, 25px) rotate(0);
        transition: 200ms;
      }
      
      .l>div:nth-child(2) {
        opacity: 1;
        transform: scale(1, 1) translate(20px, 45px) rotate(0);
        transition: 200ms;
      }
      
      .l>div:nth-child(3) {
        transform: translate(20px, 65px) rotate(0);
        transition: 200ms;
      }
      
      .l:hover {
        background-color: black;
      }
      
      .l:hover>div {
        background-color: white;
      }
      /* Animate the three bars */
      
      .l:hover>div:nth-child(1) {
        transform: translate(20px, 45px) rotate(45deg);
      }
      /* Change the scale x to 0 */
      
      .l:hover>div:nth-child(2) {
        opacity: 0;
        transform: scale(0, 1) translate(20px, 45px) rotate(0);
      }
      
      .l:hover>div:nth-child(3) {
        transform: translate(20px, 45px) rotate(-45deg);
      }
  
    </style>
    <!-- ******************************************* -->
  





    <!-- ******************************************* -->
    <!-- Hamburger X 3 -->
    <div class="example">
      <div class="m">
        <div></div>
        <div></div>
        <div></div>
      </div>
      <span>Hamburger 3</span>
    </div>
    <!-- Styles for Hamburger X 3 -->
    <style>
      /* Start with a hamburger made from three horizontal 
      bars. These will form an arrow on hover. */
      
      .m {
        border: solid 1px black;
        width: 100px;
        height: 100px;
        transition: 200ms;
      }
      
      .m>div {
        width: 60px;
        height: 10px;
        background-color: black;
        position: absolute;
      }
      
      .m>div:nth-child(1) {
        transform: translate(20px, 25px) rotate(0);
        transition: 200ms;
      }
      
      .m>div:nth-child(2) {
        opacity: 1;
        transform: scale(1, 1) translate(20px, 45px) rotate(0);
        transition: 200ms;
      }
      
      .m>div:nth-child(3) {
        transform: translate(20px, 65px) rotate(0);
        transition: 200ms;
      }
      
      .m:hover {
        background-color: black;
      }
      
      .m:hover>div {
        background-color: white;
      }
      
      .m:hover>div:nth-child(1) {
        width: 53px;
        transform: translate(10px, 30px) rotate(-45deg);
      }
      
      .m:hover>div:nth-child(2) {
        transform: translate(20px, 45px) rotate(0);
      }
      
      .m:hover>div:nth-child(3) {
        width: 53px;
        transform: translate(10px, 60px) rotate(45deg);
      }
  
    </style>
    <!-- ******************************************* -->
  



    <!-- ******************************************* -->
    <!-- Hamburger X 4 -->
    <div class="example">
      <div class="n">
        <div></div>
        <div></div>
        <div></div>
      </div>
      <span>Hamburger 4</span>
    </div>
    <!-- Styles for Hamburger X 4 -->
    <style>
      .n {
        border: solid 1px black;
        width: 100px;
        height: 100px;
        transition: 200ms;
      }
      
      .n>div {
        width: 60px;
        height: 10px;
        background-color: black;
        position: absolute;
      }
      
      .n>div:nth-child(1) {
        transform: translate(20px, 25px) rotate(0);
        transition: 200ms;
      }
      
      .n>div:nth-child(2) {
        border: none;
        border-radius: 0;
        transform: translate(20px, 45px);
        transition: 200ms;
      }
      
      .n>div:nth-child(3) {
        transform: translate(20px, 65px) rotate(0);
        transition: 200ms;
      }
      
      .n:hover {
        background-color: black;
      }
      
      .n:hover>div {
        background-color: white;
      }
      
      .n:hover>div:nth-child(1) {
        width: 50px;
        transform: translate(25px, 45px) rotate(45deg);
      }
      /* This div changes from a bar to circle */
      
      .n:hover>div:nth-child(2) {
        width: 60px;
        height: 60px;
        background-color: transparent;
        border: 10px solid white;
        border-radius: 50%;
        transform: translate(10px, 10px);
      }
      
      .n:hover>div:nth-child(3) {
        width: 50px;
        transform: translate(25px, 45px) rotate(-45deg);
      }
  
    </style>
    <!-- ******************************************* -->




    <!-- Card animations the styles for these are below -->
  <div class="example">
    <div class="box-6">
      <img src="kitten-domo.jpg">
    </div>
  </div>

  <div class="example">
    <div class="box-7">
      <img src="kitten-domo.jpg">
      <h3>Domo Kitten</h3>
    </div>
  </div>

  <div class="example">
    <div class="box-8">
      <img src="kitten-domo.jpg">
      <h3>Domo Kitten</h3>
      <p>$5.99</p>
    </div>
  </div>


  <!-- Button ripple effect -->
  <div class="example">
    <div class="boop">
      <div></div>
    </div>
  </div>

  <style>
    .boop {
      width: 100px;
      height: 100px;
      background-color: tomato;
      position: relative;
    }

    .boop > div {
      position: absolute;
      width: 10px;
      height: 10px;
      background-color: rgba(255,255,255, 0.5);
      border-radius: 50%;
      left: 50%;
      top: 50%;
      
      /* Circle expanded and transparent */
      opacity: 0;
      transform: translate(-50%, -50%) scale(12);
      transition: 200ms;
    }

    /* When clicked set the time to 0 and the size to small and opaque */
    .boop:active > div {
      opacity: 1;
      transform: translate(-50%, -50%) scale(0);
      transition: 0ms;
    }
  </style>


<div class="example">
  <div class="boop">
    <div></div>
  </div>
</div>

<style>
  .boop {
    width: 100px;
    height: 100px;
    background-color: tomato;
    position: relative;
  }

  .boop > div {
    position: absolute;
    width: 10px;
    height: 10px;
    background-color: rgba(255,255,255, 0.5);
    border-radius: 50%;
    left: 50%;
    top: 50%;
    opacity: 0;
    transform: translate(-50%, -50%) scale(12);
    transition: 200ms;
  }

  .boop:active > div {
    opacity: 1;
    transform: translate(-50%, -50%) scale(0);
    transition: 0ms;
  }
</style>
</div>

<style>


  .box-4 {
    width: 40px;
    height: 100px;
    border: 4px solid;
    border-radius: 10px;
    overflow: hidden;
    position: relative;
  }

  .box-4 > div:first-child {  
    width: 100%;
    height: 10px;
    background-color: yellowgreen;
    position: absolute;
    bottom: 0;
    animation-name: power;
    animation-duration: 6000ms;
    animation-delay: 3000ms;
    animation-timing-function: linear;
    animation-iteration-count: infinite;
    animation-fill-mode: both;
  }


  .box-5 > div {
    width: 100px;
    height: 100px;
    background-color: tomato;
    transform: perspective(300px);
    animation-name: flip;
    animation-duration: 2000ms;
    animation-timing-function: linear;
    animation-iteration-count: infinite;
  }

  .box-5 > div > div {
    width: 60px;
    height: 60px;
    border-radius: 50%;
    transform: translate(20px, 20px);
    background-color: azure;
    font-size: 30px;
    text-align: center;
    line-height: 60px;
    font-weight: bold;
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  }

  .box-6 {
    width: 200px;
    height: 240px;
    border: 1px solid;
    overflow: hidden;
    position: relative;
  }

  .box-6 > img {
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%) scale(0.65) rotate(0);
    transition: 400ms;
  }

  .box-6:hover > img {
    transform: translate(-50%, -50%) scale(0.85) rotate(12deg);
  }



  .box-7 {
    width: 200px;
    height: 240px;
    border: 1px solid;
    overflow: hidden;
    position: relative;
  }

  .box-7 > img {
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%) scale(0.65) rotate(0);
    transition: 400ms;
  }

  .box-7:hover > img {
    transform: translate(-50%, -50%) scale(0.85) rotate(12deg);
  }

  .box-7 > h3 {
    position: absolute;
    right: -200px;
    bottom: 0;
    background-color: #fff;
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
    padding: 0.5rem 2.5rem 0.5rem 1.5rem;
    clip-path: polygon(0 0, 100% 1%, 100% 100%, 0 100%, 10% 49%);
    transition: 600ms;
    transition-timing-function: cubic-bezier(0.600, -0.280, 0.735, 0.045);
  }

  .box-7:hover > h3 {
    right: -20px;
  }
 


  .box-8 {
    width: 200px;
    height: 240px;
    border: 1px solid;
    overflow: hidden;
    position: relative;
  }

  .box-8 > img {
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%) scale(0.65) rotate(0);
    transition: 400ms;
  }

  .box-8:hover > img {
    transform: translate(-50%, -50%) scale(0.85) rotate(12deg);
  }

  .box-8 > h3 {
    position: absolute;
    right: -20px;
    bottom: 0;
    background-color: #fff;
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
    padding: 0.5rem 2.5rem 0.5rem 1.5rem;
    clip-path: polygon(0 0, 100% 1%, 100% 100%, 0 100%, 10% 49%);
    transition: 600ms;
    transition-timing-function: cubic-bezier(0.600, -0.280, 0.735, 0.045);
  }

  .box-8:hover > h3 {
    right: -200px;
  }

  .box-8 > p {
    width: 100px;
    height: 100px;
    border-radius: 50%;
    position: absolute;
    left: -14px;
    top: -14px;
    background-color: rgb(244, 93, 93);
    color: #fff;
    font-size: 24px;
    line-height: 100px;
    margin: 0;
    text-align: center;
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
    transition: 600ms;
    transition-timing-function: ease-in-out;
    transition-delay: 100ms;
    transform: translate(-100px, -100px) scale(0.5);
  }

  .box-8:hover > p {
    transform: translate(0, 0) scale(1);
  }
  
  .box-9 > div {
    width: 100px;
    height: 100px;
    background-color: tomato;
    transform: perspective(300px);
    animation-name: flip;
    animation-duration: 2000ms;
    animation-timing-function: linear;
    animation-iteration-count: infinite;
  }

  .box-9 > div > div:first-child {
    width: 60px;
    height: 60px;
    border-radius: 50%;
    position: absolute;
    transform: translate(20px, 20px);
    backface-visibility: hidden;
    background-color: azure;
    font-size: 30px;
    text-align: center;
    line-height: 60px;
    font-weight: bold;
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  }

  .box-9 > div > div:last-child {
    opacity: 0;
    width: 60px;
    height: 60px;
    border-radius: 50%;
    position: absolute;
    backface-visibility: hidden;
    transform: translate(20px, 20px) rotateY(180deg);
    background-color: azure;
    font-size: 30px;
    text-align: center;
    line-height: 60px;
    font-weight: bold;
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  }

  @keyframes power {
    0% {
      height: 0;
      background-color: yellowgreen;
    }

    100% {
      height: 90%;
      background-color: tomato;
    }
  }

  @keyframes flip {
    0% {
      transform: perspective(300px) rotateY(0);
    }

    100% {
      transform: perspective(300px) rotateY(360deg);
    }
  }

  .atom {
    width: 20px;
    height: 20px;
    background-color: darkturquoise;
    animation-name: orbit;
    animation-duration: 3000ms;
    animation-timing-function: linear;
  }

  @keyframes orbit {
    0% {
      transform-origin: 20px 0;
    }

    25% {
      transform-origin: 40px 0;
    }

    50% {
      transform-origin: 20px 0;
    }

    75% {
      transform-origin: 40px 0;
    }

    100% {
      transform-origin: 20px 0;
    }
  }


  .button {
    cursor: pointer;
    width: 100px;
    height: 30px;
    padding: 5px 10px;
    margin: 2em;
    border: 2px solid deepskyblue;
    background-color: deepskyblue;
    color: white;
    border-radius: 5px;
    font-size: 20px;
    transition: 400ms;
    overflow: hidden;
    position: relative;
  }

  .button:after {
    content: "";
    background-color: #FFFFFF;
    border-radius: 50%;
    width: 10px;
    height: 10px;
    display: block;
    position: absolute;
    left: 50%;
    top: 50%;

  }

  .button:hover {
    border-color:rgb(0, 143, 190);
    color:rgb(0, 90, 121);
  }


/* button 2 */
  .button2 {
    position: relative;
    background-color: rgb(76, 135, 175);
    border: none;
    font-size: 28px;
    color: #FFFFFF;
    padding: 20px;
    width: 200px;
    text-align: center;
    -webkit-transition-duration: 0.4s; /* Safari */
    transition-duration: 0.4s;
    text-decoration: none;
    /* overflow: hidden; */
    cursor: pointer;
  }

  .button2:after {
    content: "";
    background: rgb(255, 0, 0);
    display: block;
    position: absolute;
    padding-top: 300%;
    padding-left: 350%;
    margin-left: -20px!important;
    margin-top: -120%;
    opacity: 0;
    transition: all 0.8s;
  }

  .button2:active:after {
    padding: 0;
    margin: 0;
    opacity: 1;
    transition: 0s;
  }


  .example {
    /* border: 1px solid; */
    margin: 1rem;
    width: 200px;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
  }

  .container {
    width: calc((200px + (2 * 1rem)) * 3);
    margin: auto;
    display: flex;
    flex-wrap: wrap;
  }

  body {
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  }
</style>
```


