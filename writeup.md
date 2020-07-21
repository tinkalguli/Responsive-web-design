# Responsive web design

Responsive web design is an approach to develop all screen-size versions of your websites.The websites should worked in any divice so that users can open the website from any device . For that our website should be responsive. The responsive web design is accomplished by making the layouts responsive and adaptive.

> *Responsive:* Responsive layout that reacts quickly and positively to any change. The responsive layouts are also known as flexible layouts, which will have fluidity. If the viewport width changes, the layout will also change fluidly. Flexible layout covers two things which is "flexible layout" and "flexible media".

> *Adaptive:* The adaptive layouts changes based on a new purpose or condition. In CSS "media queries" are used to conditionally apply CSS rules.

So the responsive web design is broken into three main components: *flexible layouts*,  *flexible media*, and *media queries*.

## Flexible Layouts

Flexible layout or responsive layout respond quickly and fluidly to any change. We can create a flexible layout by creating the flexible container. For that we have to use relative units of length which is percentage(%), viewport width, viewport height etc.

## Flexible Media

We can get a flexible media by applying `max-width: 100%` to those media types. Applying so when the viewport size gets smaller the media will also scale down as per the container width.

```
img, video, audio {
    max-width: 100%;
    height: auto;
}
```

### Flexible Embeded Media

Unfortunately, the `max-width: 100%` trick doesn't work well with the embedded media, specifically iframes. For example, when we embed third-party media such as YouTube, it requires an `iframe` tag.

To make embedded media first embedded media must have 100% width and height and also `position: absolute`. Still the embedded media dose not have flexibility so the parent element must have `position: relative` , `width: 100%` and `height: 0` . For a flexible height parent must have  `padding-bottom` of `56.25%` which is for `16:9` aspect ratio media. Calculation for the `padding-bottom` would be `(9/16)*100`.

```
<!-- HTML -->
  <div class="wrapper">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/LXb3EKWsInQ" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
  </div>

  <!-- CSS -->
  .wrapper {
    height: 0;
    padding-bottom: 56.25%; /* 16:9 */
    position: relative;
    width: 100%;
  }
  iframe {
    height: 100%;
    left: 0;
    position: absolute;
    top: 0;
    width: 100%;
  }
```