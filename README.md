# Simple jQuery Slider

Simply slider based on jQuery. 

## Features

* Easy to install;
* Multiple sliders support;
* Automatic sliding, see settings;
* As small as 2kb.

## Settings

### HTML

Сreate HTML of the slider. You can add multiple sliders on a single page as well.

```html
<div class="slider">
 <ul>
  <li><img src="i/1.jpg" alt=""></li>
  <li><img src="i/2.jpg" alt=""></li>
  <li><img src="i/3.jpg" alt=""></li>
  <li><img src="i/4.jpg" alt=""></li>
  <li><img src="i/5.jpg" alt=""></li>
  </ul>
</div>
```

### CSS

Add this CSS:

```css
<style type="text/css">
 .slider {
 z-index: 9;
 width: 700px;
 height: 290px;
 overflow: hidden;
 margin: 0 0 7px;
 position: relative;
 }
 .slider ul,
 .slider li {
 padding: 0;
 margin: 0;
 list-style-type: none;
 }
 .slider ul {
 width: 9999px; 
 }
 .slider ul li {
 list-style-type: none;
 float: left;
 width: 700px;
 height: 290px;
 }
 .slider .nav {
 position: absolute;
 left: 15px;
 bottom: 12px; 
 }
 .slider .nav span {
 opacity: 0.9;
 background: #fff;
 margin: 0 8px 0 0;
 width: 16px;
 height: 16px;
 border-radius: 8px;
 cursor: pointer;
 overflow: hidden;
 display: block;
 float: left;
 box-shadow: 0 1px 2px #000;
 }
 .slider .nav span.on {
 background: #2e9419;
 }
</style>
```

### JavaScript

All you need to make your slider work is to finish by adding this JS-code. See comments to understand what's going on:

```js
<script type="text/javascript">
 $(document).ready(function() {
 $(".slider").each(function() {

 var repeats = 5, // number of automatic slides
 interval = 1, // interval, seconds
 repeat = true, // turn on automatic sliding (true/false)
 slider = $(this),
 repeatCount = 0,
 elements = $(slider).find("li").length;

 $(slider)
 .append("<div class='nav'></div>")
 .find("li").each(function() {
 $(slider).find(".nav").append("<span data-slide='"+$(this).index()+"'></span>");
 $(this).attr("data-slide", $(this).index());
 })
 .end()
 .find("span").first().addClass("on");

 // add timeout

 if (repeat) {
 repeat = setInterval(function() {
 if (repeatCount >= repeats - 1) {
 window.clearInterval(repeat);
 }

 var index = $(slider).find('.on').data("slide"),
 nextIndex = index + 1 < elements ? index + 1 : 0;

 sliderJS(nextIndex, slider);

 repeatCount += 1;
 }, interval * 1000);
 }

 });
 });

function sliderJS(index, slider) { // slide
 var ul = $(slider).find("ul"),
 bl = $(slider).find("li[data-slide=" + index + "]"),
 step = $(bl).width();

 $(slider)
 .find("span").removeClass("on")
 .end()
 .find("span[data-slide=" + index + "]").addClass("on");

 $(ul).animate({
 marginLeft: "-" + step * index
 }, 500);
}

$(document).on("click", ".slider .nav span", function(e) { // slider click navigate
 e.preventDefault();
 var slider = $(this).closest(".slider"),
 index = $(this).data("slide");

 sliderJS(index, slider);
});
</script>
```

### Settings

As you can see is JS above, all the settings are stored in this part:

```js
var repeats = 5, // number of automatic slides
 interval = 1, // interval, seconds
 repeat = true, // turn on automatic sliding (true/false)
 slider = $(this),
 repeatCount = 0,
 elements = $(slider).find("li").length;
 ```
## Demo

Working example can be [found here](http://dedushka.org/demo/slider/auto.html).
