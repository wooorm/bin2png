# bin2png
Embed binary data inside an HTML file in an efficient way.

[![Netlify Status](https://api.netlify.com/api/v1/badges/7f568d67-7de0-45c8-b308-f6f84261f884/deploy-status)](https://app.netlify.com/sites/bin2png-example/deploys)

## How to use

You can see a full example of how to use `bin2png` and `png2bin` with an external build tool (in this case, parcel) in the [`example/`](./example/) folder. 

### Step 1: convert your binary files to png

Install **bin2png** in your dev dependencies (you only need it to build your html file):
```
npm install --save-dev bin2png
```

#### Use the CLI tool

You can use the [bin2png](https://www.npmjs.com/package/bin2png) CLI tool that is provided with the npm package:

```
npx bin2png file.bin encoded.png
```

#### Use the API
From a build script, you can use:

```js
const bin2png = require("bin2png").bin2png;

// bin2png takes an Uint8Array and returns another Uint8Array
const pngData = await bin2png(binaryData);
```


### Step 2: Use the png file


Add **png2bin** to your normal dependencies:

```
npm install png2bin
```

Then use the `png2bin` function from the package to decode the image:

#### In your HTML
```html
<img id="myfile"
    decoding="async" loading="eager"
    style="display:none"
    src="data:image/png;base64,..." />
```

#### In you JavaScript
```js
import { png2bin } from "png2bin";
const img = document.getElementById("myfile");
const mydata = await png2bin(img);
// mydata is now an Uint8Array with the contents of the original file
```
