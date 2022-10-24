# Media Queries 

Media queries are used to modify your styles based on the general type and or specific characteristics of a device. 

Most often media queries are used to create responsive web pages. 

Media types are: 

- all
- print
- screen

Media features are: 

- any-hover
- any-point 
- aspect-ratio
- color
- color-gamut
- color-index
- device-aspect-ratio
- device-height
- device-width
- display-mode
- dynamic-range
- forced-colors
- grid
- height
- hover
- inverted-colors
- monchrome
- orientation
- overflow-block
- overflow-inline
- pointer
- prefers-color-scheme
- prefers-contrast
- prefers-reduced-motion
- resolution
- scripting
- video-dynamic-range
- width

Take a few minutes and explore this list. 

What did you see? 

Why so many features? 

## Using Media Queries

The basic syntax for a media query looks like this: 

```CSS
@media <media-query-list> {
  <stylesheet>
}
```

Here's an example: 

```CSS
@media print {
	/* These styles only apply to print */
  body {
    font-size: 10pt;
  }
}

@media screen {
	/* These styles only apply to screen */
  body {
    font-size: 13px;
  }
}

@media screen, print {
	/* These apply to both screen and print */
  body {
    line-height: 1.2;
  }
}

@media only screen and (min-width: 320px) and (max-width: 480px) and (resolution: 150dpi) {
	/* Applies to screen when the width is between 320px and 480px, and the resolution is 150dpi */
  body {
    line-height: 1.4;
  }
}

```

Why would you use this? Imagine you need to change your stylesheet when your app is viewed on a smaller screens. 

This is how you make your site "responsive". 

## Strategies

Usually most of your styles are good everywhere. Define them like you always do. 

Use media queries to define the situation where styles should change and those styles that changed. 

Here's a simple example: 

```CSS
body {
	color: tomato;
	background-color: lightgray;
	font-size: 16px;
}

@media print {
  body {
    color: black;
		background-color: white;
  }
}
```

The first rule sets the color to tomato with a background color of lightgray, and font-size of 16px. These styles apply everywhere. 

When the media is print the styles in the media query apply. These overwrite the color and background-color to black and white. 

Here is a more practical strategy that rearranges the grid when the screen is smaller. 

```CSS
/* Set up a grid */
.wrapper {
	display: grid;
	grid-template-areas: "h h h"
	                     "m m s"
											 "f f f";
	grid-template-columns: 1fr 1fr 1fr;
	gap: 2rem;
}

/* Assign elements to grid */
.header {
	grid-area: h;
}

.main {
	grid-area: m;
}

.side-bar {
	grid-area: s;
}

.footer {
	grid-area: f;
}

/* Add media query that applies when the screen is 1000px or smaller */
@media (max-width: 1000px) {
	.wrapper {
		grid-template-areas: "h h h"
		                     "s s s"
	                       "m m m"
											   "f f f";
	}
}
```

Code above shows .main and .side-bar side by side when the screen is larger than 1000px, it places the .side-bar above .main and makes both take up the full width when the screen is 1000px or smaller. 

### Mobile First vs Desktop first design

Mobile first is a design strategy where you would prioritize designing for a mobile environments. 

Desktop first is the strategy where you would prioritize for the desktop first. 

Today 54% of traffic is on mobile devices. Many applications migth benfit from a a good user experience and design on mobile. 

For many products it can be better to design for mobile first. 

Using Media Queries...

For responsive projects your goal would be to develop the design of your project so that it displays the way you intend on mobile or desktop first. 

Then add media queries to fix and improve display problems on other types of displays. 

Don't design for both at the same time! 

