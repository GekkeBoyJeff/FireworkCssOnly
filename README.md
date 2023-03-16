# FireworkCssOnly

## Assignement
The assignment is to make a firework animation with only CSS. The animations should be triggered by checkboxes. The animation should be responsive and work on mobile devices. It should be possible to add multiple fireworks at the same time. 

## Demo
[Firework show (gekkeboyjeff.github.io)](https://gekkeboyjeff.github.io/FireworkCssOnly/)

## Features
- [x] Responsive
- [x] Mobile friendly
- [x] Multiple fireworks at the same time
- [x] Animation triggered by checkboxes
- [x] Animation triggered by hover
- [ ] Animation triggered by focus

![](https://raw.githubusercontent.com/GekkeBoyJeff/FireworkCssOnly/main/assets/product.gif)

## Conclusion
I made less than I had hoped for. I took way to much time trying to figure out what and how I wanted to make it.  
I learned a lot about the :has property
I got stuck on trying to animate the first animation from the bottom properly. the other two divs do not start from the bottom for some reason.
I couldn't make the animations I practiced on work in the end so they will remain in this readme forever. (sadface)

I need to think less about what I want to make and just start. I think if I had made more time for the animations themselves I could have made much more.
including the motion path which I wanted to try but I did not have enough time for it sadly.

# weekly work

## Week 1 planning
- [x] uittekenen hoe ik het ontwerp wil maken
- [x] Een uitschuifbaar menu maken
- [x] Een werkende vuurpijl maken

This week it was my intention to make a basis for the assignment. Unfortunately, not everything worked out.

### Sketches:
I started drawing out my menu which came out like this
![](https://raw.githubusercontent.com/GekkeBoyJeff/FireworkCssOnly/main/assets/LayoutW1.png)

I moestly designed the UI with this sketch. It occurred to me that I should have a form with a number of fieldsets. As indicated above, the foldable menus are the field sets.

The basic HTML I was able to get out from my sketch for this week is as follows
![](https://raw.githubusercontent.com/GekkeBoyJeff/FireworkCssOnly/main/assets/HtmlW1.png)The input fields in the middle (of the image above) are for sliding the field sets in and out.

### Css
For the base I have not yet taken into account the final styling because I still want to determine that.
![](https://raw.githubusercontent.com/GekkeBoyJeff/FireworkCssOnly/main/assets/Css0W1.png)
![](https://raw.githubusercontent.com/GekkeBoyJeff/FireworkCssOnly/main/assets/Css1W1.png)
As shown above, you can press both labels to slide out the menus. The "buttons" in the menu on the left have not been further developed yet.

### Feedback week 1
During the feedback conversation it came up that I used the has selector perfectly to make this. Below you see an image of the css selector in which I place the menu at the location on the left.
![](https://raw.githubusercontent.com/GekkeBoyJeff/FireworkCssOnly/main/assets/Css2W1.png)

#### Takeaways
- Continue with your assignment. Speed it up a bit because you don't have flares and explosions yet. 
- I can eventually make something of a gallery of different firecrackers that become visible when I press another button. This can also be my process book at the same time.


## Start week 2
This week I'll continue with my takeaways from last week, the plan is to add the firecracker animation and add the explosion in multiple ways. I also have to add the textboxes on the bottom as shown in the layout sketch in week 1.

- [ ] Add a firecracker
- [ ] Add the animation to make it fly upwards
- [ ] Add the explosion
- [ ] Make the layout prettier
- [ ] Add a background
- [ ] Add layered backgrounds

### Lesson on custom properties

Custom properties are interesting for experimentation and architecture.

```CSS
/* Old custom properties */

button{
	color:teal;
	border-color:currentcolor;
}
button[type="submit"]{
	color:rebeccapurple
}
button[type="reset"]{
	color: saddlebrown;
}
```

The example above uses the colors already defined from css. That also works as a kind of variable.

```CSS
/* with recent custom properties */

button{
--button-color:teal;

	color:var(--button-color);
	border-color:var(--button-color);
}
button[type="submit"]{
	color:white
	background-color:var(--button-color);
}
button[type="reset"]{
	color: saddlebrown;
}
button:hover{
	--button-color: deeppink;
}
```

Above you can see that there are no variables defined in the root but rather in the components themselves. Sanne wanted to make it clear that it is also possible to update them within different components..

The fun fact about variables is that you can add a fallback to them if the color does not work

```CSS
button{
	background-color:(--button-color, red)
}

li{
	animation-delay:var(--delay, 0s)
}

li:nth-of-type(2){
	--delay:2s;
}
li:nth-of-type(3){
	--delay:.5s;
}
```
A nice use case for this is adding a fallback in advance. Every list item has a standard delay of zero seconds unless the delay variable has been set.

**Unitless custom properties**
'``Lea verou' has an article coverin this. You want to do this for changing the animation based on how long something takes.

[cust props - more with calc - start (codepen.io)](https://codepen.io/GekkeBoyJeff/pen/eYLZeaL)

### Responsiveness
Since the buttons on the bottom left were both placed in an absolute position there was not much I could do to make it responsive. 
- I could make a media query to set them at another location to make them 'responsive'  
I did try this out but I was not happy with the result. I wanted the buttons to make sense for being at a certain position.

So I thought of a different way in which I could place them in my HTML file to make them responsive without having to add media queries.

So instead of placing them directly in the form. I placed them in the fieldset where they belonged. Then I positioned them with position relative. to give them a bit more of default 'responsiveness' which I tweaked a bit to my liking.

However, I now had a button which said 'Menu left' 
![](https://raw.githubusercontent.com/GekkeBoyJeff/FireworkCssOnly/main/assets/w2MenuLeftButton.png)
which I did not like. I also wanted to change the text of the button when it was pressed but since I wasn't allowed to use javascript I had to think of a different way or option.

It took me a while to figure out how to change the text but I found out I could change the text of 'content' which resides in the before and after tag. So I made this work.

![](https://raw.githubusercontent.com/GekkeBoyJeff/FireworkCssOnly/main/assets/w2MenuLeftButtonAfter1.png)
![](https://raw.githubusercontent.com/GekkeBoyJeff/FireworkCssOnly/main/assets/w2MenuLeftButtonAfter2.png)

#### Positioning the left button
```CSS
/* Left side button */
/* Because it is relative, it is directly in the middle, hence top -23.7em */
body>form:first-of-type fieldset:first-of-type label:first-of-type {
    position: relative;
    order: 1;
    top: -23.7em;
    padding: 0;
    flex: unset;
    left: 18em;
    width: 11em;
    background-color: unset;
    color: transparent;
    text-align: right;
}

/* Resizes the label and allows you to click through it */
form:has(> fieldset:first-of-type > input:first-of-type:checked)>fieldset:first-of-type>label:first-of-type {
    pointer-events: none;
    height: 3.3em;
    background-color: #1b1b1b;
    z-index: -1;
    width: 9em;
    left: 15em;
}
```

##### Changing the button on click
```CSS
/* Move the after 'button' to the top left and set the text to Firework */
body>form:first-of-type fieldset:first-of-type label:first-of-type::before {
    content: 'Firework';
    background-color: red;
    color: #1b1b1b;
    font-family: system-ui;
    font-weight: 700;
    padding: 1em;
    position: absolute;
    border-radius: 0 .5em .5em 0;
    left: 0em;
    pointer-events: all;
    transform: translateX(6em);
    transition: 1s;
    z-index: -6;
}

/* location and size of the expand button changes. This button is the styling for the expand button */
/* Also changes the text to an X */
body>form:has(> fieldset:first-of-type > input:first-of-type:checked)>fieldset:first-of-type label:first-of-type::before {
    content: 'X';
    color: red;
    background-color: #1b1b1b;
    transform: translateX(3em);
    transition: .5s;
    width: 8em;
    left: -4em;
}
```

#### Positioning the bottom menu and button
The menu on the bottom of the screen was done in a similar way, except I did not need to change the ::after selector. I could simply rotate it.

```CSS
/* hide the menu down by default */
form:has(>fieldset:nth-of-type(2)>input:first-of-type:checked)>fieldset:nth-of-type(2) {
    transform: translateY(0em);
} 

/* Change text in the label by placing the after */
form>fieldset:nth-of-type(2)>label:first-of-type::after {
    content: '^';
    color: #1b1b1b;
    font-weight: bold;
    font-size: 3em;
    position: relative;
    top: .2em;
    transition: .5s;
    order: -1;
    margin-left: .2em;
}
```

However, getting the arrow at the bottom to look well was a big tougher. Since I used another method for changin the button on the left I had to think of a way to make this look good aswell.
The difference between the top-left button and the one on the bottom is that the one on the top-left is hiding it's button and actually shows it's ::before element which is also clickable. I made the button itself click-through with pointer-events:none;

The button at the bottom simply has the same text-color as the background and has the bottom positioned with left:-.55em; to put it over the text. This however was not ideal since on mobile it would look like so:
![](https://raw.githubusercontent.com/GekkeBoyJeff/FireworkCssOnly/main/assets/w3menuBottomButon.png)

It took me a while to figure out that it was better if I either made a ::before element of it or used order:-1; I did not know you could change the order of an element with a minus value. This was good to know.

After adding the order and removing the left property I added a flip once it has been pressed. it was the easiest way to animate this button. I did rotate the text in the after element at first but that didnt rotate through the center but rather through the right and it did not look pretty. so I changed it to a minus scale to rather flip it. which I think is better for a menu which goes up and down.

```CSS
/* Animation for flipping the arrow */
form:has(>fieldset:nth-of-type(2)>input:first-of-type:checked)>fieldset:nth-of-type(2)>label:first-of-type::after {
    top: -0.1em;
    transform-origin: .28em;
    transform: scaleY(-1);
}
```

After adding the slider buttons I added functionality for the other animation buttons. 

```CSS
form:has(> fieldset:first-of-type > input:nth-of-type(3):checked)>fieldset:nth-of-type(4) {
    background-color: brown;
    transform: translateY(-100%);
}

form>fieldset:nth-of-type(n+4) {
    position: absolute;
    width: 100vw;
    top: 100%;
}
```

the first selector is for a fieldset once the checkbox has been checked. I repeated multiple times for each animation.

### Animation
So I started working on my first animation. I want them to play once the checkbox has been pressed in the left menu.

A few days ago Sanne gave us a lesson about animation. I decided that I would use that animation for a base.
The HTML consisted out of:

```HTML
<div>
  <div></div>
  <div></div>
</div>
```

```CSS
body{
height:100vh;
display:grid;
place-content:center;
}

body div {
  width:5em;
  aspect-ratio:1;
  background-color:green;
  
  animation-name:omhoog;
  animation-duration:2s;
  animation-fill-mode:forwards;
  animation-play-state:paused;
  position:relative;
} 

@keyframes omhoog{
  0%{
    transform:translateY(0);
  }
  50%, 100%{
    transform:translateY(-200%);
  }
}

div div  {
  position:absolute;
  inset:0;
  background-color:red;
}

div div:nth-of-type(1){
  animation-name:links;
  animation-duration:1s;
  animation-delay:1s;
/*   animation-iteration-count:infinite; */
  animation-play-state:paused;
  animation-fill-mode:forwards;
}

div div:nth-of-type(2){
  animation-name:rechts;
  animation-duration:1s;
  animation-delay:1s;
/*   animation-iteration-count:infinite; */
    animation-fill-mode:forwards;
  animation-play-state:paused;
}

@keyframes links{
0%{
	transform:translateX(0%);
}
100%{
	transform:translateX(-200%);
  }
}
@keyframes rechts{
0%{
	transform:translateX(0%);
}
100%{
transform:translateX(200%);
  }
}
  
body:hover div{
  animation-play-state: running;
}
```

The code above shows a single red block which splits into three blocks.
![](https://raw.githubusercontent.com/GekkeBoyJeff/FireworkCssOnly/main/assets/w2SingleBlock.png) ![](https://raw.githubusercontent.com/GekkeBoyJeff/FireworkCssOnly/main/assets/w2TrippleBlock.png)

So I tried to chain animations by placing a div around them which starts all the animations on hover. This however did not work fluently and felt wrong. After trying to make it work for a while a classmate told me I could simply place the other animation in the same css property and that I could add a delay for it aswell. 

So all I had to do was add the new animation
```CSS
@keyframes dissapear{
  0%{
    opacity:1;
  }100%{
    opacity:0;
  }
}

body div {
  width:5em;
  aspect-ratio:1;
  background-color:green;
  
  animation-name:omhoog, dissapear;
  animation-duration:2s, 1s;
  animation-delay:0s, 1.5s;
  animation-fill-mode:forwards;
  animation-play-state:paused;
  position:relative;
} 
```

As shown above, the animation-name has 2 properties now. the same goes for duration and delay so each animation has its sperate duration and starts at a different time.

There was a bug in which the second animation starts without a delay once it has animated once.  I was not able to fix this sadly
[Css chaining animation (codepen.io)](https://codepen.io/GekkeBoyJeff/pen/bGxNbBq)


## Week 3
This week was really stressfull since I haven't added any animations yet and it had to be delivered on this day.

So I started by adding three divs to the third fieldset.
```HTML
<fieldset>
	<div></div>
	<div></div>
	<div></div>
</fieldset>
```

After that I added fake firework.
```CSS
form:has(> fieldset:first-of-type > input:nth-of-type(2):checked)>fieldset:nth-of-type(3)>div:first-of-type {
    position: absolute;
    top: 50%;
    left: 50%;
	aspect-ratio: 1;
    transform: translate(-50%, -50%);
    background: radial-gradient(circle, #ff0 .2em, #0000 0) 50% 00%,
        radial-gradient(circle, #ff0 .3em, #0000 0) 00% 25%,
        radial-gradient(circle, #ff0 .5em, #0000 0) 15% 45%,
        radial-gradient(circle, #ff0 .2em, #0000 0) 95% 25%;
    background-size: 0.2em 0.2em;
    background-repeat: no-repeat;
    animation: firework 2s infinite;
    border-radius: .5em;
}
```

The background property has a couple of different radial gradients which are the 'sparks' which come off the explosions. the value next to them are their positions within the div.

In the animation I decided to change the width of the div itself. by doing this the radial gradients are able to hold their position within the div.

```CSS
@keyframes firework {
    0% {
        transform: translateY(60vh);
        opacity: 0;
    }
  
    50% {
        width: 0.3em;
        opacity: 1;
    }
  
    100% {
        width: 50dvw;
        opacity: 0;
    }
}
```

![](https://raw.githubusercontent.com/GekkeBoyJeff/FireworkCssOnly/main/assets/w3Begin1stAnimation.png)

The result was quite pleasing. After that I added a few more radial gradients.
```CSS
    background: radial-gradient(circle, #ff0 .2em, #0000 0) 50% 00%,
        radial-gradient(circle, #ff0 .3em, #0000 0) 00% 25%,
        radial-gradient(circle, #ff0 .5em, #0000 0) 15% 45%,
        radial-gradient(circle, #ff0 .2em, #0000 0) 95% 45%,
        radial-gradient(circle, #ff0 .3em, #0000 0) 5% 70%,
        radial-gradient(circle, #ff0 .5em, #0000 0) 65% 85%,
        radial-gradient(circle, #ff0 .2em, #0000 0) 25% 85%,
        radial-gradient(circle, #ff0 .3em, #0000 0) 85% 65%,
        radial-gradient(circle, #ff0 .5em, #0000 0) 75% 25%,
        radial-gradient(circle, #ff0 .2em, #0000 0) 90% 15%;
```

Now to make the effect bigger and more spectecular I tried adding a before and after element to the selector.

that was quite easy to do since I only had to copy and paste the current selector and add the before and after. I did however struggle with getting it to work but I completely forgot to add content to it...

```CSS
form:has(> fieldset:first-of-type > input:nth-of-type(2):checked)>fieldset:nth-of-type(3)>div:first-of-type,
form:has(> fieldset:first-of-type > input:nth-of-type(2):checked)>fieldset:nth-of-type(3)>div:first-of-type::before,
form:has(> fieldset:first-of-type > input:nth-of-type(2):checked)>fieldset:nth-of-type(3)>div:first-of-type::after {
    content: '';
    }
```

And to make them a bit different I added another transform to the before and after element
```CSS
form:has(> fieldset:first-of-type > input:nth-of-type(2):checked)>fieldset:nth-of-type(3)>div::before {
    transform: translate(-50%, -50%) rotate(25deg) !important;
}
  
form:has(> fieldset:first-of-type > input:nth-of-type(2):checked)>fieldset:nth-of-type(3)>div::after {
    transform: translate(-50%, -50%) rotate(-37deg) !important;
}
```

I also had to add !important because I couldn't make the css more specific.

After that I added custom properties so that I could change one of the properties of the hsl color.

I gave the div a var called colorDeg which is different for the before and after effects. Because of this I was able to easily manipulate the colors of the before, after and other animations aswell

```CSS
    --colorDeg: 60deg;
    --color: hsl(var(--colorDeg) 100% 50%);
```

```CSS
form:has(> fieldset:first-of-type > input:nth-of-type(2):checked)>fieldset:nth-of-type(3)>div::before {
    transform: translate(-50%, -50%) rotate(45deg) !important;
    --colorDeg: 30deg;
}

form:has(> fieldset:first-of-type > input:nth-of-type(2):checked)>fieldset:nth-of-type(3)>div::after {
    transform: translate(-50%, -50%) rotate(-27deg) !important;
    --colorDeg: 10deg;
}
```

I also changed the position of the other animations
```CSS
form:has(> fieldset:first-of-type > input:nth-of-type(2):checked)>fieldset:nth-of-type(3)>div:nth-of-type(2),
form:has(> fieldset:first-of-type > input:nth-of-type(2):checked)>fieldset:nth-of-type(3)>div:nth-of-type(2)::before,
form:has(> fieldset:first-of-type > input:nth-of-type(2):checked)>fieldset:nth-of-type(3)>div:nth-of-type(2)::after {
    left: 20%;
    bottom: 20%;
    animation-delay: .5s;
    --colorDeg: 80deg;
    --color: hsl(var(
    --colorDeg) 100% 50%);
}
form:has(> fieldset:first-of-type > input:nth-of-type(2):checked)>fieldset:nth-of-type(3)>div:nth-of-type(3),
form:has(> fieldset:first-of-type > input:nth-of-type(2):checked)>fieldset:nth-of-type(3)>div:nth-of-type(3)::before,
form:has(> fieldset:first-of-type > input:nth-of-type(2):checked)>fieldset:nth-of-type(3)>div:nth-of-type(3)::after {
    left: 80%;
    top: 40%;
    animation-delay: 1.2s;
    --colorDeg: 20deg;
    --color: hsl(var(
    --colorDeg) 100% 50%);
    transform: translate(-50%, -50%) rotate(45deg);
}

```

I re-colored the menu, gave the background a color to simulate night and day. This depends on if you've got a black theme or white theme.

I also added a sun and moon.

```CSS
@media (prefers-color-scheme: light){
    body::before{
        color:black;
        content:"it's a bit light in here, isn't it?, try the dark mode";
        position: absolute;
        z-index: 0;
        width: 100%;
        text-align: center;
        top: 1em;
    }
    body:after{
        content:'';
        position: absolute;
        top: -1em;
        right: -4em;
        background:yellow;
        box-shadow: 0 0 2em yellow;
        width: 12em;
        aspect-ratio:1;
        border-radius: 50%;
        z-index: -1;
    }
}
```

```CSS
body:after{
    content:'';
    position: absolute;
    top: -1em;
    right: -4em;
    background: #c9c9c9;
    box-shadow: 0 0 2em #616161;
    width: 12em;
    aspect-ratio:1;
    border-radius: 50%;
    z-index: -1;
}
```

## Animation 2
While trying to make a motion path I wanted to animate it. I generated a svg with text on [this website)](https://danmarshall.github.io/google-font-to-svg-path/).  However while trying to animate it, the animation went wrong. 

![](https://raw.githubusercontent.com/GekkeBoyJeff/FireworkCssOnly/main/assets/offsetPath1.png)

```CSS
form:has(> fieldset:first-of-type > input:nth-of-type(3):checked)>fieldset:nth-of-type(4) div {
    offset-path:path("M 187.1 74 L 177.2 74 L 160.8 24.4 L 169.1 21.5 L 182.5 63.8 L 194.7 25.7 L 204.4 25.7 L 216.3 63.8 L 229.6 21.5 L 237.6 24.4 L 221.1 74 L 211.2 74 L 199.2 35.3 L 187.1 74 Z M 388.9 69 L 382.7 75 L 355.8 47.3 L 355.8 74 L 346.8 74 L 346.8 0 L 355.8 0 L 355.8 42.3 L 379.3 21 L 384.5 26.7 L 364.4 44.5 L 388.9 69 Z M 9.5 74 L 0 74 L 0 4 L 41.5 4 L 41.5 12.2 L 9.5 12.2 L 9.5 33.6 L 36.2 33.6 L 36.2 41.4 L 9.5 41.4 L 9.5 74 Z M 393.4 69.8 L 397.2 62.3 A 18.557 18.557 0 0 0 400.344 64.426 Q 401.898 65.27 403.75 65.95 A 24.073 24.073 0 0 0 411.361 67.387 A 27.464 27.464 0 0 0 412.2 67.4 Q 417.592 67.4 420.435 65.685 A 7.738 7.738 0 0 0 420.65 65.55 Q 423.5 63.7 423.5 60.8 A 7.123 7.123 0 0 0 423.186 58.653 A 6.212 6.212 0 0 0 422.45 57.1 A 6.384 6.384 0 0 0 421.521 56.006 Q 420.507 55.034 418.834 54.081 A 22.3 22.3 0 0 0 418.6 53.95 A 28.462 28.462 0 0 0 416.606 52.957 Q 414.49 51.995 411.501 50.946 A 103.602 103.602 0 0 0 410.5 50.6 A 46.616 46.616 0 0 1 406.102 48.857 Q 403.988 47.883 402.312 46.795 A 19.335 19.335 0 0 1 399.55 44.65 A 11.324 11.324 0 0 1 396.256 38.654 A 16.794 16.794 0 0 1 395.9 35.1 Q 395.9 29.1 401.15 24.95 Q 405.554 21.469 412.808 20.908 A 37.527 37.527 0 0 1 415.7 20.8 A 40.794 40.794 0 0 1 420.146 21.031 Q 422.454 21.284 424.47 21.815 A 25.234 25.234 0 0 1 424.6 21.85 Q 428.5 22.9 431.6 24.5 L 429.1 31.9 Q 426.4 30.3 422.95 29.3 A 25.024 25.024 0 0 0 418.467 28.453 A 31.837 31.837 0 0 0 415.3 28.3 A 20.632 20.632 0 0 0 412.363 28.495 Q 409.277 28.94 407.4 30.4 A 9.322 9.322 0 0 0 406.042 31.673 Q 405.34 32.492 405.005 33.365 A 4.529 4.529 0 0 0 404.7 35 A 4.921 4.921 0 0 0 406.195 38.552 A 7.082 7.082 0 0 0 406.8 39.1 A 9.88 9.88 0 0 0 408.1 39.969 Q 410.373 41.271 414.798 42.734 A 84.459 84.459 0 0 0 415 42.8 A 67.753 67.753 0 0 1 420.062 44.698 Q 425.989 47.217 428.8 50.1 Q 432.7 54.1 432.7 60.1 Q 432.7 66.848 427.449 70.855 A 16.618 16.618 0 0 1 427.05 71.15 Q 422.31 74.547 414.862 75.095 A 40.423 40.423 0 0 1 411.9 75.2 Q 406 75.2 401.25 73.7 A 30.883 30.883 0 0 1 397.41 72.215 Q 395.429 71.284 393.848 70.136 A 18.229 18.229 0 0 1 393.4 69.8 Z M 154 51.7 L 117.6 51.7 A 24.088 24.088 0 0 0 118.739 56.725 Q 120.075 60.538 122.7 63.1 Q 126.9 67.2 133.8 67.2 Q 138.3 67.2 141.9 66.25 Q 145.5 65.3 148.8 63.8 L 150.9 71.5 A 40.77 40.77 0 0 1 146.565 73.126 A 51.863 51.863 0 0 1 142.8 74.15 A 38.914 38.914 0 0 1 137.708 74.969 A 52.025 52.025 0 0 1 132.7 75.2 A 28.318 28.318 0 0 1 124.954 74.195 A 21.108 21.108 0 0 1 114.95 68.05 A 23.521 23.521 0 0 1 109.745 58.51 Q 108.4 53.845 108.4 48 A 35.359 35.359 0 0 1 109.233 40.178 A 28.84 28.84 0 0 1 111.35 34.05 A 24.642 24.642 0 0 1 116.366 26.968 A 22.887 22.887 0 0 1 119.6 24.35 A 21.048 21.048 0 0 1 129.859 20.878 A 26.205 26.205 0 0 1 131.9 20.8 Q 139.4 20.8 144.35 24.05 Q 149.3 27.3 151.8 32.8 A 28.185 28.185 0 0 1 154.226 42.664 A 33.434 33.434 0 0 1 154.3 44.9 A 75.204 75.204 0 0 1 154.009 51.597 A 69.426 69.426 0 0 1 154 51.7 Z M 84 74 L 75 74 L 75 22 L 83.7 22 L 83.7 33.3 Q 85 30 87.2 27.15 Q 89.4 24.3 92.7 22.55 A 14.817 14.817 0 0 1 97.38 21.026 A 19.459 19.459 0 0 1 100.4 20.8 Q 101.9 20.8 103.4 20.95 A 18.972 18.972 0 0 1 104.455 21.084 Q 104.955 21.162 105.382 21.262 A 8.817 8.817 0 0 1 105.9 21.4 L 103.2 30.7 A 9.763 9.763 0 0 0 101.055 30.088 Q 99.959 29.9 98.7 29.9 A 12.958 12.958 0 0 0 92.07 31.746 A 15.609 15.609 0 0 0 91.65 32 Q 88.322 34.086 86.178 38.442 A 22.927 22.927 0 0 0 86.15 38.5 Q 84.387 42.107 84.07 47.328 A 39.09 39.09 0 0 0 84 49.7 L 84 74 Z M 315.9 74 L 306.9 74 L 306.9 22 L 315.6 22 L 315.6 33.3 Q 316.9 30 319.1 27.15 Q 321.3 24.3 324.6 22.55 A 14.817 14.817 0 0 1 329.28 21.026 A 19.459 19.459 0 0 1 332.3 20.8 Q 333.8 20.8 335.3 20.95 A 18.972 18.972 0 0 1 336.355 21.084 Q 336.855 21.162 337.282 21.262 A 8.817 8.817 0 0 1 337.8 21.4 L 335.1 30.7 A 9.763 9.763 0 0 0 332.955 30.088 Q 331.859 29.9 330.6 29.9 A 12.958 12.958 0 0 0 323.97 31.746 A 15.609 15.609 0 0 0 323.55 32 Q 320.222 34.086 318.078 38.442 A 22.927 22.927 0 0 0 318.05 38.5 Q 316.287 42.107 315.97 47.328 A 39.09 39.09 0 0 0 315.9 49.7 L 315.9 74 Z M 255.7 71.75 A 24.559 24.559 0 0 0 260.298 73.84 Q 264.353 75.2 269 75.2 Q 276.4 75.2 282.25 71.8 Q 288.1 68.4 291.5 62.25 A 26.255 26.255 0 0 0 294.153 55.109 A 34.184 34.184 0 0 0 294.9 47.8 A 34.542 34.542 0 0 0 294.415 41.891 A 25.795 25.795 0 0 0 291.45 33.45 Q 288 27.4 282.15 24.1 A 24.848 24.848 0 0 0 277.509 22.073 A 27.738 27.738 0 0 0 269 20.8 A 31.325 31.325 0 0 0 267.42 20.839 A 26.169 26.169 0 0 0 255.8 24.1 Q 249.9 27.4 246.5 33.5 A 26.023 26.023 0 0 0 243.751 41.09 A 35.006 35.006 0 0 0 243.1 48 A 34.82 34.82 0 0 0 243.365 52.354 A 27.451 27.451 0 0 0 246.45 62.15 Q 249.8 68.3 255.7 71.75 Z M 59 74 L 50 74 L 50 22 L 59 22 L 59 74 Z M 269 67.2 Q 276.9 67.2 281.3 61.85 A 18.802 18.802 0 0 0 285.119 53.76 A 27.105 27.105 0 0 0 285.7 48 Q 285.7 42.8 283.5 38.45 A 19.198 19.198 0 0 0 279.328 32.881 A 18.17 18.17 0 0 0 277.55 31.45 Q 273.8 28.8 269 28.8 A 19.249 19.249 0 0 0 263.774 29.472 A 14.037 14.037 0 0 0 256.7 34 A 17.878 17.878 0 0 0 253.026 41.374 Q 252.3 44.306 252.3 47.8 Q 252.3 53 254.5 57.45 A 19.437 19.437 0 0 0 258.03 62.49 A 17.627 17.627 0 0 0 260.45 64.55 Q 264.2 67.2 269 67.2 Z M 117.5 44.4 L 146 44.4 A 24.355 24.355 0 0 0 145.596 39.815 Q 145.1 37.231 143.996 35.207 A 12.422 12.422 0 0 0 142.2 32.7 A 12.488 12.488 0 0 0 135.239 28.924 A 18.395 18.395 0 0 0 131.7 28.6 A 13.58 13.58 0 0 0 126.588 29.535 A 12.524 12.524 0 0 0 122.1 32.65 Q 118.3 36.7 117.5 44.4 Z M 50.137 11.288 A 5.973 5.973 0 0 0 54.5 13.1 A 8.175 8.175 0 0 0 55.996 12.969 A 5.647 5.647 0 0 0 59.1 11.35 Q 60.8 9.6 60.8 6.8 A 7.26 7.26 0 0 0 60.8 6.719 A 6.06 6.06 0 0 0 58.95 2.35 A 7.395 7.395 0 0 0 58.892 2.293 A 6.059 6.059 0 0 0 54.5 0.5 A 8.264 8.264 0 0 0 52.844 0.658 A 5.661 5.661 0 0 0 49.9 2.2 A 5.588 5.588 0 0 0 48.429 4.832 A 7.987 7.987 0 0 0 48.2 6.8 A 5.992 5.992 0 0 0 48.692 9.219 A 6.643 6.643 0 0 0 50.05 11.2 A 7.466 7.466 0 0 0 50.137 11.288 Z");
    animation: move 10000ms infinite alternate ease-in-out;
    width: 2em;
    height: 2em;
    background: cyan;
}
@keyframes move {
    0% {
    offset-distance: 0%;
    }
    100% {
    offset-distance: 100%;
    }
}
```

I only added the path but it went all over the place. not following the actual words.

So I decided to do this per letter.
I changed the path to the following code for the first letter; F.

```svg

M 9.5 70 L 0 70 L 0 0 L 41.5 0 L 41.5 8.2 L 9.5 8.2 L 9.5 29.6 L 36.2 29.6 L 36.2 37.4 L 9.5 37.4 L 9.5 70 Z
```

Now it was finally using the correct path for the letter.

I adjusted the animation speed so that it would look like there was a path.
```CSS
form:has(> fieldset:first-of-type > input:nth-of-type(3):checked)>fieldset:nth-of-type(4) div div {
    animation: move 200ms infinite cubic-bezier(0.32, 0.28, 0.6, 0.71);
}
```

So the css path worked. However, it was still not readable so I had to adjust the height and width of the letters.

Since the animations move I can't screenshot it.

I did however add a reduced motion for the animations.
```CSS
@media (prefers-reduced-motion) {
    form:has(> fieldset:first-of-type > input:nth-of-type(3):checked)>fieldset:nth-of-type(4) div div{
        animation:move 2000ms infinite cubic-bezier(0.32, 0.28, 0.6, 0.71);
    }
}
```

