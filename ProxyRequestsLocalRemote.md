## Proxy Requests for Local and Remote Service Parity
We can use proxy middleware from `express` to request items from an external server the same way we might request items locally. Use the `express-http-proxy` client to do this.

```bash
yarn add express express http-proxy
```

```javascript
const path = require('path');
const express = require('express');
const proxy = require('express-http-proxy');
const baseImageUrl = process.env.BASE_IMAGE_URL;
const proxyBaseImageUrl = baseImageUrl
    ? proxy(baseImageUrl, {
        proxyReqPathResolver: function (req) {
            const newPath = baseImageUrl + req.path;
            console.log(newPath);
            return newPath;
        }
    })
    : express.static(path.join(__dirname, 'public/images'))

const app = express();
app.use('/images', proxyBaseImageUrl);
app.listen(8080);
```