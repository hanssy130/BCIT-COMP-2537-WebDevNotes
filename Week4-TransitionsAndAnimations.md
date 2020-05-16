# Week4 — Transitions and Animation
**Transitions**
* Allows you to change property values smoothly, over a given duration

**Animations**
* Allows animation of HTML elements without using JavaScript or Flash!

## 1) Transitions
> Process or change over a span of time.

### Syntax — Examples
```
transition: property duration timing-function delay;

transition-property: property:
transition-duration: duration;
transition-timing-function: timing-function;
transition-delay: delay;
```
* Property can be the width
* Duration = how long
* Timing-function = how should it change? should it accelerate?
* Delay = how long until transition starts?

### Events that trigger a transition
Examples include:
* Giving/removing focus from element a web form element
* Entering valid/invalid data into web form
* Hovering over web link/moving mouse pointer away

### Demo
```
transition: all 3s
```
all: any non-specified changes will change instantaenously

```
shorthand:
transition: background-color 3s, width 2s;

longhand:
transition-property: background-color, width;
transition-duration: 3s, 2s;
```

### Transition Timing
Acceptable values:
* ease (default) - start slow, speed up, change very slowly at end
* linear - constant rate of change
* ease-in - start slow, speed at end
* ease-out - start fast, slow down at end 
* ease-in-out - start slower than ease, speed up and slow down towards end (sine graph)
* cubic-bezier

## 2) Animations
> Move an object or a div

### Animation: Keyframes
Keyframes establish the behavior of an animation over time

|Required Properties|Definition|
|---|---|
|animation-duration| Specifies how many seconds/milliseconds to complete|
|animation-name|specifies name of keyframe you want to bind to selector|

|Optional Properties|Definition|
|---|---|
|animation-timing-function|speecurve of animation (ease, ease-in...)|
|animation-delay|how long until start|
|animation-iteration-count|how many times?|
|animation-direction|should it play in reverse on alternate cycles?|
|animation-fill-mode|what values are applied by animation outside the time it is executing|
|animation-play-state|is animation playing or paused?|

### Syntax
```
@keyframes name-of-animation {
  from {some-css-properties}
  to {some-css-properties}
}

#box {
  animation-name: yeet
  animation-duration: 5ms
}
```

```
@keyframes moveleft {
  from {left:0px;
  to {left: 400xp;
}
#some_image {
  animation-name: moveleft;
  animation-duration: 4s;
}
```

### Complex Example
Use percentages.
```
@keyframes example {
  0% {background-color: red;}
  25% {background-color: yellow;}
  50% {backgorund-color: blue;}
  100% {background-color: green;}
}
