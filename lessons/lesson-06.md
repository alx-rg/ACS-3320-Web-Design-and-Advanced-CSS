# FEW 2.2 - Advanced CSS - Frameworks

## Lesson Video

Follow this lesson lecture in video form: 

https://youtube.com/playlist?list=PLoN_ejT35AEhF_M9vBuZgW0E4PiDb19oX

Watch Lesson 06 1-3

## Review

Imagine you need to design a dashboard page for a new product. This page is divided into a grid. Below is an image showing what the final page might look like. 

Grid Challenge: 

![grid challenge](images/grid-challenge.png)

Your goal is to recreate the image above with the markup below. Imagine this as a coding interview. 

Follow these steps: 

- Think about the problem and formulate at least one question for the interviewer. Your question should help clarify the problem and focus the expectation. 
- Outline your solution with comments. Think of this as Pseudo coding your solution! Review your pseudo code with the interviewer before coding! 
- Code your solution. 

```HTML
<!DOCTYPE html>
<html>
<head>
  <title>Dashboard</title>
  <style>
    
  </style>
</head>
<body>
  <div class="dashboard">
    <h1 class="title">Dashboard</h1>
    <div class="monster grid-cell">Monster</div>
    <div class="welcome grid-cell">
      <h2>Welcome</h2>
      <p>Some text... </p>
    </div>
    <div class="parents grid-cell">
      <h2>Parents</h2>
      <p>Some text... </p>
    </div>
    <div class="customize grid-cell">
      <h2>Customize</h2>
    </div>
    <div class="level-up grid-cell">
      <h2>Level Up</h2>
    </div>
    <div class="play grid-cell">
      <h2>Play</h2>
    </div>
  </div>
  
</body>
</html>
```

## Why you should know this?

A frontend developer should have an understanding of CSS frameworks. There is a lot to choose from they all have their pros and cons you should be able to get in and use any of these. 

## Learning Objectives 

1. Use CSS Frameworks
1. Evaluate CSS frameworks
1. Use CSS Custom properties

## What is a CSS Framework?

It could be a lot of things. Here a few popular CSS frameworks, you have used one or more of these:

- https://getbootstrap.com
- https://get.foundation
- https://bulma.io
- https://tailwindcss.com
- https://getuikit.com
- https://milligram.io
- https://purecss.io
- http://tachyons.io
- https://materializecss.com

Read up on these 9 CSS Frameworks here: https://athemes.com/collections/best-css-frameworks/

## Use the Framework

Each framework has its systems and paradigms. For the most part, they will work in this way: 

- You will link to a stylesheet you may also have the option to include a JS file. 
- Linking to the stylesheet will add a set of default styles that cover the common tags like:
 - Base font and typography
 - Headings
 - Links
 - Lists 
 - Tables 
 - form elements

The framework will offer more styles and custom elements that are created by using a combination of markup/HTML and class names. 

- Navbars
- buttons
- cards
- other features...

## Making your Framework

Study the frameworks above. Look at what they offer. You will make your framework! 

## After Class

There is two assignment for this week. 

Assignment 1 - Create a version of the CSS Zen Garden page using a CSS Framework. You can choose your favorite framework, it's up to you. With this assignment you are allowed to make any changes you like to zen garden HTML markup. 

Study the way the framework operates. Ask yourself these questions:

- What tags does it style? No need for a class name? 
- What markup is required? Sometimes to get something to work you need to combine certain tags and may have to include a class name. 
- How are class names used? 

Assignment 2 - 

Your goal is to create your CSS Framework. This will be a stylesheet that has all of the base styles that you might use in any project. 

You can emulate the features in the frameworks above. Look at the ideas these contain, implement them in your framework with your ideas. 

Get started by downloading the starter code:

https://github.com/Make-School-Labs/css-framework-starter). 

Copy this repo above. It contains a single HTML file. You will add a stylesheet that styles the contents of this file. 

The HTML file contains a range of typical elements that you will see on any website. The stylesheet you create should style these things so they look better than the default styles! 

What's in the markup? 

- Type - This inlcudes: 
	- Headings
	- paragraphs
	- links
- Buttons
- Forms - This inlcudes: 
	- Forms
	- Inputs
	- Check Boxes
- Colors - Color swatches showing the colors used by your framework
- Nav Bar

Your job is to create a default stylesheet that you could add to any project that will make it look better than the default HTML styles.

## Additional Resources

- [9 CSS Frameworks](https://athemes.com/collections/best-css-frameworks/)
- [Beginners Guide to CSS Frameworks](https://blog.zipboard.co/a-beginners-guide-to-css-front-end-frameworks-8045a499456b)

