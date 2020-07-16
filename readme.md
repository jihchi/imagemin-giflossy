# imagemin-giflossy
[![npm version](https://img.shields.io/npm/v/imagemin-giflossy.svg)](https://www.npmjs.com/package/imagemin-giflossy)
[![npm downloads](https://img.shields.io/npm/dm/imagemin-giflossy.svg)](https://www.npmjs.com/package/imagemin-giflossy)
[![Build Status](http://img.shields.io/travis/jihchi/imagemin-giflossy.svg?style=flat)](https://travis-ci.org/jihchi/imagemin-giflossy)
[![Build status](https://ci.appveyor.com/api/projects/status/hdus9imkfyrlh5ls?svg=true)](https://ci.appveyor.com/project/jihchi/imagemin-giflossy)

> giflossy imagemin plugin


## Install

```
$ npm install --save imagemin-giflossy
```

## Usage

```js
const imagemin = require('imagemin');
const imageminGiflossy = require('imagemin-giflossy');

imagemin(['images/*.gif'], 'build/images', {use: [imageminGiflossy({lossy: 80})]}).then(() => {
	console.log('Images optimized');
});
```


## API

### imageminGiflossy([options])(buffer)

Returns a promise for a buffer.

#### options

##### interlaced

Type: `boolean`<br>
Default: `false`

Interlace gif for progressive rendering.

##### optimizationLevel

Type: `number`<br>
Default: `1`

Select an optimization level between `1` and `3`.

> The optimization level determines how much optimization is done; higher levels take longer, but may have better results.

1. Stores only the changed portion of each image.
2. Also uses transparency to shrink the file further.
3. Try several optimization methods (usually slower, sometimes better results)

##### colors

Type: `number`

Reduce the number of distinct colors in each output GIF to num or less. Num must be between 2 and 256.

##### lossy

Type: `Number`  
Default: `undefined`

Order pixel patterns to create smaller GIFs at cost of artifacts and noise.

Adjust lossy argument to quality you want (30 is very light compression, 200 is heavy).

It works best when only little loss is introduced, and due to limitation of the compression algorithm very high loss levels won't give as much gain.

e.g.:
```js
imageminGiflossy({ lossy: 80 });
```

##### resize

Type: `string`  
Default: `undefined`

Resize the output GIF to *widthxheight*.

e.g.:
```js
imageminGiflossy({ resize: '300x200' });
```

##### noLogicalScreen

Type: `boolean`  
Default: `false`

Sets the output logical screen to the size of the largest output frame.

e.g.:
```js
imageminGiflossy({ noLogicalScreen: true });
```

##### resizeMethod

Type: `string`  
Default: `mix`

Set the method used to resize images.

e.g.:
```js
imageminGiflossy({ resizeMethod: 'sample' });
```

##### colorMethod

Type: `string`  
Default: `diversity`

Determine how a smaller colormap is chosen.

e.g.:
```js
imageminGiflossy({ colorMethod: 'blend-diversity' });
```

##### optimize

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

##### unoptimize

Type: `boolean`  
Default: `false`

Unoptimize GIF animations into an easy-to-edit form.

e.g.:
```js
imageminGiflossy({ unoptimize: true });
```

#### buffer

Type: `buffer`

Buffer to optimize.

## License

MIT © [Jih-Chi Lee](https://github.com/jihchi)
