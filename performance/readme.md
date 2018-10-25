# Performance

Implement the best practices in performance.

Client makes a request to server and gets a HTML file. This file can have instructions to make more requests to load other content like images, CSS and Javascript files. Making more requests means taking more time to load and it directly affects users.

Performance improvements can be done in many distinct areas but there are three areas that can be highlighted.
1 - client side/front end
2 - network latency
3 - server side/back end

The best solution to optimise a website is to focus on the most significant bottle necks of a website. It means focusing on things present a great performance improvement

### Part 1 - Network Latency

##### Honey I shurnk the files

How to reduce the size of the files? Minimize text and minimize image. Uglify is an example of minimizing JS files to in order to shrink size but now this technique is commonly used in tools like web pack. Images is more complex because it depends on what is the propose of the image.

* JPG is used for photographs and images with many colors. No transparency allowed. It tends to be big in file size.
* GIF limited number of color usage and very good at animations
* PNG few sets of colors with transparency allowed
* SVG tend to be very simplistic and with good to show on retina monitors due to its characteristics.

TIPS:

* Reduce PNG with TinyPNG
* Reduce JPG with JPGOptimizer
* Try to use simple illustrations over high quality photo
* Always lower JPEG image quality (30% ~ 70%)
* Display different size images to different backgrounds.

Media queries is the solution to show different images depending on the display size.

```
@media screen and (min-width: 900px) {
  body {
    background: url('.large-background.jpg')
  }
}
@media screen and (max-width: 500px) {
  body {
    background: url('.small-background.jpg')
  }
}
```

* Use Content Delivery Networks - CDN

A content delivery network or content distribution network is a geographically distributed network of proxy servers and their data centers. The goal is to distribute service spatially relative to end-users to provide high availability and high performance. (Wiki)

* Remove photo metadata

Details from a picture such as what device the picture was taken, camera details and all information that you don't need to store in your images

##### The traveling delivery man

Reducing the number of page requests, the number of JS libries, look for native solutions over customizable resources.

##### Critical Render Path

DOM > CSSOM > Render Tree > Layout > Paint

Critical Render Path is the process of requesting HTML file from a server and rendering it on the screen. It is possible to optimize this process to load the webpage faster. Based on the HTML file, DOM creates a tree structure to each HMTL tag.

CSS and Javascript files take high priority compared to images. To improve this process CSS has to be delivered first and Javascript has to be delivered as late as possible. It means style tags at the top and script tags at the bottom.

- HTML
> Load style tag in the head
> Load script tag right before </body>
- CSS
> Load when the user needs that code. For example, scroll loading
> Use media attributes which are used to load according to device
> Don't use long chains of CSS specification
- JS
> Load scripts which are not essencial to user experience (changes DOM or CSS-DOM) asynchronously with tag `<script async>`
> Defer loading of scripts which aren't very important to the website `<script defer>`
> Minimize DOM manipulation is relevant due to critical render path. Once the browser starts downloading the javascript files, it has to check if there is any code to be executed. If it has, it stops to execute the code within the file and then it continues running.
> Avoid long running javascript because it sometimes blocks the page
