---
title: "npm live-server not working as epxected"
date: 2019-09-27
---
I discovered today that npm's live-server will not work properly, ie. will not serve up the page to a local host when you make changes in the source files, unless the structure of the index.html file contains the opening and closing html and body tags.

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

