<template lang='pug'>
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
</template>

<script>
import { TweenMax, Back, Power0 } from 'gsap';
export default {
  components: {},
  props: {
    sec: {
      type: Number,
      default: 20,
    },
  },
  data() {
    return {
      counter: {
        timeCounter: this.sec,
        dasharray: 880,
        dashoffset: 0,
      },
    };
  },
  computed: {
    ...mapGetters({
      currentStatus: 'status/currentStatus',
      QUIZ_STATUSES: 'status/QUIZ_STATUSES',
    }),
    quizStatus() {
      return this.currentStatus.quizStatusId;
    },
  },
  watch: {
    quizStatus(newStatusId, oldStatusId) {
      if (
        newStatusId === this.QUIZ_STATUSES.THINKING &&
        oldStatusId === this.QUIZ_STATUSES.QUESTION
      ) {
        this.start();
      }
    },
  },
  methods: {
    repeat() {
      this.counter.timeCounter = this.counter.timeCounter - 1;
    },
    complete() {
      this.counter.timeCounter = 0;
      TweenMax.staggerFromTo(
        '.counter--timeup span',
        0.6,
        { opacity: 0, y: 14 },
        { opacity: 1, y: 0, ease: Back.easeOut.config(2) },
        0.1,
        () => {
          TweenMax.to('svg', 0.3, {
            delay: 0.3,
            scale: 1.2,
            opacity: 0,
            ease: Back.easeIn.config(1),
            onComplete: this.sendComplete,
          });
          TweenMax.to('.counter--timeup span', 0.3, { delay: 0.5, opacity: 0 });
        }
      );
    },
    reset() {
      this.counter.timeCounter = this.sec;
      TweenMax.killAll();
      TweenMax.set('svg', { scale: 1, opacity: 1 });
    },
    start() {
      this.reset();
      TweenMax.fromTo(
        this.counter,
        1,
        { dashoffset: this.counter.dasharray },
        {
          repeat: this.counter.timeCounter - 1,
          dashoffset: 0,
          ease: Power0.easeNone,
          onRepeat: this.repeat,
          onComplete: this.complete,
        }
      );
    },
    sendComplete() {
      this.$emit('complete');
    },
  },
};
</script>

<style lang='scss' scoped>
.count_down {
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 300px;
  height: 300px;
}
.count_down .circle_wrap {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  transform: rotate(-90deg);
}
.count_down svg {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}
.count_down svg .circle {
  fill: transparent;
  stroke-width: 18;
}
.count_down svg .circle--base {
  stroke: #ddd;
}
.count_down svg .circle--animation {
  stroke: #000;
}
.count_down .counter {
  font-size: 128px;
  font-weight: bold;
}
.count_down .counter--timeup {
  font-size: 32px;
}
.count_down .counter--timeup span {
  display: inline-block;
}
button {
  margin-top: 40px;
}
</style>
