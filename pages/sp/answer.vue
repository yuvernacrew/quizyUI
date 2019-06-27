<template lang="pug">
  section.container
    .container__inner
      section.userData
        p.userData__inner
          span.userData__text {{ user.name }} さんのポイント
          span.userData__text {{ user.point }}pt
      section.answer
        .correct(v-show='correct')
          img(src='~/assets/images/correct.png')
        .incorrect(v-show='!correct')
          img(src='~/assets/images/incorrect.png')

      p 正解は #[span.answer__text こにゃーーーー] です。
      .correct(v-show='correct')
        p #[span.answer-point__text 33pt] ゲット！！
</template>

<script>
export default {
  data() {
    return {
      correct: false,
      user: {
        name: 'ちーずかまぼこ',
        point: '227'
      },
    }
  }
}
</script>

<style lang="sass">

$primary-color: #FCC205;
$secondary-color: #FFF598;
$base-color: #FFFEE6; 
$text-main-color: #44443F;

html,
body 
  width: 100%;
  height: 100%;
  background-color: $base-color;
  font-size: 16px;
  font-family: "M PLUS Rounded 1c";
  color: $text-main-color;
  background-color: #fff;
  font-weight: bold;

.container
  &__inner 
    min-height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
  
.userData
  background-color: $primary-color;
  box-shadow: 0 3px 6px rgba(0,0,0,0.2);
  width: 100vw;
  margin-bottom: 20px;
  position: fixed;
  top: 0;
  color: white;
  &__inner
    padding: 24px;
    display: flex;
    justify-content: space-between
  &__text 
    font-size: 16px;

.answer 
  margin-bottom: 30px

  &__text
    color: #ED254A 
    font-size: 1.4em

  &-point__text
    color: #ED254A
    font-size: 2.4em
</style>
