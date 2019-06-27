<template lang="pug">

  .count_down
    .circle_wrap
      svg
        circle.circle.circle--base(
          r="140"
          cx="150"
          cy="150"
        )
        circle.circle.circle--animation(
          ref="circle"
          :stroke-dasharray="counter.dasharray"
          :stroke-dashoffset="counter.dashoffset"
          r="140"
          cx="150"
          cy="150"
        )
    p.counter(v-show="!!counter.timeCounter") {{ counter.timeCounter }}
    p.counter.counter--timeup(v-show="!counter.timeCounter")
      span T
      span I
      span M
      span E
      span U
      span P
  button(@click="start") START
</template>

<style lang="sass" scoped>

#app {
  min-height: 100%
  display: flex
  justify-content: center
  align-items: center
  flex-direction: column
  font-family: sans-serif
}

.count_down {
  position: relative
  display: flex
  justify-content: center
  align-items: center
  width: 300px
  height: 300px

  .circle_wrap {
    position: absolute
    top: 0
    left: 0
    width: 100%
    height: 100%
    transform: rotate(-90deg)
    
 
  svg
    position: absolute
    top: 0
    left: 0
    width: 100%
    height: 100%
    
    .circle
      fill: transparent
      stroke-width: 18
      
      &--base
        stroke: #ddd
      
      &--animation
        stroke: #000
        
  .counter
    font-size: 128px
    font-weight: bold
    
    &--timeup
      font-size: 32px
      
      span
        display: inline-block

button
  margin-top: 40px
</style>
