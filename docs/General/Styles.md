---
layout: default
title: Styles & Design
parent: General
nav_order: 3
---

# Typography

## Fonts
Any fonts less than 12px must STRICTLY be <span style="font:600 11px Times">Serif</span> only.

# Images
## Size
- The maximum size of any image for the given component must be 10% more than its size in pixels on a standard 1080p display. So say if it is supposed to be 600x400, make it not more than 660x440
- All images (Exception: External Images & SVGs) must have `srcset` attribute and must have multiple images to display the correct size on the correct display. A mobile does not need to load a 4K image
- All images must have strictly defined height and width, either inline or in CSS

## Fallbacks
All images must have `onerror`
```html
<img src="" srcset="" alt="About the image" onerror="this.src = 'someOtherImage'" />
```
as a fallback to display another image of same dimensions in case this doesn't load & an alt attribute for the visually impaired

## Resolution switching using `srcset`&`sizes` Attribute
`srcset`: attribute accepts multiple images with their respective width in pixels, and the browser uses these values to choose between provided images

`sizes`: attribute defines the space that the image will take up on the screen
```html
<picture>
   <source
      srcset="small-car-image.jpg 400w,
              medium-car-image.jpg 800w,
              large-car-image.jpg 1200w"
      sizes="(min-width: 1280px) 1200px,
             (min-width: 768px) 400px,
             100vw">
   <img src="medium-car-image.jpg" alt="Car">
</picture>
```
_It is advisable not to use the_ `picture` _tag just for Resolution Switching since the same can be achieved using the updated version of the_ `img` _tag. But, in most cases, we need to handle both Resolution Switching and Art Direction simultaneously, and the_ `picturetag` _is the best solution_

## Art Direction Using `media` Attribute

The main idea is to display different images based on the screen sizes of the device. With `picture` tag, we can easily achieve resolution switching by using multiple `source` tags inside the `picture` tag.
```html
<picture>
   
   <source ....>
   <source ....>
   <source ....>
</picture>
```
This is a complete example of using Art Direction and Resolution Switching using a `picture` tag
```html
<picture>
     
   <source media="(orientation: landscape)"
             
      srcset="land-small-car-image.jpg 200w,
              land-medium-car-image.jpg 600w,
              land-large-car-image.jpg 1000w"
             
      sizes="(min-width: 700px) 500px,
             (min-width: 600px) 400px,
             100vw">
     
   <source media="(orientation: portrait)"
             
      srcset="port-small-car-image.jpg 700w,
              port-medium-car-image.jpg 1200w,
              port-large-car-image.jpg 1600w"
             
      sizes="(min-width: 768px) 700px,
             (min-width: 1024px) 600px,
             500px">
     
   <img src="land-medium-car-image.jpg" alt="Car">
</picture>
```
The last `img` tag is there for browsers that do not support `picture` tags

## Partially Supported Image Types
There are different images types such as webp, svg , and avif which provide a higher user experience level but there are some limitations in some browsers which can be solved using `picture` tag as it allows to include multiple sources inside it
```html
<picture>
  <source srcset="test.avif" type="image/avif">
  <source srcset="test.webp" type="image/webp">
  <img src="test.png" alt="test image">
</picture>
```
