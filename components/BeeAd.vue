<template>
  <div
    v-if="!removeAd"
    class="container">
    <div class="bee-ad">
      <div class="inner">
        <a @click="clickAd" />
        <span
          class="close"
          @click="removeAd = true">
          x
        </span>
      </div>
    </div>
  </div>
</template>

<script>
import BeeTranslator from '@/components/BeeTranslator'

export default {
  components: {
    BeeTranslator
  },
  props: {
    animate: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      removeAd: ''
    }
  },
  methods: {
    clickAd() {
      // window.location.href = 'https://telemet.org'
      window.open('https://telemet.org', '_blank')
      setTimeout(() => dataLayer.push({event: 'clickAd'}), 222)
    }
  }
}
</script>

<style scoped lang="scss">
.container {
  position: absolute;
  bottom: 80px;
  padding-top: 20px;
  padding-right: 35px;
  width: auto;
  right: 0;
  z-index: 1000;
  overflow: hidden;
}
.bee-ad {
  position: relative;
  // bottom: 80px;
  // right: 35px;
  z-index: 1000;
  // overflow: hidden;
  .inner {
    transform: translateX(150%);
    @include animation(
      fadeInAndOutAd,
      0.333s,
      1.333s,
      cubic-bezier(0, 0.33, 0.2, 1),
      1,
      forwards,
      forwards
    );
  }
  // transition: all 1s 2s cubic-bezier(0, 0.33, 0.2, 1);
  // &.animate {
  //   right: 35px;
  // }
}

a {
  display: block;
  width: 118px;
  height: 88px;
  font-size: $h6;
  font-weight: $bold;
  text-align: center;
  padding-top: 32px;
  margin: 0;
  color: lighten($white, 10);
  border: 2px solid $muted;
  background-image: url('/images/telemet-ad.jpg');
  border-radius: 2px;
  user-select: none;
  &:hover {
    border-color: $brand;
  }
}

span.close {
  position: absolute;
  top: -8px;
  right: -8px;
  line-height: 13px;
  width: 20px;
  height: 20px;
  border-radius: 50%;
  font-size: $h8;
  border: 2px solid $muted;
  font-weight: $bold;
  color: lighten($muted, 0);
  background: $background;
  cursor: pointer;
  user-select: none;
  &:hover {
    color: $brand;
    background: rgba($background, 100);
    border-color: $brand;
  }
}

@keyframes fadeInAndOutAd {
  0% {
    opacity: 0;
    transform: translateX(150%);
  }
  100% {
    opacity: 1;
    transform: translateX(0%);
  }
}
</style>
