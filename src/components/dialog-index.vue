<template>
  <div class="layer" v-if="show" @touchmove.stop="preventD">
    <div class="dialog">
      <div class="dialog-content">
        <h4 class="dialog-content-title">使用说明</h4>
        <div class="dialog-content-detail">
          <p><span>拼工作餐</span>小程序终于和大家见面啦，大家在第一次使用的时候肯定会有很多疑问，它到底应该怎么用呢？</p>
          <ul>
            <li>1. 拷贝<span>可选的订餐信息</span>，<span>订餐方式</span>。</li>
            <li>2. 把支付二维码<span>截图并上传</span>。</li>
            <li>3. 把拼单<span>分享到群</span>。</li>
            <li>4. 小伙伴可以<span>点击进入参与拼饭</span>。</li>
          </ul>
          <p>请授权后开始使用</p>
        </div>
      </div>
      <button open-type="getUserInfo" lang="zh_CN" @getuserinfo="onGotUserInfo">授权</button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    show: {
      type: Boolean,
      default: false
    }
  },
  watch: {
    show (val) {
      val ? this.$emit('onShow') : this.$emit('onHide')
    }
  },
  methods: {
    preventD () {},
    hideDialog () {
      this.$emit('update:show', false)
    },
    onGotUserInfo() {
      this.hideDialog();
    }
  }
}
</script>

<style lang="less">
.layer {
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  background: rgba(0, 0, 0, .5);
  z-index: 100;
  .dialog {
    position: fixed;
    height: 100vh;
    left: 50rpx;
    right: 50rpx;
    z-index: 200;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    &-content {
      background: #fff;
      width: 100%;
      max-width: 650rpx;
      margin-bottom: 60rpx;
      border-radius: 8rpx;
      &-title {
        text-align: center;
        padding: 33rpx 0;
        font-size: 34rpx;
        color: #333;
        border-bottom: 1rpx solid #e6ebf0;
      }
      &-detail {
        padding: 40rpx 50rpx;
        color: #333;
        font-size: 28rpx;
        span {
          color: rgb(255, 142, 2);
        }
        p {
          margin-bottom: 30rpx;
        }
        ul {
          margin-bottom: 30rpx;
          li {
            margin-bottom: 15rpx;
          }
        }
      }
    }
  }
}
</style>
