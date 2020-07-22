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

### Media Type

The common media types of media queries are `all`, `screen`, `print`, `tv`, and `braille`. The default media type is `screen`. This media types are used with media features seperating by logical operators. Let's take a look at the logical operators.

### Logical Operators in Media Queries

We have three logical operstors in media queries which are `and`, `not` and `only`.These operators helps to build powerful expressions.

#### and

The and operator is used to add an extra condition to the media query. For example:

```
@media all and (min-width: 768px) and (max-width: 992px) {
    .....
  }
```
In the above example there are two conditions `min-width: 768px` and `max-width: 992px` .Also there is a media type which is `all` so it will be applied to all the media type between `768px` and `992px`. 

#### not

The not logical operator negates a query specified in the media query. The media rule select all the query to accept the specified one. For example:

```
@media not screen and (color) {
    .....
  }
```

In the above example, the expression will be applied to the screens which do not have color. The black and white or monochromatic screens would be selected here.

#### only

This operator is used to select specific media features and media types.

```
@media only screen and (orientation: portrait) {
    ...
  }
```
The above example includes the only operator. The expressions will be applied only when the screen will be in portrait orientation.

### Media Features in Media Queries

Media Features decide what is going to be selected in the media query expressions. Media query has various media features. Let's see some of them :

#### Height & Width Media Features

The most common media feature used in media query is `height` and `width`. Normally the height and width media feature is prefixed with `min` and `max`. The `height` and `width` media features are based on the viewport width and height. When the expression meets the viewport's width or height specified in the media query the styles are applied.

>***The Min and Max Prefixes***: The min prefix indicates the values greater than or equal to while max indicates the value less than or equal to.

```
@media all and (min-width: 320px) and (max-width: 768px) {
    .....
  }
```

#### Orientation Media Features

The orientation media features include `landscape` and `portrait` values. The `landscape` mode is triggered when the display is wider than taller, and `portrait` mode triggered when the display is taller than the wider. Any of these values used in the expression determines whether the device is in `landscape` or `portrait` orientation.

```
@media all and (orientation: landscape) {
    .....
  }
```

In the above example the exression will applied when the display will be in `landscape` orientation.

#### Aspect Media Features

The `aspect-ratio` and `device-aspect-ratio` features specifies the `width/height` pixel ratio of the device. If the device's ratio is equal to the ratio specified in the expression the styles will be applied. We can also prefix this feature with `min` or `max` stating the ratio below or above specified in the expression.

```
 @media all and (min-device-aspect-ratio: 16/9) {...}
```

In the above example if the device's ratio will be equal to or greater than 16/9 the styles will be applied.

#### Resolution Media Features

The `resolution` media features specify the resolution of the device in pixel, also known as DPI or dot per inch.

```
@media print and (min-resolution: 300dpi) {
    .....
  }
```

In the above example expression will be applied if the resolution is equal to or greater than `300dpi`.

#### Other Media Features

There are some other media features are there like `color`, `color-index`, and `monochromatic`. These media features are less common but can be used whenever needed.

### Media Queries Demo

In the above we define some specific point where the website will implement the media queries like below 768px and between 768px and 992px. Here the specific points are called `breakpoints`.

To write a media query we just have to take a break point and then inside that we can put normal css.

#### CSS Breakpoints to Create Responsive Layout

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

#### Mobile First Approach

We have two approach to write media queries i.e. `Mobile-First Approach` and `desktop-first approach`. The above examples are based on the `desktop-first approach`. In the `mobile-first approach` the styles are applied to the mobile or small devices first and the advanced styles or the media queries  are applied to the larger devices. This approach is taken using `min-width` media feature. For example :

```
/* This applies from 0px to 600px */
  body {
    background: red;
  }

  /* This applies from 600px onwards */
  @media (min-width: 600px) {
    body {
      background: green;
    }
  }
```

In the above example, the body will have a `red` background below `600px`. But it's background will change to green at `600px` and beyond.

It is believed that taking a `mobile-first approach` is considered as best practice, and it's true also. But the `mobile-first approach` has some advantages over the `desktop-first approach`. Because generally, the layout for larger devices is a bit complicated than the smaller devices. 

##### *Typical Breakpoints of Mobile-First Appraoch*

