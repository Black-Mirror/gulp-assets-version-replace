# gulp-assets-version-replace  [![Build Status](https://travis-ci.org/bammoo/gulp-assets-version-replace.svg?branch=master)](https://travis-ci.org/bammoo/gulp-assets-version-replace) [![npm version](https://badge.fury.io/js/gulp-assets-version-replace.svg)](http://badge.fury.io/js/gulp-assets-version-replace)

[Grunt version is here](https://github.com/bammoo/grunt-assets-version-replace)

[中文文档](README-cn.md)


> Gulp plugin for managing version of assets, easy to build new version to commit and deploy.


## Features

- Generate new file for js,css etc. based on md5 of file contents
- Create new version only for changed assets
- Auto replace versioned assets in template files, like php, python Django, Expressjs ejs and etc.
  

## Example


#### 1. File structure

**Assets structure：**
 
```
js_build/app.js
css_build/webapp.css
```
*Files under js_build and css_build are generated by compass uglify*

**Links in templates：**

```html
<link href="static/dist/css_build/webapp.__placeholder__.css" />
```

*Note:  `__placeholder__` is a placeholder when it's not auto versioned before*

#### 2. Configs in gulpfile.js：

```js
gulp.task('assetsVersionReplace', function () {
    assetsVersionReplace({
      tsFiles: ['test/css_build/*.css', 'test/js_build/*.js'],
      tsVersionedFilesDest: 'test/dist/',
      replaceTemplateList: [
        'test/header.php',
        'test/footer.php',
        'test/submodule/header.php'
      ]
    })
});
```
#### 3. Run gulp task

`gulp assetsVersionReplace` in your terminal.

Your get these result:

* **Files named with generated version** 

```
dest/js_build/app.c7ccb6b8ce569a65ed09d4256e89ec30.js
dest/css_build/webapp.2af81cda4dacbd5d5294539474076aae.css
```

* **Links in templates have been replaced with generated version**

```html
<link href="static/dist/css_build/webapp.2af81cda4dacbd5d5294539474076aae.css" />
```

#### 4. Commit or config more

You can commit the result of prev step directly if you are deployoing a static site.


## Install

```shell
npm install gulp-assets-version-replace --save-dev
```

In your gulpfile.js place this line:

```js
var assetsVersionReplace = require('gulp-assets-version-replace');
```

A dot file called `gulp-assets-version-replace-version.json` will be created beside your gulpfile.js to serve as a json store. **Please ignore it in your .gitignore or .hgignore etc.**

Form asset link as following in your template:

```html
<!doctype html>
<html>
<head>
  <meta charset="utf-8" />
  <title>test</title>
  <link href="static/dist/css_build/app.__placeholder__.css" />
  <link href="static/dist/css_build/desktop.__placeholder__.css" />
</head>
<body>
```

**Notes:** 
`__placeholder__` is a placeholder for replacing with generated versions at first time


## Gulp Plugin Options

#### options.tsFiles

Array of globs. Files which will be copied to a new folder and named with gerenated version.

Type: `Array`
Default value: `[]`


#### options.tsVersionedFilesDest

The destination folder place the result files.

Type: `Array`
Default value: `[]`


#### options.replaceTemplateList

List of templates which contain assets links of `tsFiles` . Support whatever extension like php, python Django, Express and etc.


Type: `Array`
Default value: `[]`


## Release History

* 2015-12-15   v1.0.0   Refactor code, add feature of version store and compare
* 2015-12-13   v0.1.2   Update github repo link
* 2015-12-13   v0.1.1   Update doc
* 2015-07-31   v0.1.0   Initial commit


