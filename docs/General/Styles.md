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

# Use of <Picture> instead of <img>

## Issues with Image resolutions
Image issues can be grouped into two major issues;

* Resolution Switching — Problems of serving smaller size images for narrow screen devices.
* Art Direction — Problem of showing different images on different screen sizes.

## Resolution Switching using ``srcset`` & sizes Attributes

Suppose you use a simple Img tag for high-res images. In that case, that same image is used in each device your application runs, and indeed it will result in performance issues in devices with lower screen resolutions like mobile devices.

This could result in longer image loading times and top to bottom partial image loadings.

This issue can be easily addressed with the ``picture`` tag by using ``srcset`` and ``sizes`` attributes.

```
<picture>
   <source      

        srcset="small-car-image.jpg 400w,
              medium-car-image.jpg 800w,
              large-car-image.jpg 1200w"
        
        sizes="(min-width: 1280px) 1200px,
             (min-width: 768px) 400px,
             100vw">

   <img src="medium-car-image.jpg" alt="Car">.

</picture>
```

``srcset`` attribute accepts multiple images with their respective width in pixels, and the browser uses these values to choose between provided images. In the above example, there are 3 versions of the same image in 3 different sizes.

The ``sizes`` attribute defines the space that the image will take up on the screen. In the above example, the image will take up 1200px if the screen’s minimum width is 1280px.


Having said that, it is advisable not to use the Picture tag just for Resolution Switching since the same can be achieved using the updated version of the Img tag (which has more browser support)

But, in most cases, we need to handle both Resolution Switching and Art Direction simultaneously, and the ``picture`` tag is the best solution.


## Art Direction Using media Attribute

The main idea behind Art Direction is to display different images based on the screen sizes of the device. In most cases, an image that looks fabulous on larger screens may get cropped or look so small when you switch to mobile.

We can address this issue by providing different versions of the image for different screen sizes. These different versions can be landscape, portrait, or any customized version of the same image.

With picture tag, we can easily achieve resolution switching by using multiple source tags inside the picture tag.

```
<picture>
   
   <source ....>
   <source ....>
   <source ....>

</picture>
```

Then we can use ``media`` attribute to define different media conditions where these sources will be used. We can also use ``srcset`` and ``sizes`` attributes in a similar manner as we discussed in the previous section.

The following example shows a complete example of using Art Direction and Resolution Switching using a ``picture`` tag.

```
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
     
   <img src="land-medium-car-image.jpg" alt="Car"></picture>
```

If the screen orientation is landscape browser will show the images from the first image set, and if the orientation is portrait browser will use the second set. In addition to that, you can use ``media`` attribute with ``max-width`` and ``min-width`` parameters:

```

```