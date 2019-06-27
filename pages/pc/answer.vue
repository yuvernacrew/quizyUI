<template lang='pug'>

section.container.foundation 
  .container__card
    .container__inner
      .question
        p 坊主なヒューマンビートボックスな人は誰？
      .rerults
        .rerult.rerult--1.is-active
          p.label コツコツ貯めたホットペッパーポイント１万円分が消失
          p.graph(:style="{width: `${Result01.graphWidth}px`}")
          p.percent {{`${Result01.percent}%`}}
        .rerult.rerult--2
          p.label コツコツ貯めたホットペッパーポイント１万円分が消失
          p.graph(:style="{width: `${Result02.graphWidth}px`}")
           p.percent {{`${Result02.percent}%`}}
        .rerult.rerult--3
          p.label コツコツ貯めたホットペッパーポイント１万円分が消失        
          p.graph(:style="{width: `${Result03.graphWidth}px`}")
          p.percent {{`${Result03.percent}%`}}
      button(@click="start") start

  </template>

<script>
import { TweenMax, Back, Power0 } from 'gsap';
export default {
  data() {
    return {
      graph: {
        progress: 0,
        maxGraphWidth: 600,
        Percent01: 1,
        Percent02: 0.12,
        Percent03: 0.12
      },
      question: {
        statement: "坊主なヒューマンビートボックスな人は誰？"
      },
      questionAnswers: [
        {
          id: 1,
          statement: "コツコツ貯めたホットペッパーポイント１万円分が消失"
        },
        {
          id: 2,
          statement: "コツコツ貯めたホットペッパーポイント１万円分が消失"
        },
        {
          id: 3,
          statement: "コツコツ貯めたホットペッパーポイント１万円分が消失"
        },
      ]
    }
  },
  computed: {
    Result01: function () {
      const Percent01 = !!this.graph.progress ? this.graph.Percent01 * this.graph.progress : 0
      const graphWidth = Math.floor(this.graph.maxGraphWidth * Percent01)
      const percent = Math.floor(100 * Percent01)
      return { graphWidth, percent }
    },
    Result02: function () {
      const Percent02 = !!this.graph.progress ? this.graph.Percent02 * this.graph.progress : 0
      const graphWidth = Math.floor(this.graph.maxGraphWidth * Percent02)
      const percent = Math.floor(100 * Percent02)
      return { graphWidth, percent }
    },
    Result03: function () {
      const Percent03 = !!this.graph.progress ? this.graph.Percent03 * this.graph.progress : 0
      const graphWidth = Math.floor(this.graph.maxGraphWidth * Percent03)
      const percent = Math.floor(100 * Percent03)
      return { graphWidth, percent }
    }
  },
  methods: {
    start() {
      this.graph.progress = 0
      TweenMax.to(this.graph, 1, { progress: 1 })
    }
  }
}

</script>

<style lang='sass'>
$primary-color: #FCC205;
$secondary-color: #FFF598;
$base-color: #FFFEE6; 
$text-main-color: #44443F;

.container 
  max-width: none
  width: 100vw;
  height: 100vh;
  padding: 40px;
  background-color: $primary-color;

  &__card 
    position: relative;
    background-color: $base-color;
    width: 100%;
    height: 100%;
    border-radius: 22px;
    box-shadow: 0 15px 20px rgba($color: #FCC205, $alpha: .75);

  &__inner 
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;

.question 
  font-size: 30px;
  margin-top: 40px;

.rerults
  position: absolute
  bottom: 0
  left: 40px
  height: 76vh;
  
.rerult
  position: absolute
  bottom: 0px
  height: 200px
  text-align: center
  font-weight: bold
  display: flex;
  align-items: center 
  
  .percent
    font-size: 24px
  
  .graph
    margin-right: 6px
    border-radius: 0 8px 8px 0;
    height: 100px;
    background-color: $primary-color
    
  .label
    margin-right: 36px;
    font-size: 16px;
    text-align: left
    width: 240px;
  
  &--1
    top: 0
      
  &--2
    top: 50%;
    transform: translateY(-50%)

  &--3
    bottom: 0

  &.is-active
    .graph
      background-color: #D1261E
    .percent
      color: #D1261E

</style>
