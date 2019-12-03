# next-preactx-plugin

NextJS Plugin for PreactX. This will not be compatible with `preact` 8.4.x and is intended to be used with `preact`>10.0.0.

# Installation
```
yarn add next-preactx-plugin preact preact-ssr-prepass preact-render-to-string
```
Or if you're using NPM:
```
npm install --save next-preactx-plugin preact preact-ssr-prepass preact-render-to-string
```

Then install `react` and `react-dom` as devDependencies in your main project:
```
yarn add react react-dom -D
```
Or with NPM: 
```
npm install react react-dom -D
``` 

**The packages `react` and `react-dom` are required in order for NextJS to allow building and running only for the initial build step. Otherwise you will not be able to build your project**

# Usage

Create a `next.config.js` file in your project directory:
```
// next.config.js
const withPreact = require('next-preactx-plugin')
module.exports = withPreact({
  /* config options here */
})
```

Create a `server.js` file in your project directory:
```
// server.js
require('next-preactx-plugin/alias')()
const { createServer } = require('http')
const next = require('next')

const app = next({ dev: process.env.NODE_ENV !== 'production' })
const port = process.env.PORT || 3000
const handle = app.getRequestHandler()

app.prepare()
.then(() => {
  createServer(handle)
  .listen(port, () => {
    console.log(`> Ready on http://localhost:${port}`)
  })
})
```

Optionally you can add your custom Next.js configuration as parameter

```
// next.config.js
const withPreact = require('next-preactx-plugin')
module.exports = withPreact({
  webpack(config, options) {
    return config
  }
})
```

Make sure to change the "dev" script in your `package.json` to make use of the newly created `server.js` file (`node server.js` instead of `next dev`).

```
// package.json
  "scripts": {
    "dev": "node server.js"
  }
```
