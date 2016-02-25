# imagemin-giflossy

[![Build Status](http://img.shields.io/travis/jihchi/imagemin-giflossy.svg?style=flat)](https://travis-ci.org/jihchi/imagemin-giflossy)
[![Build status](https://ci.appveyor.com/api/projects/status/hdus9imkfyrlh5ls?svg=true)](https://ci.appveyor.com/project/jihchi/imagemin-giflossy)

> giflossy imagemin plugin


## Install

```
$ npm install --save imagemin-giflossy
```

## Usage

```js
var Imagemin = require('imagemin');
var imageminGiflossy = require('imagemin-giflossy');

new Imagemin()
	.src('images/*.gif')
	.dest('build/images')
	.use(imageminGiflossy({lossy: 80}))
	.run();
```

You can also use this plugin with [gulp](http://gulpjs.com):

```js
var gulp = require('gulp');
var imageminGiflossy = require('imagemin-giflossy');

gulp.task('default', function () {
	return gulp.src('images/*.gif')
		.pipe(imageminGiflossy({lossy: 80})())
		.pipe(gulp.dest('build/images'));
});
```


## API

### imageminGiflossy(options)

### options.interlaced

Type: `boolean`  
Default: `false`

Interlace gif for progressive rendering.

e.g.:
```js
imageminGiflossy({ interlaced: true });
```

### options.lossy

Type: `Number`  
Default: <None>

Order pixel patterns to create smaller GIFs at cost of artifacts and noise.

Adjust lossy argument to quality you want (30 is very light compression, 200 is heavy).

It works best when only little loss is introduced, and due to limitation of the compression algorithm very high loss levels won't give as much gain.

e.g.:
```js
imageminGiflossy({ lossy: 80 });
```

### options.resize

Type: `string`  
Default: `undefined`

Resize the output GIF to *widthxheight*.

e.g.:
```js
imageminGiflossy({ resize: '300x200' });
```

### options.noLogicalScreen

Type: `boolean`  
Default: `false`

Sets the output logical screen to the size of the largest output frame.

e.g.:
```js
imageminGiflossy({ noLogicalScreen: true });
```

### options.resizeMethod

Type: `string`  
Default: `mix`

Set the method used to resize images.

e.g.:
```js
imageminGiflossy({ resizeMethod: 'sample' });
```

### options.colors

Type: `number`  
Default: `undefined`

Reduce the number of distinct colors in each output GIF to *num* or less. *Num* must be between `2` and `256`.

e.g.:
```js
imageminGiflossy({ colors: 128 });
```

### options.colorMethod

Type: `string`  
Default: `diversity`

Determine how a smaller colormap is chosen.

e.g.:
```js
imageminGiflossy({ colorMethod: 'blend-diversity' });
```

### options.optimize

Type: `string`  
Default: `1`

Optimize output GIF animations for space.

There are currently three levels:
 * `1`: Stores only the changed portion of each image. This is the default.
 * `2`: Also uses transparency to shrink the file further.
 * `3`: Try several optimization methods (usually slower, sometimes better results).

Other optimization flags provide finer-grained control.

 * `keep-empty`: Preserve empty transparent frames (they are dropped by default).

e.g.:
```js
imageminGiflossy({ optimize: '3' });
```

### options.unoptimize

Type: `boolean`  
Default: `false`

Unoptimize GIF animations into an easy-to-edit form.

e.g.:
```js
imageminGiflossy({ unoptimize: true });
```

## License

MIT © [imagemin](https://github.com/imagemin)
