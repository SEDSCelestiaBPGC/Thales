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
as a fallback to display another image of same dimensions in case this doesn't load & an alt attribute for the visually impaired.




# Use of \<Picture> instead of \<img>

## Issues with Image resolutions
Image issues can be grouped into two major issues;

- Resolution Switching — Problems of serving smaller size images for narrow screen devices.
- Art Direction — Problem of showing different images on different screen sizes.

## Resolution Switching using ``srcset`` & sizes Attributes

When you use a simple Img tag for high-res images, that same image is used in each device your application runs, and may result in performance issues in devices with lower screen resolutions like mobile devices.

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
&nbsp;   


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
<picture>
     <source media="(max-width: 767px)" ....>
     <source media="(min-width: 768px)" ....>
</picture>
```

The last ``img`` tag is there for backward compatibility for browsers that do not support ``picture`` tags.  

  
## Using with Partially Supported Image Types
With the rapid development of technologies, different types of modern image types are introduced day by day. Some of these types such as ``webp``, ``svg`` , and ``avif`` provide a higher user experience level.

On the other hand, there are limitations in some browsers on these modern image types, and things will get backfired if we don’t use the compatible image types.

But, we can easily address this issue by using Picture tag since it allows us to include multiple sources inside that.

```dotnetcli
<picture>  
    <source srcset="test.avif" type="image/avif">
    <source srcset="test.webp" type="image/webp">
    <img src="test.png" alt="test image">
</picture>
```

The above example includes three image types from ``avif``, ``webp``, and ``png`` formats. First, the browser will try ``avif`` format, and if that fails, it will try ``webp`` format. If the browser does not support both of these, it will use ``png`` image.

Things got more interesting about picture tag when Chrome announced that “DevTools will provide two new emulations in the Rendering tab to emulate partially supported image types”.

From Chrome 88 Onwards, You Can Use Chrome DevTools to Check Browser Compatibility with Image Types.  

&nbsp;  
![Using Chrome DevTools for Image Compatibility Emulations](https://i.imgur.com/uDdNJ7O.png)

&nbsp;  

## tl;dr and Conclusion

If we use the provided attributes like ``srcset`` and ``size`` wisely, we can get the maximum out of the ``img`` tag. For example, we can resolve Resolution Switching only using the ``img`` tag.

On the other hand, we can use ``picture`` tag to achieve both Resolution Switching and Art Direction easily using media queries and other provided attributes.

The ability to work with partially supported image types and Chrome DevTools support can be recognized as additional plus points for ``picture`` tag.

Hence one must carefully think and use most suitable element based on requirements.