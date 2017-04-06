<template>
  <div id="app">
    <v-header></v-header>
    <div class="tab">
      <div class="tab-itme">商品</div>
      <div class="tab-itme">评论</div>
      <div class="tab-itme">商家</div>
    </div>
    <div id="content">
      I am content
    </div>
  </div>
</template>

<script type="text/ecmascript-6">
  import header from './components/header/header.vue';
  export default {
    components: {
      'v-header': header
    }
  };
</script>

<style lang="stylus" rel="stylesheet/stylus">
    #app
      .tab
        display: flex
        width: 100%
        height: 40px
        line-height: 40px;
        .tab-itme
            flex: 1
            text-align: center

</style>
