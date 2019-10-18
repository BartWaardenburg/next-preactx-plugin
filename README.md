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