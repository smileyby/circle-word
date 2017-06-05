最近越来越懒了。

http://www.w3cplus.com/css3/css-secrets/circular-text.html

先放个地址占个位置，等研究懂了在把原理写在这。

```html

<div class="circular">
    circular reasoning works because
</div>

```

```css

/**
 * Text on a circle
 */

body {
    font: bold 120% Helvetica, sans-serif;
}

.circular {
    width: 30em;
    height: 30em;
    margin: 4em auto 0;
}

.circular svg {
    display: block;
    overflow: visible;
    xtransition: 10s linear transform;
}

.circular svg:hover { transform: rotate(-2turn); }

.circular text { fill: currentColor }
.circular path { fill: none; }

```

```js

function $$(selector, context) {
    context = context || document;
    var elements = context.querySelectorAll(selector);
    return Array.prototype.slice.call(elements);
}

$$('.circular').forEach(function(el) {
    var NS = "http://www.w3.org/2000/svg";
    
    var svg = document.createElementNS(NS, "svg");
    svg.setAttribute("viewBox", "0 0 100 100");
    
    var circle = document.createElementNS(NS, "path");
    circle.setAttribute("d", "M0,50 a50,50 0 1,1 0,1z");
    circle.setAttribute("id", "circle");
    
    var text = document.createElementNS(NS, "text");
    var textPath = document.createElementNS(NS, "textPath");
    textPath.setAttributeNS("http://www.w3.org/1999/xlink", 'xlink:href', '#circle');
    textPath.textContent = el.textContent;
    text.appendChild(textPath);
    
    svg.appendChild(circle);
    svg.appendChild(text);
    
    el.textContent = '';
    el.appendChild(svg);
});

```
