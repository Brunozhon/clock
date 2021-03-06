# Clock

A real SVG analog clock. Tick, tock, tick, tock...

## Embed

To embed the clock, use a iframe.

```html
<iframe src="https://brunozhon.github.io/clock/" width="200" height="200"></iframe>
```

## Step-by-step clock

1. Write or copy/paste this starter code.
```html
<!DOCTYPE HTML>
<html>
  <head>
    <title>Hello, world!</title>
  </head>
  <body>
  </body>
</html>
```
2. Add a SVG element with two circles inside the `<body>` element.
```html
<svg viewBox="-100 -100 200 200">
  <circle
          cx="0"
          cy="0"
          r="90"
          fill="transparent"
          stroke="#f0f0c9"
          stroke-width="7"
          stroke-dasharray="0.2 0.8"
          stroke-dashoffset="0.1"
          pathLength="60"
  />
  <circle
          cx="0"
          cy="0"
          r="90"
          fill="transparent"
          stroke="#0f0e0e"
          stroke-width="7"
          stroke-dasharray="0.2 4.8"
          stroke-dashoffset="0.1"
          pathLength="60"
  />
</svg>
```
3. Add lines for the hour, minute, and second hands along with CSS.
```html
<line class="hand" x1="0" y1="0" x2="0" y2="-50" />
<line class="hand hand--thick" x1="0" y1="-12" x2="0" y2="-50" />

<line class="hand" x1="0" y1="0" x2="0" y2="-80" />
<line class="hand hand--thick" x1="0" y1="-12" x2="0" y2="-80" />

<line class="hand hand--second" x1="0" y1="12" x2="0" y2="-80" />
```
```css
.hand {
  stroke: #ffffff;
  stroke-width: 2;
  stroke-linecap: round;
}
.hand--thick {
  stroke-width: 7;
}
.hand--second {
  stroke: yellow;
}
```
4. Put the hands in groups for the JavaScript.
```html
<g id="hour_hand">
  <line class="hand" x1="0" y1="0" x2="0" y2="-50" />
  <line class="hand hand--thick" x1="0" y1="-12" x2="0" y2="-50" />
</g>

<g id="minute_hand">
  <line class="hand" x1="0" y1="0" x2="0" y2="-80" />
  <line class="hand hand--thick" x1="0" y1="-12" x2="0" y2="-80" />
</g>

<g id="second_hand">
  <line class="hand hand--second" x1="0" y1="12" x2="0" y2="-80" />
</g>
```
5. Add the scripts like this:
```js
const hoursElement = document.getElementById("hour_hand")
const minutesElement = document.getElementById("minute_hand")
const secondsElement = document.getElementById("second_hand")

const date = new Date()
  
const hour = date.getHours()
const minute = date.getMinutes()
const second = date.getSeconds()

hoursElement.setAttribute("transform", `rotate(${(360 / 12) * hour})`)
minutesElement.setAttribute("transform", `rotate(${(360 / 60) * minute})`)
secondsElement.setAttribute("transform", `rotate(${(360 / 60) * second})`)
```
6. (Optional) If you need finer control over the hands, use this code instead:
```js
const hour = date.getHours() + date.getMinutes() / 60
const minute = date.getMinutes() + date.getSeconds() / 60
const second = date.getSeconds() + date.getMilliseconds() / 1000
```
7.  Wrap the code from `const hour = date.getHours()` to `secondsElement.setAttribute(...)` in a function called `animate`.
```js
const hoursElement = document.getElementById("hour_hand")
const minutesElement = document.getElementById("minute_hand")
const secondsElement = document.getElementById("second_hand")

function animate() {
  const date = new Date()
  
  const hour = date.getHours() + date.getMinutes() / 60
  const minute = date.getMinutes() + date.getSeconds() / 60
  const second = date.getSeconds() + date.getMilliseconds() / 1000
  
  hoursElement.setAttribute("transform", `rotate(${(360 / 12) * hour})`)
  minutesElement.setAttribute("transform", `rotate(${(360 / 60) * minute})`)
  secondsElement.setAttribute("transform", `rotate(${(360 / 60) * second})`)
}
```
8. Request the animation frame for `animate`.
```js
const hoursElement = document.getElementById("hour_hand")
const minutesElement = document.getElementById("minute_hand")
const secondsElement = document.getElementById("second_hand")

function animate() {
  const date = new Date()
  
  const hour = date.getHours() + date.getMinutes() / 60
  const minute = date.getMinutes() + date.getSeconds() / 60
  const second = date.getSeconds() + date.getMilliseconds() / 1000
  
  hoursElement.setAttribute("transform", `rotate(${(360 / 12) * hour})`)
  minutesElement.setAttribute("transform", `rotate(${(360 / 60) * minute})`)
  secondsElement.setAttribute("transform", `rotate(${(360 / 60) * second})`)
  requestAnimationFrame(animate)
}

requestAnimationFrame(animate)
```
You're all done in 8 steps! Here's the finished code:
```html
<!DOCTYPE HTML>
<html>
  <head>
    <title>Hello, world!</title>
    <style>
      .hand {
        stroke: #ffffff;
        stroke-width: 2;
        stroke-linecap: round;
      }
      .hand--thick {
        stroke-width: 7;
      }
      .hand--second {
        stroke: yellow;
      }
    </style>
  </head>
  <body>
    <svg width="200" height="200" viewBox="-100 -100 200 200">
      <circle 
              cx="0"
              cy="0"
              r="90"
              fill="transparent"
              stroke="#f0f0c9"
              stroke-width="7"
              stroke-dasharray="0.2 0.8"
              stroke-dashoffset="0.1"
              pathLength="60"
      />
      <circle
              cx="0"
              cy="0"
              r="90"
              fill="transparent"
              stroke="#0f0e0e"
              stroke-width="7"
              stroke-dasharray="0.2 4.8"
              stroke-dashoffset="0.1"
              pathLength="60"
      />
      
      <g id="hour_hand">
        <line class="hand" x1="0" y1="0" x2="0" y2="-50" />
        <line class="hand hand--thick" x1="0" y1="-12" x2="0" y2="-50" />
      </g>
      
      <g id="minute_hand">
        <line class="hand" x1="0" y1="0" x2="0" y2="-80" />
        <line class="hand hand--thick" x1="0" y1="-12" x2="0" y2="-80" />
      </g>
      
      <g id="second_hand">
        <line class="hand hand--second" x1="0" y1="12" x2="0" y2="-80" />
      </g>
    </svg>
    <script>
      const hoursElement = document.getElementById("hour_hand")
      const minutesElement = document.getElementById("minute_hand")
      const secondsElement = document.getElementById("second_hand")
      
      function animate() {
        const date = new Date()
        
        const hour = date.getHours() + date.getMinutes() / 60
        const minute = date.getMinutes() + date.getSeconds() / 60
        const second = date.getSeconds() + date.getMilliseconds() / 1000
        
        hoursElement.setAttribute("transform", `rotate(${(360 / 12) * hour})`)
        minutesElement.setAttribute("transform", `rotate(${(360 / 60) * minute})`)
        secondsElement.setAttribute("transform", `rotate(${(360 / 60) * second})`)
        
        requestAnimationFrame(animate)
      }
      requestAnimationFrame(animate)
    </script>
  </body>
</html>
```
