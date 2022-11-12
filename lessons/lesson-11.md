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

## @Keyframes and animation

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










## Research Pseudo-elements

Read this article. It talks about the uses for ::before and ::after. 

https://css-tricks.com/pseudo-element-roundup/

## Custom Checkboxes and radio buttons

The checkbox and radio button are limited in what the browser allows you to style. With Pseudo-elements we open up the possibility to customize these elements. 

### How are checkboxes and radio buttons marked up?

Usually you will want to markup up checkboxes and radio buttons like this: 

```HTML
<label>
	<input type="checkbox">
	Pickles?
</label>

<label>
	<input type="radio" name="choice" checked>
	Converse
</label>

<label>
	<input type="radio" name="choice">
	Vans
</label>
```

The label is an important element here. Besides providing a label that can be read, the label provides an element that can be interacted with. 

**With the label wrapped around the input clicking the label is the same as clicking the input.**

What are the elements needed for a checkbox or radio button? 

![checkbox radio](images/checkbox-radio.png)

The checkbox or radio button is usually made of two parts a container, a box or circle, and a mark, check, or dot. The mark is sometimes visible and sometimes not. 

This can also be more complicated than what is presented here but these are the basic elements or starting place to create checkboxes and radio buttons. 

To make this possible we need to add a little more markup. The markup presented above doesn't allow us enough to control the checkbox with CSS alone. By adding one extra tag we can do that. 

```HTML
<label>
	<input type="checkbox">
	<span>Pickles?</span>
</label>

<label>
	<input type="radio" name="choice">
	<span>Converse</span>
</label>

<label>
	<input type="radio" name="choice">
	<span>Vans</span>
</label>
```

With the extra span, you can use the + or ~ selectors to connect the span with the input. More on this below. 

Since we are going to include this in our frameworks it's probably best to make it something that is opt-in. Do this by adding a class name: 

```HTML
<label class="frmwrk-checkbox">
	...
</label>

<label class="frmwrk-radio">
	...
</label>

<label class="frmwrk-radio">
	...
</label>
```

By including the class frmwork-checkbox or frmwrk-radio you'll get the fancy checkboxes and radio buttons. Without these classes, you get the standard checkbox and radio buttons. 

You'll need 5 selectors. Here they without their inner styles. Each of these performs a different function. Read the comments below. 

```CSS
/* checkbox button base element */
.frmwrk-checkbox > span {
	...
}
/* Selected "checkmark" styles */
.frmwrk-checkbox > input[type=checkbox] + span::before {
	... 
}
/* Selected "mark" styles */
.frmwrk-checkbox > input[type=checkbox]:checked + span::before {
	...
}
/* Outline */
.frmwrk-checkbox > input[type=checkbox] + span::after {
	...
}
/* Hide the input */
.frmwrk-checkbox input {
	...
}
```

- base element - sets the style of the label and its children
	- .frmwrk-checkbox > span
- Selected "checkmark" - Sets the style for the pseudo-element that appears in the box or circle. The selector here selects the ::before an element of the span that immediately follows the input with type=checkbox
	- .frmwrk-checkbox > input[type=checkbox] + span::before
	- https://www.w3schools.com/cssref/sel_element_pluss.asp
- Selected "mark" - Sets the style for the checkmark when the mark is visible or selected. The selector here says: select the ::before the pseudo-element that belongs to the span that immediately follows an input with type=checkbox. 
	- .frmwrk-checkbox > input[type=checkbox]:checked + span::before
	- https://developer.mozilla.org/en-US/docs/Web/CSS/:checked
- Outline - Styles the box or circle that contains the mark. The selector here says to select an input that has type=checkbox that is a child of an element with class frmwrk-checkbox. 
	- .frmwrk-checkbox > input[type=checkbox] + span::after
	- https://www.w3schools.com/css/css_attribute_selectors.asp

With these selectors, you're ready to make some custom checkboxes or radio buttons. 

You can see the full source code for the examples above here: 

- Fancy Blockquote - [lesson-08-fancy-blockquote.html](lesson-08-fancy-blockquote.html)
- Fancy Underline - [lesson-08-fancy-underline.html](lesson-08-fancy-underline.html)
- Custom Checkboxes and Radio Buttons - [lesson-08-custom-checkboxes-radio-buttons.html](lesson-08-custom-checkboxes-radio-buttons.html)

There are many articles here are a few that I picked out. You can follow these to help guide or inspire and provide direction. 

- https://www.appitventures.com/blog/styling-checkbox-css-tips
- https://www.w3schools.com/howto/howto_css_custom_checkbox.asp
- https://codepen.io/Vestride/pen/dABHx


## Activity 

Create your custom checkboxes and radio buttons. Add these to your CSS framework. 

## After Class 

Use the ideas above and add styles for "fancy" block quotes to your CSS framework.

## Additional Resources

1. https://www.smashingmagazine.com/2011/07/learning-to-use-the-before-and-after-pseudo-elements-in-css/
1. https://codersblock.com/blog/diving-into-the-before-and-after-pseudo-elements/
1. https://dev.to/ruppysuppy/css-decoded-before-and-after-1o56

