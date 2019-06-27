<template lang="pug">
  section.container
    //TODO(cheese): 画像の差し替え！
    .correct(v-show='correct')
      img(src='~/assets/images/correct.png')
    .incorrect(v-show='!correct')
      img(src='~/assets/images/incorrect.png')

    p 正解は　ーーー です。
    .correct(v-show='correct')
      p 33pt ゲット！！
</template>

<script>
export default {
  data() {
    return {
      correct: true
    }
  }
}
</script>

<style lang="sass">

.container
  &--inner 
    min-height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
  


</style>
