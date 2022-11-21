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


