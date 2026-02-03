# PageSpeed

A good PageSpeed score directly impacts SEO rankings. Google uses Core Web Vitals as a ranking factor, meaning slow sites rank lower in search results. Fast-loading pages also reduce bounce rates and improve user experience, leading to better engagement and conversions.

## Table of Contents
  1. [Testing](#testing)
  1. [Images](#images)
  1. [Videos](#videos)
  1. [Bundling](#bundling)
  1. [DOM size](#dom-size)
  1. [Third party scripts](#third-party-scripts)
  1. [Resource preloading](#resource-preloading)
  1. [Accessibility](#accessibility)
  1. [Console errors](#console-errors)
  1. [Tips & Tricks](#tips--tricks)

## Testing

Regular testing prevents performance regressions and ensures issues are caught early when they're easier to fix.

  <a name="testing-regularly"></a><a name="0.1"></a>
  - [0.1](#testing-regularly) Test regularly during development
  
    Use [PageSpeed Insights](https://pagespeed.web.dev/) to test your pages throughout the build process.

    > Why? Catching performance issues early is easier to fix than addressing them after the site is finished. Performance regressions can sneak in with each new feature.

    ✅ **Do:**
    - Test after adding new components or features
    - Test both mobile and desktop scores
    - Address issues before moving to the next feature
    
    🚫 **Don't:**
    - Wait until the site is finished to test performance
    - Ignore score drops during development
    - Only test on fast networks or powerful devices

## Images

Images are often the largest assets on a page. Optimizing format, size, and loading strategy has the biggest impact on performance.

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
     <source media="(min-width:1440px)" srcset="https://cdn.images.com/largeimage.jpg?width=1200&height=600&format=webp" type="image/webp">
     <source media="(min-width:1350px)" srcset="https://cdn.images.com/largeimage.jpg?width=1350&height=675&format=webp" type="image/webp">
     <source media="(min-width:1024px)" srcset="https://cdn.images.com/largeimage.jpg?width=1024&height=512&format=webp" type="image/webp">
     <source media="(min-width:768px)" srcset="https://cdn.images.com/largeimage.jpg?width=768&height=384&format=webp" type="image/webp">
     <source media="(min-width:412px)" srcset="https://cdn.images.com/largeimage.jpg?width=412&height=206&format=webp" type="image/webp">
     <img loading="eager" width="1200" height="600" fetchpriority="high" src="https://cdn.images.com/largeimage.jpg?width=1200&height=600&format=webp">
    </picture>
    ```

  <a name="image-loading"></a><a name="1.3"></a>
  - [1.3](#image-loading) Image loading.
  
    Lazyload all images that are offscreen. [`Defer offscreen images`](https://developer.chrome.com/docs/lighthouse/performance/offscreen-images)

    > Why? If images are not lazyloaded it can block loading other critical recoureces.

    All images onscreen set the loading attribute to eager and for the first image fetchpriority to high so it gets the highest priority.
    ```html
    <img loading="eager" width="1200" height="600" fetchpriority="high" src="https://cdn.images.com/largeimage.jpg?width=1200&height=600&format=webp">
    ```
    All offscreen images should have the loading attribute to lazy, don't forget logo's, icons in the footer.
    ```html
    <img loading="lazy" width="1200" height="600" src="https://cdn.images.com/largeimage.jpg?width=1200&height=600&format=webp">
    ```
    If u need to boost the loading of an image further, you can use link preloading in the head.

    ```js
    import ReactDOM from 'react-dom';
    ReactDOM.preload(url, { as: 'image' })
    ```
    
    ```html
    <link rel="preload" href="https://cdn.images.com/largeimage.jpg?width=1200&height=600&format=webp" as="image">
    ```

  <a name="image-dimensions"></a><a name="1.4"></a>
  - [1.4](#image-dimensions) Always specify width and height
  
    Include `width` and `height` attributes on all images to prevent Cumulative Layout Shift (CLS). [`Optimize CLS`](https://web.dev/optimize-cls/)

    > Why? Without dimensions, the browser doesn't know how much space to reserve. When the image loads, content shifts, causing a poor user experience and lower CLS scores.

    ✅ **Do:**
    ```html
    <img src="product.webp" width="400" height="300" alt="Product" />
    ```

    ```css
    /* Use CSS to make images responsive while maintaining aspect ratio */
    img {
      max-width: 100%;
      height: auto;
    }
    ```

    🚫 **Don't:**
    ```html
    <!-- Missing dimensions causes layout shift -->
    <img src="product.webp" alt="Product" />
    ```


## Videos

Videos can significantly slow down page load if not handled properly. Use modern formats and lazy loading strategies.

  <a name="video-format"></a><a name="1.4"></a>
  - [1.4](#video-format) Video format and compression
    
    Use modern video codecs like H.265 (HEVC) or VP9 for better compression. [`Efficient video formats`](https://web.dev/efficient-animated-content/)
   
    > Why? Modern codecs provide better compression ratios, reducing file size by up to 50% compared to H.264 while maintaining quality.

    ✅ **Do:**
    ```html
    <video width="1200" height="600" poster="thumbnail.webp">
      <source src="video.webm" type="video/webm">
      <source src="video.mp4" type="video/mp4">
    </video>
    ```

    🚫 **Don't:**
    ```html
    <!-- Autoplay without user interaction wastes bandwidth -->
    <video autoplay muted loop>
      <source src="heavy-background-video.mp4">
    </video>
    ```

  <a name="video-loading"></a><a name="1.5"></a>
  - [1.5](#video-loading) Video loading strategy
  
    Use lazy loading and preload metadata only. [`Lazy load videos`](https://web.dev/lazy-loading-video/)

    > Why? Videos are large resources. Loading them only when needed saves bandwidth and improves initial page load time.

    ✅ **Do:**
    ```html
    <!-- Lazy load with metadata preload -->
    <video 
      width="1200" 
      height="600" 
      controls 
      preload="metadata" 
      poster="thumbnail.webp"
    >
      <source src="video.mp4" type="video/mp4">
    </video>
    ```

    ```jsx
    // Lazy load video component
    import dynamic from 'next/dynamic';
    
    const VideoPlayer = dynamic(() => import('@/components/VideoPlayer'), {
      loading: () => <img src="thumbnail.webp" alt="Loading..." />
    });
    ```

    🚫 **Don't:**
    ```html
    <!-- Don't preload entire video -->
    <video preload="auto" src="large-video.mp4"></video>
    
    <!-- Don't autoplay above the fold -->
    <video autoplay muted loop src="hero-video.mp4"></video>
    ```

  <a name="video-poster"></a><a name="1.6"></a>
  - [1.6](#video-poster) Always use poster images
  
    Provide poster images for all videos to show content before playback.

    > Why? Poster images load faster than videos and provide immediate visual feedback, improving perceived performance.

    ✅ **Do:**
    ```html
    <video 
      poster="thumbnail.webp" 
      width="1200" 
      height="600"
      preload="none"
    >
      <source src="video.mp4" type="video/mp4">
    </video>
    ```

    🚫 **Don't:**
    ```html
    <!-- No poster means blank space until video loads -->
    <video src="video.mp4"></video>
    ```

  <a name="video-attributes"></a><a name="1.9"></a>
  - [1.9](#video-attributes) Use appropriate video attributes
  
    Apply attributes to control video behavior and reduce unnecessary resource loading.

    > Why? Proper attributes prevent unwanted behaviors like remote playback prompts and picture-in-picture, reducing browser overhead.

    ✅ **Do:**
    ```html
    <video 
      width="1200" 
      height="600"
      poster="thumbnail.webp"
      preload="metadata"
      disablepictureinpicture
      disableremoteplayback
      playsinline
    >
      <source src="video.mp4" type="video/mp4">
    </video>
    ```

    - `disableremoteplayback` - Prevents casting prompts on mobile devices
    - `disablepictureinpicture` - Removes PiP controls if not needed
    - `playsinline` - Prevents fullscreen on mobile (iOS especially)
    
## Bundling

Smaller JavaScript bundles mean faster parsing and execution. Code splitting and tree shaking reduce what users need to download.

  <a name="bundle-size"></a><a name="2.1"></a>
  - [2.1](#bundle-size) Dynamic imports
  
    Use dynamic imports for components that are not immediately visible or used conditionally. [`Code splitting`](https://nextjs.org/docs/app/building-your-application/optimizing/lazy-loading)

    > Why? Dynamic imports reduce the initial bundle size by loading code only when needed.

    ✅ **Do:**
    ```js
    // Load heavy components dynamically
    import dynamic from 'next/dynamic';
    
    const HeavyModal = dynamic(() => import('@/components/HeavyModal'));
    const Chart = dynamic(() => import('@/components/Chart'), { ssr: false });
    ```

    🚫 **Don't:**
    ```js
    // Don't import heavy components that aren't immediately needed
    import HeavyModal from '@/components/HeavyModal';
    import Chart from '@/components/Chart';
    ```

  <a name="bundle-packages"></a><a name="2.2"></a>
  - [2.2](#bundle-packages) Import only what you need
  
    Import specific functions instead of entire libraries. [`Tree shaking`](https://webpack.js.org/guides/tree-shaking/)

    > Why? Importing only needed functions allows tree-shaking to remove unused code from your bundle.

    ✅ **Do:**
    ```js
    import { format } from 'date-fns';
    import debounce from 'lodash-es/debounce';
    ```

    🚫 **Don't:**
    ```js
    import * as dateFns from 'date-fns';
    import _ from 'lodash';
    ```

  <a name="bundle-analysis"></a><a name="2.3"></a>
  - [2.3](#bundle-analysis) Analyze your bundle
  
    Use `@next/bundle-analyzer` to identify large dependencies. [`Bundle analyzer`](https://www.npmjs.com/package/@next/bundle-analyzer)

    > Why? Visualizing bundle composition helps identify optimization opportunities.

    ```bash
    npm install @next/bundle-analyzer
    ```

    ```js
    // next.config.js
    const withBundleAnalyzer = require('@next/bundle-analyzer')({
      enabled: process.env.ANALYZE === 'true',
    });

    export default  withBundleAnalyzer({});
    ```

    ```bash
    ANALYZE=true npm run build
    ```

  <a name="bundle-duplicates"></a><a name="2.4"></a>
  - [2.4](#bundle-duplicates) Check for duplicate dependencies
  
    Identify and remove duplicate packages in your bundle. [`Duplicate dependencies`](https://www.npmjs.com/package/duplicate-package-checker-webpack-plugin)

    > Why? Different versions of the same package can be bundled multiple times, unnecessarily increasing bundle size.

    ✅ **Do:**
    ```bash
    # Check for duplicates
    npx npm-dedupe
    
    # Or use yarn
    yarn dedupe
    ```

    ```js
    // Add to next.config.js for visibility
    const DuplicatePackageCheckerPlugin = require('duplicate-package-checker-webpack-plugin');
    
    module.exports = {
      webpack: (config) => {
        config.plugins.push(new DuplicatePackageCheckerPlugin());
        return config;
      },
    };
    ```

    Common culprits:
    - Multiple versions of `lodash`
    - Duplicate `react` or `react-dom`
    - Multiple date libraries (`moment`, `date-fns`, `dayjs`)


## DOM size

Large and deeply nested DOMs slow down rendering, increase memory usage, and make style calculations expensive.

  <a name="dom-depth"></a><a name="3.1"></a>
  - [3.1](#dom-depth) Keep DOM depth shallow
  
    Limit DOM depth to maximum 32 levels and avoid deeply nested structures. [`Avoid an excessive DOM size`](https://developer.chrome.com/docs/lighthouse/performance/dom-size)

    > Why? Deep DOM trees slow down rendering, increase memory usage, and make style calculations more expensive.

    ✅ **Do:**
    ```jsx
    // Shallow structure
    <article>
      <h2>{title}</h2>
      <p>{content}</p>
    </article>
    ```

    🚫 **Don't:**
    ```jsx
    // Excessive nesting
    <div>
      <div>
        <div>
          <div>
            <article>
              <div>
                <h2>{title}</h2>
              </div>
            </article>
          </div>
        </div>
      </div>
    </div>
    ```

  <a name="dom-nodes"></a><a name="3.2"></a>
  - [3.2](#dom-nodes) Limit total DOM nodes
  
    Keep total DOM nodes under 1500. Aim for fewer than 800 nodes for optimal performance.

    > Why? Large DOMs increase memory consumption, cause slower layout calculations, and delay paint times.

    ✅ **Do:**
    - Use pagination or virtual scrolling for large lists
    - Remove unnecessary wrapper divs
    - Conditionally render components based on visibility
    
    🚫 **Don't:**
    - Render all items in a long list at once
    - Use excessive wrapper elements for styling purposes
    - Keep hidden components mounted in the DOM

  <a name="dom-children"></a><a name="3.3"></a>
  - [3.3](#dom-children) Avoid too many child elements
  
    Limit parent elements to maximum 60 children.

    > Why? Parents with many children cause expensive layout recalculations when children are added, removed, or modified.

## Third party scripts

Third-party scripts like analytics and widgets can block rendering and add significant load time if not managed carefully.

  <a name="script-loading"></a><a name="4.1"></a>
  - [4.1](#script-loading) Load scripts asynchronously
  
    Use `async` or `defer` attributes for third-party scripts. In Next.js, use the Script component with appropriate strategy. [`Efficiently load third-party JavaScript`](https://web.dev/efficiently-load-third-party-javascript/)

    > Why? Third-party scripts can block page rendering and significantly slow down initial load time.

    ✅ **Do:**
    ```jsx
    // Next.js Script component
    import Script from 'next/script';
    
    <Script 
      src="https://analytics.example.com/script.js" 
      strategy="afterInteractive" 
    />
    
    // For non-critical scripts
    <Script 
      src="https://widget.example.com/embed.js" 
      strategy="lazyOnload" 
    />
    ```

    🚫 **Don't:**
    ```jsx
    // Don't use blocking scripts
    <script src="https://analytics.example.com/script.js"></script>
    
    // Don't load in <head> without defer
    <Head>
      <script src="https://heavy-script.js"></script>
    </Head>
    ```

  <a name="script-conditional"></a><a name="4.2"></a>
  - [4.2](#script-conditional) Load scripts conditionally
  
    Only load third-party scripts when actually needed. [`Reduce JavaScript execution time`](https://developer.chrome.com/docs/lighthouse/performance/bootup-time)

    > Why? Loading unnecessary scripts wastes bandwidth and processing time for users who won't use the feature.

    ✅ **Do:**
    ```jsx
    // Load chat widget only when user clicks
    const [showChat, setShowChat] = useState(false);
    
    return (
      <>
        <button onClick={() => setShowChat(true)}>Open Chat</button>
        {showChat && (
          <Script src="https://chat-widget.com/embed.js" />
        )}
      </>
    );
    ```

    🚫 **Don't:**
    ```jsx
    // Don't load chat on every page if rarely used
    <Script src="https://chat-widget.com/embed.js" strategy="afterInteractive" />
    ```

  <a name="script-facades"></a><a name="4.3"></a>
  - [4.3](#script-facades) Use facades for heavy embeds
  
    Replace heavy embeds like YouTube videos with lightweight facades that load the real embed on user interaction. [`Use facades for third-party resources`](https://web.dev/third-party-facades/)

    > Why? Embeds like YouTube can add 500KB+ of resources. Facades reduce this to a few KB until the user actually clicks.

    ✅ **Do:**
    ```jsx
    // Use lite-youtube-embed or similar
    import LiteYouTubeEmbed from 'react-lite-youtube-embed';
    
    <LiteYouTubeEmbed
      id="dQw4w9WgXcQ"
      title="Video title"
    />
    ```

    🚫 **Don't:**
    ```jsx
    // Don't embed full iframe immediately
    <iframe 
      src="https://www.youtube.com/embed/dQw4w9WgXcQ"
      width="560" 
      height="315"
    />
    ```

  <a name="script-self-host"></a><a name="4.4"></a>
  - [4.4](#script-self-host) Self-host when possible
  
    Host third-party scripts on your own domain when feasible to reduce DNS lookups and enable better caching.

    > Why? Self-hosting eliminates additional DNS lookups and connection overhead, and gives you full control over caching headers.

    ✅ **Do:**
    ```jsx
    // Self-hosted analytics
    <Script src="/scripts/analytics.js" strategy="afterInteractive" />
    ```

    🚫 **Don't:**
    ```jsx
    // Multiple external domains slow down loading
    <Script src="https://cdn1.example.com/script1.js" />
    <Script src="https://cdn2.example.com/script2.js" />
    <Script src="https://cdn3.example.com/script3.js" />
    ```

  <a name="script-impact"></a><a name="4.5"></a>
  - [4.5](#script-impact) Analyze third-party script impact
  
    Regularly audit the performance impact of third-party scripts. [`Third-party summary`](https://developer.chrome.com/docs/lighthouse/performance/third-party-summary/)

    > Why? Third-party scripts often grow in size over time and can silently degrade performance. Regular audits help identify problematic scripts.

    ✅ **Do:**
    - Use Chrome DevTools Network tab to measure script sizes and load times
    - Check Lighthouse "Third-Party Usage" section
    - Use [WebPageTest](https://www.webpagetest.org/) for detailed third-party analysis
    - Set up performance budgets for third-party scripts
    
    ```js
    // Use Performance Observer to monitor long tasks
    const observer = new PerformanceObserver((list) => {
      for (const entry of list.getEntries()) {
        console.log('Long task detected:', entry.duration, 'ms');
      }
    });
    observer.observe({ entryTypes: ['longtask'] });
    ```

    Questions to ask:
    - Does this script justify its performance cost?
    - Can we load it later or conditionally?
    - Is there a lighter alternative?
    - Can we self-host it?

## Resource preloading

React DOM provides APIs to hint the browser about resources it will need, reducing connection and download times.

  <a name="resource-prefetchdns"></a><a name="5.1"></a>
  - [5.1](#resource-prefetchdns) Use prefetchDNS for external domains
  
    Call `prefetchDNS` to look up the IP address of servers you'll connect to. [`React prefetchDNS`](https://react.dev/reference/react-dom/prefetchDNS)

    > Why? Resolving DNS early speeds up resource loading from external servers.

    ✅ **Do:**
    ```jsx
    import { prefetchDNS } from 'react-dom';
    
    const MetaResources = () => {
      prefetchDNS("https://cdn.example.com");
      prefetchDNS("https://analytics.example.com");
      return null;
    }
    ```

    🚫 **Don't:**
    ```jsx
    // Don't prefetch your own domain
    prefetchDNS("https://yoursite.com");
    ```

  <a name="resource-preconnect"></a><a name="5.2"></a>
  - [5.2](#resource-preconnect) Use preconnect for known origins
  
    Call `preconnect` to establish early connections to servers you'll request resources from. [`React preconnect`](https://react.dev/reference/react-dom/preconnect)

    > Why? Preconnecting completes DNS lookup, TCP handshake, and TLS negotiation before resources are needed.

    ✅ **Do:**
    ```jsx
    import { preconnect } from 'react-dom';
    
    const MetaResources = () => {
      preconnect("https://fonts.googleapis.com");
      return null;
    }
    ```

    🚫 **Don't:**
    ```jsx
    // Don't preconnect to too many domains (max 4-6)
    preconnect("https://domain1.com");
    preconnect("https://domain2.com");
    preconnect("https://domain3.com");
    // ... 10+ domains
    ```

  <a name="resource-preload"></a><a name="5.3"></a>
  - [5.3](#resource-preload) Use preload for critical resources
  
    Call `preload` to fetch fonts, stylesheets, images, or scripts you know you'll need. [`React preload`](https://react.dev/reference/react-dom/preload)

    > Why? Preloading downloads resources immediately rather than waiting for the browser to discover them.

    ✅ **Do:**
    ```jsx
    
    'use client'
 
    import ReactDOM from 'react-dom'

    const MetaResources = () => {

        preload("/fonts/main-font.woff2", { as: "font" });
        preload("/styles/critical.css", { as: "style" });
        preload("/hero-image.webp", { as: "image" });

        return null
    }

    ```

    🚫 **Don't:**
    ```jsx
    // Don't preload resources that aren't critical
    preload("/footer-icon.svg", { as: "image" });
    preload("/rarely-used-script.js", { as: "script" });
    ```

## Accessibility

Accessibility is a key component of PageSpeed scoring. Lighthouse measures accessibility as part of its audit, and poor accessibility directly impacts your overall score. Beyond metrics, accessible sites are faster for everyone because they use semantic HTML, which browsers parse more efficiently.

  <a name="accessibility-semantic"></a><a name="6.1"></a>
  - [6.1](#accessibility-semantic) Use semantic HTML elements
  
    Use proper HTML elements for their intended purpose. [`Semantic HTML`](https://web.dev/learn/accessibility/structure/)

    > Why? Semantic HTML improves browser parsing speed, enhances SEO, and ensures assistive technologies work correctly. It also reduces the need for extra ARIA attributes and JavaScript workarounds.

    ✅ **Do:**
    - Use `<button>` for clickable actions
    - Use `<nav>`, `<main>`, `<header>`, `<footer>` for page structure
    - Use heading levels (`<h1>` - `<h6>`) in logical order
    - Use `<ul>`, `<ol>` for lists
    
    🚫 **Don't:**
    - Use `<div>` with click handlers instead of `<button>`
    - Skip heading levels (e.g., `<h1>` to `<h4>`)
    - Use `<div>` for everything and rely on classes for meaning

  <a name="accessibility-images"></a><a name="6.2"></a>
  - [6.2](#accessibility-images) Always provide alt text for images
  
    Every `<img>` element must have an `alt` attribute. [`Image alt text`](https://web.dev/learn/accessibility/images/)

    > Why? Missing alt text fails accessibility audits and hurts your Lighthouse score. Screen readers rely on alt text to describe images.

    ✅ **Do:**
    ```html
    <img src="product.webp" alt="Red running shoes" />
    
    <!-- Decorative images should have empty alt -->
    <img src="decoration.webp" alt="" />
    ```

    🚫 **Don't:**
    ```html
    <!-- Missing alt attribute -->
    <img src="product.webp" />
    
    <!-- Non-descriptive alt text -->
    <img src="product.webp" alt="image" />
    ```

  <a name="accessibility-contrast"></a><a name="6.3"></a>
  - [6.3](#accessibility-contrast) Ensure sufficient color contrast
  
    Text must have a contrast ratio of at least 4.5:1 against its background. [`Color contrast`](https://web.dev/learn/accessibility/color-contrast/)

    > Why? Low contrast fails Lighthouse accessibility checks and makes content unreadable for users with visual impairments.

    ✅ **Do:**
    - Use tools like [WebAIM Contrast Checker](https://webaim.org/resources/contrastchecker/) during design
    - Ensure text on images has sufficient contrast or use overlays
    
    🚫 **Don't:**
    - Use light gray text on white backgrounds
    - Rely solely on color to convey information

  <a name="accessibility-interactive"></a><a name="6.4"></a>
  - [6.4](#accessibility-interactive) Make interactive elements accessible
  
    All interactive elements must be keyboard accessible and properly labeled.

    > Why? Inaccessible buttons and links fail Lighthouse audits. Users who navigate with keyboards or assistive devices cannot use inaccessible controls.

    ✅ **Do:**
    ```html
    <button aria-label="Close menu">✕</button>
    <a href="/contact">Contact us</a>
    ```

    🚫 **Don't:**
    ```html
    <!-- Div with click handler is not keyboard accessible -->
    <div onclick="closeMenu()">✕</div>
    
    <!-- Link without meaningful text -->
    <a href="/contact">Click here</a>
    ```

## Console errors

Console errors indicate JavaScript problems that can break functionality and negatively impact performance scores.

  <a name="console-errors"></a><a name="8.1"></a>
  - [8.1](#console-errors) Fix all console errors
  
    Ensure your application runs without JavaScript errors in the browser console. [`No browser errors logged to the console`](https://developer.chrome.com/docs/lighthouse/best-practices/errors-in-console/)

    > Why? Console errors indicate broken JavaScript that can block rendering, cause layout shifts, and prevent functionality from working. Lighthouse flags console errors as a best practices issue, directly impacting your score.

    ✅ **Do:**
    - Check the browser console regularly during development
    - Fix all errors before deploying to production
    - Set up error monitoring (e.g., Sentry) to catch production errors
    - Test error boundaries to handle failures gracefully

    🚫 **Don't:**
    - Ignore console errors during development
    - Deploy code with known JavaScript errors
    - Leave `console.log` statements in production code
    - Catch errors silently without proper handling

## Tips & Tricks

Quick wins and practical tips for improving PageSpeed scores.

  <a name="tips-debugging"></a><a name="9.1"></a>
  - [9.1](#tips-debugging) Debugging performance issues
  
    Tools and techniques for finding performance bottlenecks:

    ```bash
    # Run Lighthouse from CLI for detailed reports
    npx lighthouse https://example.com --view
    
    # Generate a performance trace
    npx lighthouse https://example.com --output=json --output-path=./report.json
    ```

    Chrome DevTools tips:
    - Use **Performance** tab to record and analyze page load
    - Use **Coverage** tab to find unused CSS/JS
    - Use **Network** tab with "Slow 3G" throttling to simulate real conditions
    - Check **Rendering** panel for layout shifts (enable "Layout Shift Regions")

  <a name="tips-region"></a><a name="9.2"></a>
  - [9.2](#tips-region) Deploy near PageSpeed test servers
  
    PageSpeed Insights runs tests from servers located in the United States. Deploying your application to a US region can improve your test scores.

    ✅ **Do:**
    ```js
    // vercel.json - Set region to US for better PageSpeed scores
    {
      "regions": ["iad1"]  // Washington, D.C. (US East)
    }
    ```

  <a name="tips-lighthouse-detection"></a><a name="9.3"></a>
  - [9.3](#tips-lighthouse-detection) Detect Lighthouse to hide interfering elements
  
    Use user-agent detection to hide cookie banners, popups, or other elements that negatively impact PageSpeed scores during Lighthouse tests.

    Elements to consider hiding during Lighthouse tests:
    - Cookie consent banners
    - Newsletter popups
    - Chat widgets
    - Promotional overlays
    - A/B testing scripts

    > ⚠️ Note: This is a legitimate optimization technique. You're not hiding broken functionality—you're removing non-essential overlays that don't affect core page content.

  <a name="tips-common-issues"></a><a name="9.4"></a>
  - [9.4](#tips-common-issues) Common issues and fixes
  
    | Issue | Likely cause | Fix |
    |-------|--------------|-----|
    | High LCP | Large hero image | Optimize image, add preload, use fetchpriority |
    | High CLS | Images without dimensions | Add width/height attributes |
    | High TBT | Heavy JavaScript | Code split, defer non-critical scripts |
    | Slow TTFB | Server response time | Use CDN, optimize backend |
    | Render blocking | CSS/JS in head | Inline critical CSS, defer scripts |
