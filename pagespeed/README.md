# PageSpeed

## Table of Contents
  1. [Performance](#performance)

## Performance

### Images
  <a name="image-format"></a><a name="1.1"></a>
  - [1.1](#image-format) Next generation image.
    
    Use next generation image formats when possible, WebP is recommened based on avif browser [`compatibility`](https://caniuse.com/avif) issues. [`Serve images in modern formats`](https://developer.chrome.com/docs/lighthouse/performance/uses-webp-images/?utm_source=lighthouse&utm_medium=lr)
   
    > Why? The images will be smaller and wil load faster., most CDN's support generating WebP Images.

  <a name="image-sizes"></a><a name="1.2"></a>
  - [1.2](#image-sizes) Responsive images
  
    Use responsive images, for different resolutions when possible. [`Properly size images`](https://developer.chrome.com/docs/lighthouse/performance/uses-responsive-images/?utm_source=lighthouse&utm_medium=lr)

    > Why? When u serve images for different resolutions/devices, the actual image is loaded is not larger than is rendered.

    It is not possible to serve an image for every resolution so based on design pick the breakpoints for example mobile,tablet,desktop.

    Trick for boosting pagespeed numbers add 412 & 1350 as resolutions, pagespeed uses those resolutions for measuring.

    ```html
    <!-- min-width can differ based on design -->
    
    <picture>
     <source media="(min-width:1440px)" srcset="https://cdn.images.com/largeimage.jpg?width=1200&height=600format=webp" type="image/webp">
     <source media="(min-width:1350px)" srcset="https://cdn.images.com/largeimage.jpg?width=1350&height=675format=webp" type="image/webp">
     <source media="(min-width:1024px)" srcset="https://cdn.images.com/largeimage.jpg?width=1024&height=512format=webp" type="image/webp">
     <source media="(min-width:768px)" srcset="https://cdn.images.com/largeimage.jpg?width=768&height=384format=webp" type="image/webp">
     <source media="(min-width:412px)" srcset="https://cdn.images.com/largeimage.jpg?width=412&height=206format=webp" type="image/webp">
     <img loading="eager" width="1200" height="600" fetchpriority="high" src="https://cdn.images.com/largeimage.jpg?width=1200&height=600format=webp">
    </picture>
    ```

  <a name="image-loading"></a><a name="1.3"></a>
  - [1.3](#image-loading) Image loading.
  
    Lazyload all images that are offscreen. [`Defer offscreen images`](https://developer.chrome.com/docs/lighthouse/performance/offscreen-images)

    > Why? If images are not lazyloaded it can block loading other critical recoureces.

    All images onscreen set the loading attribute to eager and for the first image fetchpriority to high so it gets the highest priority.
    ```html
    <img loading="eager" width="1200" height="600" fetchpriority="high" src="https://cdn.images.com/largeimage.jpg?width=1200&height=600format=webp">
    ```
    All offscreen images should have the loading attribute to lazy, don't forget logo's, icons in the footer.
    ```html
    <img loading="lazy" width="1200" height="600" src="https://cdn.images.com/largeimage.jpg?width=1200&height=600format=webp">
    ```

### Bundeling

### DOM size

### Thirt party scripts

## Accessibility

## Best Practices

## SEO


