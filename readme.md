# Bs-Harp-Dw

Bs-Harp + DreamWeaver Templates/Libraries

Bs-Harp内にDreamWeaverのTemplates/Librariesを埋め込む

## Install

### 1. Node.js

[Node.js](http://nodejs.org/)

### 2. Harp

[Harp](http://harpjs.com/) - the static web server with built-in preprocessing
```
$ sudo npm install -g harp
```

### 3. Download Bs-Harp or git clone Bs-Harp

### 4. Install some node-module
```
$ npm install
```

## Usage

### Start using LiveReload

Start http://localhost:9000

```
$ harp server
```

and start proxying: http://localhost:9000 and http://localhost:3000

```
$ npm start
```

### Write the code to jade files

When you write the code to jade files , there is a need to write root path.

```index.jade
img(src="/images/demo.png", alt="demo")
```

### Finish using LiveReload

control + c

### Compile source

Compile source non-minify-html in /dist

If you don't need to convert relative path to the dist directory, you change config.relativePath to false in gulpfile.js.

```
$ harp compile;gulp clean:dist;gulp dist;gulp dw;gulp clean:distTem
```

## DreamWeaver Templates/Libraries Settings

### Files for DreamWeaver Templates/Libraries when bs-harp-dw install

1. DreamWeaver Template File `/public/Templates/layout.jade`

use Harp's Layout(a common template) `/public/_layout.jade`

```_layout.jade
include _mixins
doctype
html(lang="en")
	if templateName
		<!-- InstanceBegin template="/Templates/#{templateName}.dwt" codeOutsideHTMLIsLocked="false" -->
	head
		meta(charset="utf-8")
		+dwcStart("doctitle")
		title= title
		+dwcEnd
		+dwcStart("head")
		meta(name="keywords" content="#{keywords}")
		meta(name="description" content="#{description}")
		+dwcEnd
		link(rel="stylesheet" href="/css/main.css")
	body
		block main
			!= partial("_header")
		+dwcStart("contents")
		!= yield
		+dwcEnd
		script(src="/js/jquery.min.js")
		script(src="/js/bootstrap.min.js")
		script(src="/js/custom.js")
	if templateName
		<!-- InstanceEnd -->
```

2. add DreamWeaver Template Editable Area

```
+dwcStart("contents") // Editable Area Name
...
+dwcEnd
```

3. DreamWeaver Library File `/public/Library/header.jade`

use Harp's Partial `/public/Library/_header.jade`

```_header.jade
include _mixins
+dwLibStart("header") // Library Name
.navbar.navbar-inverse.navbar-fixed-top(role="navigation")
	...
+dwLibEnd
```

### How to include DreamWeaver Templates/Libraries in jade files

1. use jade mixins（`/public/_mixins.jade`）in these files
	- `include _mixins`

2. add `title`,`keywords`,`description` and `templateName` in each `_data.json` files

`templateName` is using DreamWeaver Template File's name.

```_data.jade
{
  "index": {
    "title": "Home",
    "keywords": "keywords sample Home",
    "description": "keywords sample Home",
    "templateName": "layout"
  },...
```

3. add DreamWeaver Library

create Harp's Partial , wrap with the following code , and add jade file in Libraries directory with Library Name.

```
include _mixins
+dwLibStart("header") // Library Name
...
+dwLibEnd
```

## Change Log
### v.1.0.0 (2015.7)
Bs-Harp v.1.2.0から作成
