# FEW 2.2 Lesson 4 - Background Images

## Learning Objectives 

- Use background images

## Video Lessons

https://www.youtube.com/playlist?list=PLoN_ejT35AEhF_M9vBuZgW0E4PiDb19oX

Watch videos: lesson 04 1-6

## Background Images

Images that appear in your web pages are either part of the content or part of the design.

Content images are things like: the picture of a product, the picture of a person like a user. Content images are a picture that the content of the page talks about. 

Images that are part of the design are just that part of the design. These images enhance the visual look and feel of the site but are not the actual content. 

Why make the distinction? Content images should be displayed using the `<img>` tag. This allows them to be indexed, searched for, and downloaded, and treated like information. 

As part of the content for a page, they will always be part of the content. 

Images that are part of the design need to avoid being indexed, searched, and saved. Design can change so these images should be separate from the content of the page. 

Images that are handled with the background image property in CSS are part of the design. 

### CSS Zen Garden Examples

The CSS Zen Garden uses background images exclusively. All of the images here are added via the background image property. The page doesn't have any content images.

Take a look at the CSS Zen Garden examples. 

### background-image

A background image appears on top of the background color but underneath the content. 

A background image fills a box out to the border, this includes the padding but doesn't fill the margin. 

Any element can have multiple backgrounds! This is a very powerful idea. Just separate each property with a comma to add a new element. 

The background-image property has the following properties:

- `background-image` - sets an image
- `background-repeat` - determines how the image repeats or tiles, can be on the x, y, or both axis
- `background-position` - sets the position of the image. You can set this with a keyword: left, top, right, bottom, or center. Or with a measurement like: 100px 50px. 
- `background-size` - Determines how an image fills the space. You can use a value to set the size, or you can use the keywords: cover or contain to determine how an image fills the space. 
- `background-attachment` - Determines how the image scrolls. An image can be fixed or it can scroll with the page. 

https://developer.mozilla.org/en-US/docs/Web/CSS/background

### background-color 

Any element can have a background color. This can be a solid color or a gradient. 

Colors can be set as:

- `#ff4433` - hex color 
- `rgb(255, 123, 45)` - rgb color
- `hsl(360, 100%, 50%)` - hsl color
- `rgba(255, 0, 0, 0.8)` - rgba (like rgb but includes alpha!)
- `hsla(360, 100%, 50%)` - hsla color (like hsl but includes alpha!)
- `red` - keyword color

- https://developer.mozilla.org/en-US/docs/Web/CSS/color_value/hsl()
- https://developer.mozilla.org/en-US/docs/Web/CSS/color_value/rgba()

### Gradients 

Any element can have a gradient fill. This replaces the color or can be combined with the color. 

Gradients can be linear or radial. 

- https://developer.mozilla.org/en-US/docs/Web/CSS/linear-gradient()
- https://developer.mozilla.org/en-US/docs/Web/CSS/radial-gradient()

Experiment with Gradient Generator: 

https://www.colorzilla.com/gradient-editor/


## Formulas

Find some images to use for this section. You can use your own images or search this site for free image resources: 

https://www.oxygenna.com

**Add a background image that covers the page.**

Use a repeating patterning and set it as the background: 

```CSS
body {
	background: url(./images/material-patterns/mp-01.png);
	background-size: 100px;
}
```

Notice I'm controlling the size of the pattern image with `background-size`!

This may make your text hard to read. Give text blocks a background color, something like: 

```CSS
body > div {
	margin: 2em;
	padding: 2em;
	background-color: rgba(255, 255, 255, 0.735);
}
```

**Use a single non-repeating image to fill a page.**

Here the background image is set in the body. Repeat is none, and the background-size is set to cover. 

```CSS
body {
	background-image: url(./images/md-backgrounds/mb-bg-fb-05.png);
	background-repeat: no-repeat;
	background-size: cover;
	background-position: center;
}
```

**Add a background image behind a section.**

Same idea as above but apply the background behind a div, section, or any block. 

```CSS
body section > div, .main > div {
	background-image: url(./images/md-backgrounds/mb-bg-fb-05.png);
	background-repeat: no-repeat;
	background-size: cover;
	background-position: center;

	margin: 2em;
	padding: 2em;
}
```

This idea would work with repeating patterns also. Here I changed the image and let it repeat. I also controlled the size of the pattern with `background-size`.

```CSS
body section > div, .main > div {
	background-image: url(./images/patterns-2-2/aztec.png);
	background-size: 100px;

	margin: 2em;
	padding: 2em;
}
```

You could also this idea only for a heading: 

```CSS
h1 {
	background-image: url(./images/patterns-2-2/aztec.png);
	background-size: 100px;

	margin: 2em;
	padding: 2em;
}
```

**Make a pattern that runs along the edge of a heading**

Here the background image is set to repeat only on the x and positioned on the y. Use padding to give your element some extra space to show the image.

