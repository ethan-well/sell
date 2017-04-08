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

## Sticky footers布局
```bash
  # html结构
  <div class="detail" v-if="detailShow">
      <div class="detail-wrapper clearfix">
        <div class="detail-main">
        </div>
      </div>
      <div class="detail-close" @click="hideDetail">
        <i class="icon-close"></i>
      </div>
    </div>

  #清除fix
  .clearfix
  display: inline-block
  &:after
    display: block
    content: "."
    height: 0
    line-height: 0
    clear: both
    visibility: hidden

  # 图层样式
  .detail
      position: fixed
      top: 0
      left: 0
      z-index: 100
      width: 100%
      height: 100%
      overflow: auto
      background-color: rgba(7, 17, 27, 0.8)
      backdrop-filter: blur(10px)
      .detail-wrapper
        width: 100%
        min-height: 100%
        .detail-main
          margin-top: 64px
          padding-bottom: 64px
      .detail-close
        position: relative
        width: 32px
        height: 32px
        margin: -64px auto 0 auto
        clear: both
        font-size: 32px
```
