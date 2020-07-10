<!--suppress PointlessBooleanExpressionJS -->
<template>
  <div class="fluctuating-container">
    <div class="data-container">
      <i class="iconfont icon-data"></i>
      <digital-transform :value="value" :useGrouping="seperator"
                         :interval="interval"></digital-transform>
      <span>{{unit}}</span>
    </div>
    <transition name="lotus">
      <p class="fluctuating-animate" v-show="isShow">{{changeValue}}</p>
    </transition>
  </div>
</template>

<script>
import DigitalTransform from '@/components/DigitalTransform';

export default {
  name: 'Fluctuation',
  components: {
    DigitalTransform,
  },
  props: {
    value: {
      type: Number,
      default: 0,
      required: true,
    },
    unit: {
      type: String,
      default: '',
    },
    seperator: {
      type: Boolean,
      default: false,
    },
    interval: {
      type: Number,
      default: 500,
    },
  },
  data() {
    return {
      isShow: false,
      animatingTimer: null,
      changeValue: 0,
    };
  },
  watch: {
    value: {
      handler(newVal, oldVal) {
        this.changeValue = this.isPlus(newVal - oldVal, this.seperator);
        this.digitalDebounce();
      },
    },
  },
  methods: {
    // 数值变动动画效果防抖函数
    digitalDebounce() {
      if (this.animatingTimer) {
        clearTimeout(this.animatingTimer);
      }
      this.isShow = true;
      this.animatingTimer = setTimeout(() => {
        this.isShow = false;
        this.animatingTimer = null;
      }, 1500);
    },
    // 判断值是否为增长值 为其填上加号
    isPlus(testVal, isSep) {
      // 判断是否为带有千分位符选项
      if (isSep) {
        const changeStr = testVal.toString().replace(/^-?\d+/g, (m) => m.replace(/(?=(?!\b)(\d{3})+$)/g, ','));
        const result = changeStr.split('').join('');
        const first = changeStr.split('')[0];
        if (first.match(/^[0-9]$/)) {
          return `+${result}`;
        }
        return result;
      }
      if (testVal > 0) {
        return `+${testVal}`;
      }
      return testVal;
    },
  },
  destroy() {
    clearTimeout(this.animatingTimer);
  },
};
</script>

<style lang="stylus" scoped>
  .lotus-enter
    transform translateY(20px)
    opacity 0

  .lotus-enter-active
    transition all 0.5s cubic-bezier(1, 0.5, 0.8, 1)

  .lotus-leave-active
    opacity 0
    transition all 1s

  .fluctuating-container
    position relative
    display flex
    align-items center
    width max-content
    height 32px
    border-radius 8px
    background #F8F8F8FF

    .fluctuating-animate
      position absolute
      left 36%
      top -32px
      text-align center
      font-family 'Arial-BoldItalicMT', 'Arial Bold Italic', 'Arial'
      font-weight 700
      font-style italic
      font-size 18px
      color limegreen

    .data-container
      font-size 16px
      font-family SFProRounded-Bold, SFProRounded
      font-weight bold
      color rgba(0, 0, 0, 0.85)
      line-height 19px

      i
        margin-left 8px
        margin-right 18px
        font-size 22px
        color #6A83DAFF

      span
        margin-left 6px
        margin-right 34px
        line-height 19px
</style>