```
@media screen and (max-width: 600px)  {...}
  @media screen and (min-width: 600px)  {...}
  @media screen and (min-width: 768px)  {...}
  @media screen and (min-width: 992px) {...}
  @media screen and (min-width: 1200px) {...}
```

#### Desktop First Approach

On the other hand in `desktop-first approach` the styles are first applied to desktop or larger devices. Thereafter advanced styles are written to override the styles for small screen devices via media query.

```
body {
    background: green;
  }

  /* This applies from 0px to 600px onwards */
  @media (min-width: 600px) {
    body {
      background: red;
    }
  }
```

The body will have `green` background for all width devices, but if the screen is below `600px` the beckground will change to `red`.

### Viewport

The viewport is a visible area of the window in which web content can be seen i.e. screen. The viewport size can be vary from device to device , mobile or small devices have the small viewport and the large devices have the large viewport. 

Apple invented the `viewport` meta tag to let control over the viewport size, scale, and resolution of a website. The `viewport` meta tag is applied inside the `head` tag in the HTML document. That gives instruction to the browser to control the page's dimension and scaling.

```
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

#### Viewport Width & Height

The `width=device-width` part will inherit the default width of the device for the best results and best view. Apart from viewport width you can also viewport height, `height=device-height`.

#### Viewport Scale

##### Initial-scale

The `initial-scale` of the website should be set to `1` that sets the zoom level when page load for the first time i.e. no zoom at all. The `initial-scale` can be set between `0` to `10`.

##### Other controls

Apart from `initial-scale` to control scalable capability of the page there comes few other properties also, `minimum-scale`, `maximum-scale`, and `user-scalable`.

###### Minimum-scale

The `minimum-scale` tells the browser that to which point the user can scale or zoom out the webpage. The `minimum-scale` should be equal or lower than the `initial-scale`.

###### Maximum-scale

The `maximum-scale` tells the browser that to which point the user can scale or zoom in the webpage. The `maximum-scale` should be equal or greater than the `initial-scale`.

###### User-scalable

By default, the `user-scalable` value is `yes`. However, if you want to turn off the zooming you can set the value to `no`. Turning off the zooming ability is not a good idea. It harms the accessibility, usability, prevents disable people from viewing the website as they desire.

*Never forget to apply this viewport meta tag in your document.*

>*Responsive font-size :* Now we know that how to make responsive the containers and the page responsive but we should keep in mind that we have to make the fonts flexible. For that we can use relative units like `view width(vw)` for the font size but it will make the font size very small in the mobile device(`desktop-first approach`) or it will make the font size very large in the large device(`mobile-first approach`).So we can use absolute units. If we use pixel value then we have to initialize font-size in every `break-point`. For this problem we have some realy good units which is `rem` and `em`.

#### Rem

The `rem` is always related to the root elememt's `font-size` i.e. `html`. For example:

```
html {
  font-size: 20px;
}

section {
  font-size: 0.5rem;
}
```

In the above example `section` will be having `font-size` of `10px`.

We can also use `rem` every where like padding, margin etc. For example :

```
html {
  font-size: 10px;
}

section {
  padding: 2rem;
}
```

In the above example `section` will be having `padding` of `20px`.

Now we know that the `rem` is related to the root element so we can use this by changing the root element's `font-size` in every break-point. For example :

```
html {
  font-size: 20px;
}

section {
  padding: 2rem;
  font-size: 0.5rem;
}

@media screen and (max-width: 768px){
  html {
    font-size: 16px;
  }
}
```

In the above example when the viewport will reduce to `768px` then the `font-size` and `padding` of the `section` will be reduce with related to the `html`'s `font-size` i.e. `font-size: 8px` and  `padding: 32px`.

#### Em

The `em` is always related to the some element's font-size. If the font-size of the element is not available then it will related to the parent elememt's `font-size`. For example:

```
section {
  font-size: 10px;
  padding: 2rem;
}
```
In the above example `padding` of the `section` will be `20px`.

```
<!--html-->

<section>
  <article>
    ...
  </article>
</section>

/*css*/
section {
  font-size: 10px;
}

article {
  padding: 2rem;
  font-size: 1rem;
}
```

In  the above example the `padding` and the `font-size` of the `article` will be `20px` and `10px` respectively.

*We can use `rem` and `em` individually or together at a same time*
