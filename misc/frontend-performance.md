# A Guide to Auditing Front-end Performance

## 1. Asset size
* What is overall page size?
  - Don't worry. Even if your site _needs_ to load many large assets, they don't all have to count against page size.
  - Where possible, switch from libraries like jQuery and Bootstrap to native alternatives like document.querySelectorAll() and CSS-grid.
  - Consolidate use of frameworks & libraries (e.g. finish migrating from Backbone to React and enforce use of a single version) so you only have to load the latest version.
  - Enable gzip compression. It's easy, so do it!
* Are images optimized?
  - Manually optimize them.
  - Add an optimization step to your build.
  - Let a CDN do it all automatically.
* Are HTML, JS & CSS minified?
  - A simple build step.
* Is there unused JS & CSS?
  - Again, switching from libraries to native alternatives will help--you likely don't use the entire library, so why load it all?
  - Modern build tooling features like tree-shaking and code-splitting can help.
  - Split out code that is only needed for some scenarios (e.g. don't load CSS for both large and small devices if you'll only use one).
* Are some resources being loaded more than once?
  - This can be a complex issue to identify & solve, but proper configuration of frontend bundling can fix it and there are analysis tools to help.

## 2. Loading of assets
* Are assets being cached? If so, what's the caching strategy?
  - Employ maximum caching of all assets and cache busting via a fingerprinting step in the build that uses content hashes.
  - Group assets based on size & how frequently they change (e.g. separate external libraries that rarely change from your app's code which is likely to change often).
* Are critical assets being loaded first?
  - Make sure you're loading things in the correct order.
  - Preload or "defer" assets you know you'll need loaded.
* Are non-critical assets blocking page render?
  - Lazy load all non-critical (e.g. below-the-fold) images, JS, & CSS after page load.
* Is a CDN being used?
  - Fast, reliable delivery of content via smart networks of servers is what they do.

## 3. Number of requests & payload size
* Use HTTP/2
 - Updating your servers to HTTP/2 is usually simple and straightforward--no code changes needed.
* Bundle JS & CSS
  - Combine all scripts and stylesheets that you don't specifically want to cache separately.
* Eliminate duplicate requests by caching the response data
  - Wrap server calls in singletons.
  - Utilize session storage, local storage, and cookies.
  - Consider a client-side query tool like GraphQL with built in caching.
* Consolidate similar requests
	- Making a request for every item in a list? Try making one request with a list of IDs and returning a list instead.
	- Making 3 requests and combining the data from the responses? Consider exposing an endpoint which does that server side and requires only one client-side request.
* Eliminate unnecessary overhead from response payloads.
  - Either beef up your back end to be more tailored to what the front end needs
  - OR use something like GraphQL which allows the request to dictate the shape and size of the response.

## 4. Rendering and the big, bad DOM
There are 3 main things we ask of the browser:
1. make network requests
2. render HTML
3. run JavaScript calculations

JavaScript, like any modern programming language, can do simple calculations incredibly quickly, however JS is often used to interact with the DOM, which is less efficient and typically constitutes the vast majority of JS "scripting," or calculation time.

* Update your front-end framework & libraries.
  - All the major new FE frameworks now implement a virtual DOM to minimize actual DOM changes and rendering, while older frameworks such as AngularJS have not aged well in terms of performance.
* Server side rendering
  - Serving up HTML beyond a container div for your FE to inject into provides useful content to the user and reduces "Time to meaningful paint"
  - Modern FE frameworks almost all support what is known as isomorphic rendering, meaning you can use the same tech for server-side rendering that you use client-side. This makes such efforts much easier.
* Minimize the size of your DOM
  - Eliminate unnecessary markup like nested wrapper divs and spans
  - Avoid deeply nested structures
  - If you can't whittle your DOM down far enough, you can resort to buffering the DOM by loading things in and out of it as they enter and exit the viewport
* Avoid traversing the DOM as much as possible
  - Store references
  - Use IDs & document.getElementById()
* Take advantage of event delegation
  - This allows us to reduce the number of listeners we bind to the DOM
  - Avoid event.stopPropagation() where possible
* Throttle or debounce event handlers
  - Events like scroll and mousemove fire hundreds of times per second, but you almost never need to execute your listeners that often. Throttle will make sure they execute only once every X milliseconds, while debounce will defer execution until a condition is met (e.g. the user is done scrolling).
  - Many libraries have throttle & debounce utilities built in
  - Optimize listeners that fire repeatedly
* Don't neglect CSS!
  - Just because you're writing JS doesn't mean every solution should be done there. If you need to add styling, hide/show, or move/animate things, manage the classes and markup as needed with JS, but let CSS do the heavy lifting.
* Batch your DOM updates
  - Less communication between your JS & the DOM is better
  - Instead of swapping a section, hiding some things, then adding some details, is there a way you can do all of this at once?
  - This will result in less render cycles in the browser.
