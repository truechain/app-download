<template lang="pug">
div.page
  .page-con
    .page-con-left
      img(src="~@/assets/images/logo_blue.png").page-con-left-logo
      p.page-con-left-title TrueChain钱包
      p.page-con-left-title-intr 简单、安全、有趣的区块链钱包
      img(src="~@/assets/images/wallet.png").bj
    .page-con-right
      a.down-btn(
        v-if="ua !== 'ios'"
        target="_blank",
        href="https://qiniu.truescan.net/file/true.apk",
        @click="onDownAndroid"
      )
        img(src="~@/assets/android.svg")
        span.color_f Android版本下载
      a.down-btn(
        v-if="ua !== 'android'"
        target="_blank",
        href="itms-services://?action=download-manifest&url=https://qiniu.truescan.net/file/true-wallet.plist",
        @click="onDownIos"
      )
        img(src="~@/assets/ios.svg")
        span.color_f iPhone版本下载
    p.coy Copyright ⓒ TrueChain All Rights Reserved.
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      ua: ''
    }
  },
  mounted() {
    const u = navigator.userAgent
    const isAndroid = u.indexOf('Android') > -1 || u.indexOf('Adr') > -1
    const isiOS = !!u.match(/\(i[^;]+;( U;)? CPU.+Mac OS X/)
    if (isAndroid && !isiOS) {
      this.ua = 'android'
    } else if (isiOS && !isAndroid) {
      this.ua = 'ios'
    }
  },
  methods: {
    onDownIos () {
      window._hmt.push(['_trackEvent', 'software', 'download', 'iosh5down'])
    },
    onDownAndroid (e) {
      var isWeixinBrowser = (/micromessenger/i).test(navigator.userAgent);
      if(isWeixinBrowser){
        e.preventDefault()
        alert('点击右上角，选择在浏览器中打开')
      }
      window._hmt.push(['_trackEvent', 'software', 'download', 'androidh5down']);
    }
  },
}
</script>

<style lang="stylus">
body
  margin 0
  padding 0
  font-family PingFang SC, Microsoft Yahei, Hiragino Sans GB, NotoSansCJKsc, Helvetica Neue, Roboto
p
  margin 0
.page
  position relative
  background-color #fff
  padding-top 50px
  min-height 100vh
  box-sizing border-box
  .page-con
    flex-direction column
    align-items center
    display flex
    justify-content space-between
    max-width 820px
    margin 0px auto
  .page-con-left
    width 80%
    text-align center
  .page-con-left-title
    display block
    margin-bottom 10px
  .page-con-left-title-intr
      color #808590
      font-size 12px
      font-weight 500
      line-height 1.2
      margin-bottom 30px
    .bj
      max-width 100%
      max-height 40vh
  .page-con-right
    padding 20px 0
    display flex
    height 180px
    flex-direction column
    justify-content center
    .down-btn
      display flex
      align-items center
      justify-content center
      background-color #0071BC
      width 300px
      border-radius 8px
      margin 20px 0px
      line-height 30px
      height 50px
      text-decoration none
      img
        margin-right 10px
      span
        color #fff
        font-size 15px
        line-height 30px
        display block
  .page-con-left-logo
    width 80px
    height 80px
    margin-bottom 10px
.coy
  position absolute
  bottom 20px
  font-size 12px
  color rgba(32,50,96,1)
</style>
