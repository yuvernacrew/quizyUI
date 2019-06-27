<template lang='pug'>
  main.quiz.container
    .container__inner
      section.userData
        p.userData__inner
          span.userData__text {{ user.name }} さんのポイント
          span.userData__text {{ user.point }}pt
      
      section.question
        .question
          span.question__number Q{{ currentStatus.questionNo }}
          p.question__sentence {{ question.statement }}
        .choice
          ul.choiceList
            li.answer-list-item(v-for='answer, index in questionAnswers')
              button(
                type='button'
                @click='hundleClickAnswer(answer.id)'
                :class='{selected: answer.id === voteAnswerId}'
              )
                span {{ index + 1 }}.
                span {{ answer.statement }}
  </template>

<script>
export default {
  data() {
    return {
      countdownTime: 15,
      voteAnswerId: '',
      user: {
        name: 'ちーずかまぼこ',
        point: '227'
      },
      quizStatusIs: "WAITING",
      currentStatus: {
        questionNo: "1"
      },
      question: {
        statement: "坊主なヒューマンビートボックスな人は誰？"
      },
      questionAnswers: [
        {
          id: 1,
          statement: "大原"
        },
        {
          id: 2,
          statement: "牧"
        },
        {
          id: 3,
          statement: "大塚"
        },
      ]
    }
  }
}
</script>

<style lang='sass'>

$primary-color: #FCC205;
$secondary-color: #FFF598;
$base-color: #FFFEE6; 
$text-main-color: #44443F;

html,
body 
  width: 100%;
  height: 100%;
  box-sizing: border-box;
  background-color: $base-color;
  font-size: 16px;
  font-family: "M PLUS Rounded 1c";
  color: $text-main-color;
  background-color: $base-color;
  font-weight: bold;

.container 
  width: 100%;
  height: 100vh;
  padding: 40px;

  &__inner 
    min-height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;

.userData
  background-color: $secondary-color;
  width: 92vw;
  margin-bottom: 20px;
  position: fixed;
  top: 4vh;

  &__inner
    padding: 10px;
    display: flex;
    justify-content: space-between

  &__text 
    font-size: 14px;

.question 
  text-align: center;
  margin-bottom: 40px;

  &__number
    display: inline-block;
    padding: 0 40px 2px;
    line-height: 28px;
    height: 32px;
    border-radius: 20px;
    border: 2px solid $text-main-color;
    margin-bottom: 12px;
  
  &.__sentence 
    font-size: 24px;

.choice
  .choiceList 
    li 
      padding: 10px;
      border: 1px solid $primary-color;
      
      &:not(:last-child) 
        margin-bottom: 10px;

      button
        font-size: 24px;
    &.is-active
      background-color: $primary-color;
      color: #fff;


</style>
