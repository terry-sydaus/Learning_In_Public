---
title: "npm live-server not working as epxected"
date: 2019-09-27
---
I discovered today that npm's live-server will not work properly, ie. will not serve up the page to my local host when you make changes in the source files, unless the structure of the index.html file contains the opening and closing html and body tags.

Examples that will work:

````html
<html>
  <body>
    <div>hello world</div>
  </body>
</html>
````

````html
<body>
  <div>hello world</div>
</body>
````

Examples that will *not* work:

````html
<div>hello world</div>
````

This might be obvious, like most things are once you find out how to fix them, but I have included this observation in this blog post as a means to capture and document my findings so that I remember the next time.