```CSS
h1 {
	background-image: url(./images/patterns-2-2/spartans.png);
	background-size: 100px;
	background-repeat: repeat-x;
	background-position-y: 100px;

	margin: 2em;
	padding: 2em;
}
```

**Add an icon next to a heading**

Here we have an image with no repeat. Set the background-size to control the size of the image. I wanted to place the image on the left so I added padding on the left and positioned the image on the left and center vertical. 

```CSS
h1 {
	background-image: url(./images/animal-attributes-icons/ant-tenacity-colored.png);
	background-size: 100px;
	background-position: left center;
	background-repeat: no-repeat;
	padding-left: 100px;
}
```

**Add a "divider" above or below a section**

Add a background image. Use no-repeat, and position center bottom. Add some padding to leave space below your content to show the image. 

```CSS
.main > div {
	background-image: url(./images/decorative-elements/decoration-1.png);
	background-size: 300px;
	background-repeat: no-repeat;
	background-position: center bottom;
	padding-left: 2em;
	padding-top: 2em;
	padding-right: 2em;
	padding-bottom: 100px;
}
```

**Multiple background images**

To add more that one image you'll list the images each seprated by a comma. For example: 

```CSS
background-image: <image 1>, <image 2>, <image 3>;
```

Important! The first image is on top! The images are stacked top (first) to bottom (last.)

Other image properties, for example, repeat, size, position etc. can also be listed seprated by commas and are applied to the image at the same index. 

```CSS
background-position: <image 1>, <image 2>, <image 3>;
background-size: <image 1>, <image 2>, <image 3>;
background-repeat: <image 1>, <image 2>, <image 3>;
```

You can use mulitple images to places a gradient under a repeating pattern or other transparent image. You could place multiple icons in different locations. There are many possibilities. 

**Place an image to the left and/or right of a heading**

Here I used two images as the background for the same element! The background properties allow for multiple backgrounds separate the properties by a comma. 

Notice below the cat and dog images are each separated by a comma. The sizes are also. The position is the same but the first image is set to `left center`, and the second is set to `right center`. 

I added padding on the left and right to leave room for the images. 

I position the text I used text-align to center the text on the horizontal axis and set the `line-height` to center the text vertically.

```CSS
h1 {
	background-image: 
		url(./images/animal-attributes-icons/cat-agility-colored.png), 
		url(./images/animal-attributes-icons/cat-agility-colored.png);
	background-size: 100px, 100px;
	background-position: left center, right center;
	background-repeat: no-repeat, no-repeat;

	padding-left: 100px;
	padding-right: 100px;

	height: 100px;

	line-height: 100px;
	text-align: center;
}
```

Important! When using background-position you can create an offset by combining a keyword with a value. Here are a couple examples: 

```CSS
background-position: right center; /* Put the image at the right and vertical center */
background-position: right 10px center; /* offsets the image 10px from the right */
background-position: right center 20px; /* Offsets the image 20px from the vertical center */
```

## Challenges

Using the Zen Garden page try the following challenges. You will submit your solution styles to Gradescope. 

You can download a fresh copy of the Zen Garden HTML, again you are not allowed to change the markup! 

1. Add a gradient to the background of the page. 
2. Add a background image to the page that uses a repeating pattern. 
3. Add an avatar image to the upper left of the page. 
There should only be one image here and it should be sized to display reasonably. 
4. Style the example HTML and CSS file links as buttons. Add an icon to the right 
side of the button. The icon should not overlap the text and should not repeat. 
It should also be reasonably sized. 
5. Style the links in the footer to display like "buttons". You should hide the 
text, and display an icon in the center. The background image should not repeat. 
The icons should be reasonably sized. 

You can download the images [here](../images). 

Submit your work to GradeScope!

Here are some pictures. 

![challenge image 1](images/module-4-challenge-1.png)

This is footer. Notice the text is hidden and each link displays an image. 

![challenge image 2](images/module-4-challenge-2.png)

## After Class

Continue working on your CSS Zen Garden Page. Use the concepts from class to solve these problems: 

- Use background images on your page. Try these ideas: 
	- Use a single image or a repeating pattern to fill the background. 
	- Use an image as a background for a heading, card, or section. 
	- Use an image to add an icon next to a heading link or button. 
- Use a Gradient
	- Use a gradient to fill the background of the page. 
	- Use a gradient as a background to a heading or section

## Resources 

- [Image Resources](https://www.oxygenna.com)
- [CSS Background](https://developer.mozilla.org/en-US/docs/Web/CSS/background)
- [Linear Gradient](https://developer.mozilla.org/en-US/docs/Web/CSS/linear-gradient())
- [Radial Gradient](https://developer.mozilla.org/en-US/docs/Web/CSS/radial-gradient())
- [HSLA Color](https://developer.mozilla.org/en-US/docs/Web/CSS/color_value/hsl())
- [RGBA Color](https://developer.mozilla.org/en-US/docs/Web/CSS/color_value/rgba())