# Responsive web design

Responsive web design is an approach to develop all screen-size versions of your websites.The websites should worked in any divice so that users can open the website from any device . For that our website should be responsive. The responsive web design is accomplished by making the layouts responsive and adaptive.

> ***Responsive:*** Responsive layout that reacts quickly and positively to any change. The responsive layouts are also known as flexible layouts, which will have fluidity. If the viewport width changes, the layout will also change fluidly. Flexible layout covers two things which is "flexible layout" and "flexible media".

> ***Adaptive:*** The adaptive layouts changes based on a new purpose or condition. In CSS "media queries" are used to conditionally apply CSS rules.

So the responsive web design is broken into three main components: **flexible layouts**,  **flexible media**, and **media queries**.

## Flexible Layouts

Flexible layout or responsive layout respond quickly and fluidly to any change. We can create a flexible layout by creating the flexible container. For that we have to use relative units of length which is percentage(%), viewport width(vw), viewport height(vh) etc.

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

## Media Queries

Media queries provide the ability to apply CSS rules conditionally. We can apply CSS specifically for an individual browser or depending on the viewport width or device orientations. The media queries provide the ability to present our same HTML content in different styles on different sizes of screens. It can be different for small devices and different for larger devices.

### Initializing Media Query

There are a couple of different ways to use media queries i.e. by linking a new css file to html , importing a new stylesheet using `@import` rule or the most recommended is using `@media` rule inside an existing stylesheet.

##### *HTML*

```
<!-- Separate CSS File -->
  <link href="styles.css" rel="stylesheet" media="all and (max-width: 1024px)">
```

##### *CSS*

```
/* @import Rule */
  @import url(styles.css) all and (max-width: 1024px) {...}
```

```
@media screen and (max-width: 992px) {
    .....
  }
```

For example:

```
<!-- CSS -->
  body {
    background-color: red;
  }
  <!-- Media Queries -->
  @media screen and (max-width: 992px) {
    body {
      background-color: green;
    }
  }
  @media screen and (max-width: 768px) {
    body {
      background-color: blue;
    }
  }
```

In the above example, the background-color of the body will be red by default. But there are two other conditions also which are applied using media queries, those are the conditional CSS rules. When the viewport width will be below 992px the background-color will be green and below 768px it will be blue.

The media rule depends upon different factors like `media type, logical operators, and media features`. The query begins with `@media` follows by "media type" and may include "media features and values". When the condition for media feature and value is true the styles are applied or if it is false the styles are ignored.

#### Media Type

The common media types of media queries are `all`, `screen`, `print`, `tv`, and `braille`. The default media type is `screen`. This media types are used with media features seperating by logical operators. Let's take a look at the logical operators.

#### Logical Operators in Media Queries

We have three logical operstors in media queries which are `and`, `not` and `only`.These operators helps to build powerful expressions.

##### and

The and operator is used to add an extra condition to the media query. For example:

```
@media all and (min-width: 768px) and (max-width: 992px) {
    .....
  }
```
In the above example there are two conditions `min-width: 768px` and `max-width: 992px` .Also there is a media type which is `all` so it will be applied to all the media type between `768px` and `992px`. 

##### not

The not logical operator negates a query specified in the media query. The media rule select all the query to accept the specified one. For example:

```
@media not screen and (color) {
    .....
  }
```

In the above example, the expression will be applied to the screens which do not have color. The black and white or monochromatic screens would be selected here.

##### only

This operator is used to select specific media features and media types.

```
@media only screen and (orientation: portrait) {
    ...
  }
```
The above example includes the only operator. The expressions will be applied only when the screen will be in portrait orientation.

#### Media Features in Media Queries

Media Features decide what is going to be selected in the media query expressions. Media query has various media features. Let's see some of them :

##### Height & Width Media Features

The most common media feature used in media query is `height` and `width`. Normally the height and width media feature is prefixed with `min` and `max`. The `height` and `width` media features are based on the viewport width and height. When the expression meets the viewport's width or height specified in the media query the styles are applied.

>***The Min and Max Prefixes***: The min prefix indicates the values greater than or equal to while max indicates the value less than or equal to.

```
@media all and (min-width: 320px) and (max-width: 768px) {
    .....
  }
```

##### Orientation Media Features

The orientation media features include `landscape` and `portrait` values. The `landscape` mode is triggered when the display is wider than taller, and `portrait` mode triggered when the display is taller than the wider. Any of these values used in the expression determines whether the device is in `landscape` or `portrait` orientation.

```
@media all and (orientation: landscape) {
    .....
  }
```

In the above example the exression will applied when the display will be in `landscape` orientation.

##### Aspect Media Features

The `aspect-ratio` and `device-aspect-ratio` features specifies the `width/height` pixel ratio of the device. If the device's ratio is equal to the ratio specified in the expression the styles will be applied. We can also prefix this feature with `min` or `max` stating the ratio below or above specified in the expression.

```
 @media all and (min-device-aspect-ratio: 16/9) {...}
```

In the above example if the device's ratio will be equal to or greater than 16/9 the styles will be applied.

##### Resolution Media Features

The `resolution` media features specify the resolution of the device in pixel, also known as DPI or dot per inch.

```
@media print and (min-resolution: 300dpi) {
    .....
  }
```

In the above example expression will be applied if the resolution is equal to or greater than `300dpi`.

##### Other Media Features

There are some other media features are there like `color`, `color-index`, and `monochromatic`. These media features are less common but can be used whenever needed.

#### Media Queries Demo

In the above we define some specific point where the website will implement the media queries like below 768px and between 768px and 992px. Here the specific points are called `breakpoints`.

To write a media query we just have to take a break point and then inside that we can put normal css.

##### CSS Breakpoints to Create Responsive Layout

CSS breakpoints are the points where the content responds according to the device width, allowing the best possible way to show the layout to the user. But now comes a big question `how to choose breakponts` . For that we should take such a way that covers all the device. The ideal option is to choose breakpoints based on the content. This will allow you to simply add breakpoints where your content needs adjustment. This will keep your media query lot simpler and manageable. 

Typical device breakpoints widely used:

*Extra small devices (phones, 600px and down)*

```
 @media screen and (max-width: 600px) {
    ...
  }
```

*Small devices (portrait tablets and large phones, 600px and up)*

```
@media screen and (min-width: 600px) and (max-width: 768px) {
    ...
  }
```

*Medium devices (landscape tablets, 768px and up)*

```
@media screen and (min-width: 768px) and (max-width: 992px) {
    ...
  }
```

*Large devices (laptops/desktops, 992px and up)*

```
@media only screen and (min-width: 992px) and (max-width: 1200px) {
    ...
  }
```

*Extra large devices (large laptops and desktops, 1200px and up)*

```
@media only screen and (min-width: 1200px) {
    ...
  }
```
These are the five common groups that cover all the devices.

>We should always try to define a breakpoint where your content breaks and needs to be restructured. It should be always based on your content, not devices.

