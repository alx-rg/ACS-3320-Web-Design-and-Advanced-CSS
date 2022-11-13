# FEW 2.2 - Animation part 2

Use @keyframes to create more complex animations.  

## Why you should know this?

All of the best applications use motion to their advantage! You want your applications and the applications you are building to stand out!

## Learning Objectives

- Describing key framing
- Describe in betweening
- Use `@keyframes` define key frames
- Use `animation` to make things move

## key frames

Animation is the creation of many still images that are played back quickly giving the appearance of smooth motion. 

In animation the concept of key frames is the idea of drawing the extremes of a motion. For example a ball bouncing the extremes would the ball at the highest point and the ball at the highest point. 

![Key frames](images/keyframes-1.png)

Most often you are animating numeric values and these numbers represent your key frames. 

![Key frames](images/keyframes-2.png)

You could define these key frames with `@keyframe` in CSS like this: 

```CSS
@keyframes bounce {
	0% { top: 0; }
	100% { top: 200px; }
}
```

The extremes of the animation are 0 and 200px. The values between these numbers are the in betweens. 

Inbetweens are the frames that need to be generated between the key frames! 

This applies to every property that needs to be animated. 

Notice that you have placed keyframes along the length of the animation using %. The time has not been set yet but the first key frame applies at 0% of the length of the animation and the last key frame applies at the end or 100% the length of the animation! 

To apply this key frame to an object use the animation properties: 

```CSS
.ball {
  animation-name: bounce; /* Set the key frames */
  animation-duration: 2s; /* Set the duration  */
  animation-iteration-count: infinite; /* Set the repeats */
  animation-direction: alternate; /* Set the direction */
  animation-timing-function: ease-out;
}
```

Animation has more than a few properties. Try and remember the concepts, look up the property names if you forget them. 

The process of using animation: 

- Define some key frames with `@keyframes`
- Assign your keyframes to an object with `animation-name`
- Set the duration of the animation with `animation-duration`
- set the number of times the animation should repeat with `animation-iteration-count`

From there you might use other properties to modify the animation you created. 

- Use `animation-direction` to play the animation forward, backward, alternate (back and forth)
- Use `animation-timing-function` to change the "quality" of the motion. This chnages the math function that generates the inbetween values. 
- Use `animation-delay` to create a pause before the animation starts. 
- Use `animation-fill-mode` to determine what happens before and after the animation. Often you'll use this to make an object stop at the end point of the animation instead of snapping back to it's starting value.

## @Keyframes and animation example

Use these properties to create longer more complex animations that can be looped and repeated. 

To create keyframe animations define some keyframes. A keyframe describes the values for CSS properties at a point in time. 

Assign keyframe animation a name, `scaleAndRotate` in the example below. 

Define the value for properties along the length of the animation. Here `transform: scale(0.5) rotate(0)` happens at the beginning `0%`, `background-color: blue` happens at the half way point `50%`, and `transform: scale(1.0) rotate(23deg)` happens at the end of the animation `100%`.
```CSS
@keyframes scaleAndRotate {
  0% { transform: scale(0.5) rotate(0); }
  50% { background-color: blue; }
  100% { transform: scale(1.0) rotate(23deg); }
}
```

The code above defines the animation. Below the animation is applied to an element. 

The `animation` property applies an animation to an element. The line: `animation: scaleAndRotate 5s infinite` sets the animation to `scaleAndRotate` (matches the name above), sets the length of the animation 5 secs (`5s`), and repeat infinitely (`infinite`).

```CSS
div {
  width: 100px;
  height: 100px;
  background: red;
  position :relative;
  /* name duration iteration-count */
  animation: scaleAndRotate 5s infinite;
}
```

The animation property is the shorthand property for: 

- `animation-delay`
- `animation-duration`
- `animation-fill-mode`
- `animation-iteration-count`
- `animation-name`
- `animation-play-state`
- `animation-timing-function`

The code above could be broken into three lines: 

```CSS
animation-name: scaleAndRotate;
animation-duration: 5s;
animation-iteration-count: infinite;
```

## Challenges

The challenge for today is open ended. You will design your own loading animation. This can be anything you like. Take a look at the examples. 



## Activity 

 

## After Class 



## Additional Resources

1. https://www.smashingmagazine.com/2011/07/learning-to-use-the-before-and-after-pseudo-elements-in-css/
1. https://codersblock.com/blog/diving-into-the-before-and-after-pseudo-elements/
1. https://dev.to/ruppysuppy/css-decoded-before-and-after-1o56

