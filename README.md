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
## 根据评分显示星星
```bash
  #html
  <div class="star-wrapper">
     <star :size="48" :score="seller.score"></star>
  </div>

  #抽出一个组件
  <template>
  <div class="star" :class="starType">
    <span v-for="(itemClass,index) in itemClasses" :class="itemClass" class="star-item" key="index"></span>
  </div>
  </template>

  <script type="text/ecmascript-6">
  const LENGTH = 5;
  const CLS_ON = 'on';
  const CLS_HALF = 'half';
  const CLS_OFF = 'off';

  export default {
    props: {
      size: {
        type: Number
      },
      score: {
        type: Number
      }
    },
    computed: {
      starType() {
        return 'star-' + this.size;
      },
      itemClasses() {
        let result = [];
        let score = Math.floor(this.score * 2) / 2;
        let hasDecimal = score % 1 !== 0;
        let integer = Math.floor(score);
        for (let i = 0; i < integer; i++) {
          result.push(CLS_ON);
        }
        if (hasDecimal) {
          result.push(CLS_HALF);
        }
        while (result.length < LENGTH) {
          result.push(CLS_OFF);
        }
        return result;
      }
    }
  };
  </script>

  <style lang="stylus" rel="stylesheet/stylus">
  @import "../../common/stylus/mixin.styl"

  .star
    font-size: 0
    .star-item
      display: inline-block
      background-repeat: no-repeat
    &.star-48
      .star-item
        width: 20px
        height: 20px
        margin-right: 22px
        background-size: 20px 20px
        &:last-child
          margin-right: 0
        &.on
          bg-image('star48_on')
        &.half
          bg-image('star48_half')
        &.off
          bg-image('star48_off')
    &.star-36
      .star-item
        width: 15px
        height: 15px
        margin-right: 6px
        background-size: 15px 15px
        &:last-child
          margin-right: 0
        &.on
          bg-image('star36_on')
        &.half
          bg-image('star36_half')
        &.off
          bg-image('star36_off')
    &.star-24
      .star-item
        width: 10px
        height: 10px
        margin-right: 3px
        background-size: 10px 10px
        &:last-child
          margin-right: 0
        &.on
          bg-image('star24_on')
        &.half
          bg-image('star24_half')
        &.off
          bg-image('star24_off')
</style>
```
