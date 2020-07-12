# vue-fluctuation
一个基于vue&vue-digital-transform的数值波动效果组件
## Demo
[vue-fluctuation]("https://yanggoing.github.io/#/vue-fluctuation")

## Install
```
npm install vue-fluctuation
```

## Quick Start
```html
<template>
<fluctuation :value="value" 
             :seperator="isSep"
             :unit="unit"                       
             :interval="interval"
>
    <template>
        <i>可以选择插入以i标签包裹的icon</i>
    </template>
</fluctuation>
</template>
```
```js
import Fluctuation from "vue-fluctuation";

export default {
  components: {
    Fluctuation
  },
  data() {
    return {
      value: 666666,
      isSep: false,
      unit: '个',
      interval: 1000
    };
  }
};
```
## Slot
可以选择插入一个icon，以i标签包裹，自带默认样式
```vue
<fluctuation :value="value">
    <template>
        <i>可以选择插入以i标签包裹的icon</i>
    </template>
</fluctuation>
```

## Props

| prop                  | type          | description                                   | default   |
| --------------------- | ------------- | --------------------------------------------- | --------- |
| value                 | Number        | 需要监听数值波动的值                             | 0 |
| separator             | Boolean       | 是否开启千分位分隔符                             | false     |
| unit                  | String        | 数值单位，可以是任何你认为正确的单位                | ''        |
| interval              | Number        | 数字滚动过渡时间（ms）                            | 500       |
