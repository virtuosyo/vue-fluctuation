<template>
  <div id="app">
    <div class="container">
      <div class="introduce">
        <h1>vue-fluctuation</h1>
        <div>
          <a href="https://github.com/Yanggoing/vue-fluctuation">
            <svg xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink"
                 width="126" height="20">
              <linearGradient id="s" x2="0" y2="100%">
                <stop offset="0" stop-color="#bbb" stop-opacity=".1"/>
                <stop offset="1" stop-opacity=".1"/>
              </linearGradient>
              <clipPath id="r">
                <rect width="126" height="20" rx="3" fill="#fff"/>
              </clipPath>
              <g clip-path="url(#r)">
                <rect width="47" height="20" fill="#555"/>
                <rect x="47" width="79" height="20" fill="#97ca00"/>
                <rect width="126" height="20" fill="url(#s)"/>
              </g>
              <g fill="#fff" text-anchor="middle"
                 font-family="Verdana,Geneva,DejaVu Sans,sans-serif"
                 text-rendering="geometricPrecision" font-size="110">
                <text x="245" y="150" fill="#010101" fill-opacity=".3" transform="scale(.1)"
                      textLength="370">Github
                </text>
                <text x="245" y="140" transform="scale(.1)" textLength="370">Github</text>
                <text x="855" y="150" fill="#010101" fill-opacity=".3" transform="scale(.1)"
                      textLength="690">@Yanggoing
                </text>
                <text x="855" y="140" transform="scale(.1)" textLength="690">@Yanggoing</text>
              </g>
            </svg>
          </a>
        </div>
        <p>一个基于vue&vue-digital-transform的数值波动效果组件</p>
      </div>
      <p>
        二次封装了vue-digital-transform这个组件，增加了数值变动时的增减动画效果，在一些需要实时监测数据波动并展示的场景下可以使用，组件还有一些不完美的地方需要改进，支持的话，帮我点个Star吧！
      </p>
      <h2>体验Demo</h2>
      <div class="demo-box">
        <span class="type-box">基本数值样式</span>
        <span class="random-btn" @click="randomClick">摇摇乐</span>
        <label>
          <input type="text"
                 placeholder="这里修改单位"
                 v-model.trim.lazy="ordUnit"
          >
        </label>
        <div class="show-box">
          <fluctuation :value="testValue"
                       :seperator="false"
                       :unit="ordUnit"
                       :interval="500"
          >
            <template>
              <i class="iconfont icon-data"></i>
            </template>
          </fluctuation>
        </div>
      </div>
      <div class="demo-box">
        <span class="type-box">千分位符样式</span>
        <span class="random-btn" @click="randomSepClick">摇摇乐</span>
        <div class="show-box">
          <fluctuation
            :value="testMoney"
            seperator
            :unit="moneyUnit"
          >
            <template>
              <i class="iconfont icon-data"></i>
            </template>
          </fluctuation>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Fluctuation from '@/components/Fluctuation';

export default {
  name: 'App',
  components: {
    Fluctuation,
  },
  data() {
    return {
      testValue: 666666,
      testMoney: 10000000,
      ordUnit: '',
      moneyUnit: '元',
    };
  },
  methods: {
    randomClick() {
      this.testValue = Math.floor(Math.random() * (666666 - 1 + 1) + 1);
    },
    randomSepClick() {
      this.testMoney = Math.floor(Math.random() * (10000000 - 1 + 1) + 1);
    },
  },

};
</script>

<style lang="stylus">
  @keyframes shake
    10%, 90%
      transform translate3d(-1px, 0, 0)
    20%, 80%
      transform translate3d(2px, 0, 0)
    30%, 50%, 70%
      transform translate3d(-4px, 0, 0)
    40%, 60%
      transform translate3d(4px, 0, 0)

  .container
    width 800px
    margin auto

    .introduce
      text-align center

    .demo-box
      display flex
      align-items center
      margin-top 20px
      padding: 20px
      box-shadow: 0 0 11px 0 rgba(0, 0, 0, 0.12)
      border-radius: 4px

      .show-box
        display flex
        align-items center
        width max-content
        height 32px
        padding-right 20px
        border-radius 8px
        background #F8F8F8FF

      label
        display flex
        align-items center
        width 100px
        height 30px
        padding-left 10px
        padding-right 5px
        border-radius 15px
        margin-right 20px
        background-color: #eee;

        span
          margin-right 10px

        input
          width 100px
          height 16px
          background none
          outline none
          border none

      .type-box
        width 100px
        height 30px
        padding 0 5px
        margin-right 20px
        border-radius 4px
        text-align center
        line-height 30px
        border: 1px solid rgba(255, 229, 143, 1)
        background rgba(247, 181, 0, 1)

      .random-btn
        width 100px
        height 30px
        margin-right 30px
        border-radius 15px
        line-height 30px
        text-align center
        color #ffffff
        background-color #6A83DAFF

      .random-btn:hover
        animation shake 0.82s cubic-bezier(.36, .07, .19, .97) both

</style>
