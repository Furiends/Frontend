<template>
  <view class="up_img_wrap">
    <image :src="src"></image>
    <icon type="clear" size="23" color="red"></icon>
  </view>
</template>

<script>
export default {
  name: 'imagesUpload',
  props: {
    src: {
      type: String,
      default: '',
    },
  },
};
</script>

<style>
.up_img_wrap {
  width: 90rpx;
  height: 90rpx;
  position: relative;
}
.up_img_wrap image {
  width: 100%;
  height: 100%;
  border-radius: 15rpx;
}
.up_img_wrap icon {
  position: absolute;
  right: -5rpx;
}
</style>
