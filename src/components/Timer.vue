<template>
    <div class="timer">
        <div class="progress" :style="{ width: percentage + '%' }"></div>
        <label class="label">00:{{ time }}</label>
    </div>
</template>
<script>
export default {
  name: 'Timer',
  data () {
    return {
      elapsed: 0,
      max: 30,
      interval: null
    }
  },
  computed: {
    percentage () {
     return (this.elapsed/this.max)*100
      /**
       * TODO: Calculate the percentage of the elapsed time
       */
      //return 50
    },
    time () {
      return this.pad(this.elapsed)
    }
  },
  mounted () {
    this.reset()
  },
  methods: {
    pad (number) {
      return ('00' + number).slice(-2)
    },
    start () {
      this.tick()

      setInterval(this.tick, 1000);


      /**
       * TODO: Setup an interval that calls the tick function every second
       *
       * Hint: Use the interval in the data -> this.interval
       */
    },
    reset () {

      this.elapsed = 0
      clearInterval(this.interval)
      this.$emit('tick', this.elapsed)
      this.start()
    },
    tick () {
      if (this.elapsed >= this.max) {
        clearInterval(this.interval)
         /* TODO: Stop the timer
         */

        this.$emit('done')
        return
      }


      this.elapsed++ // update and add one
       *//

      this.$emit('tick', this.elapsed)
    }
  }
}
</script>
<style scoped lang="scss">
    .timer {
        display: flex;
        align-items: center;
        justify-content: center;

        position: relative;
        height: 30px;
    }

    .progress {

        position: absolute;

        background-color: lighten(#46A379, 30%);
        z-index: -1;
        height: 100%;

        transition: width 150ms ease-in-out;
    }

    .label {
        color: black;
    }
</style>
