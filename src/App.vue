<template lang="pug">
div.page
  .page-con
    .page-con-left
      .page-con-left-logo(
        :style="{'background-color': mainColor}"
      )
      p.page-con-left-title True Wallet 钱包下载 
        span.en / Download
      p.page-con-left-title-intr(v-html="text")
      img(:src="require(`@/assets/images/wallet${version ? '_' + version : ''}.png`)").bj
    .page-con-right
      a.down-btn(
        v-if="ua !== 'ios'"
        href="https://qiniu.truescan.net/file/true.apk",
        :style="{'background-color': mainColor}"
        @click="onDownAndroid"
      )
        img(src="~@/assets/android.svg")
        span.color_f Android版本下载 
          span.en / Download
      a.down-btn(
        v-if="ua !== 'android'"
        target="_blank",
        href="https://testflight.apple.com/join/bwvKiO5a",
        :style="{'background-color': mainColor}"
        @click="onDownIos"
      )
        img(src="~@/assets/ios.svg")
        span.color_f iPhone版本下载 
          span.en / Download
    p.coy Copyright ⓒ TRUECHAIN FOUNDATION LTD. All Rights Reserved.
</template>

<script>
const colors = {
  '214': '#f97873'
}
const texts = {
  '214': '初链红包，支持TRUE、ETH收发红包'
}

export default {
  name: 'app',
  data () {
    return {
      version: '',
      mainColor: '#0071BC',
      text: '简单、安全、有趣的区块链钱包<br>Simple, Safe and Interesting Blockchain Wallet',
      ua: ''
    }
  },
  created () {
    const reg = /(\?|&)v=([^&]*)(&|$)/
    const res = location.search.match(reg)
    if (res && res[2]) {
      this.version = res[2]
      this.mainColor = colors[this.version] || '#0071BC'
      this.text = texts[this.version] || '简单、安全、有趣的区块链钱包<br>Simple, Safe and Interesting Blockchain Wallet'
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
      line-height 1.2em
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
    margin 0 auto 15px
    border-radius 15px
    background-image url(assets/images/logo.png)
    background-size contain
    background-repeat no-repeat
.coy
  position absolute
  bottom 20px
  font-size 12px
  color rgba(32,50,96,1)
.en
  display inline!important
  opacity .7
</style>
