# sell

> A Vue.js project

## Build Setup

``` bash
# install dependencies
npm install -g

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

```

## 模拟后台数据核心代码
``` bash
  #1 ./build/dev-server.js
  var app = express()

  var appData = require('../data.json')
  var seller = appData.seller
  var goods = appData.goods
  var ratings = appData.ratings

  var apiRoutes = express.Router()

  apiRoutes.get('/seller', function (req, res) {
    res.json({
      errno: 0,
      data: seller
    });
  })

  apiRoutes.get('/goods', function (req, res) {
    res.json({
      errno: 0,
      data: goods
    })
  })

  apiRoutes.get('/ratings', function (req, res) {
    res.json({
      errno: 0,
      data: ratings
    });
  })

  app.use('/api', apiRoutes)

  #2 添加数据文件data.json
```
