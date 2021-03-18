<template>
  <h1> The pomodoro clock </h1>
  <section id="app">
    <div >
      <div class="container has-text-centered">
        <h2 class="title is-6">{{ message }}</h2>

        <!--  THE TIMER NUMBERS  -->
        <div id="timer">
          <span id="minutes">{{ twoDigits(m) }}</span>
          <span id="middle">:</span>
          <span id="seconds">{{ twoDigits(s) }}</span>
        </div>

        <!--  THE BUTTONS  -->
        <div id="buttons">
          <!--  START BUTTON    -->
          <button
            id="start"
            class="button is-dark is-large"
            @click="startTimer()"
            v-if="state === 's' || state === 'p'"
          >
            <i class="far fa-play-circle"></i>
          </button>

          <!--   PAUSE BUTTON   -->
          <button
            id="stop"
            class="button is-dark is-large"
            @click="pauseTimer()"
            v-if="state === 'r'"
          >
            <i class="far fa-pause-circle"></i>
          </button>

          <!--  RESET BUTTON   -->
          <button
            id="reset"
            class="button is-dark is-large"
            @click="resetTimer()"
            v-if="state === 'r' || state === 'p'"
          >
            <i class="fas fa-undo"></i>
          </button>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'Timer',
  data () {
    return {
      message: 'Let the countdown begin!!',
      state: 's',
      interval: undefined,
      m: 25,
      s: 0
    }
  },
  methods: {
    resetTimer: function () {
      this.state = 's'
      clearInterval(this.interval)
      this.message = 'Let the countdown begin !! '
      this.m = 25
      this.s = 0
    },
    startTimer: function () {
      this.message = 'Greatness is within sight !!'
      this.state = 'r'
      this.interval = setInterval(() => {
        if (this.s === 0) {
          this.m = this.m - 1
        } else {
          this.s = this.s - 1
        }
        if (this.m === 0 && this.s === 0) {
          this.resetTimer()
        }
      }, 1000)
    },
    pauseTimer: function () {
      this.state = 'p'
      clearInterval(this.interval)
      this.message = 'Never quit, keep going !!'
    }
  },
  filters: {
    twoDigits: function (num) {
      if (num < 10) {
        return '0' + num
      } else {
        return num
      }
    }
  }
}
</script>
<style scoped>
#message {
  color: #ddd;
  font-size: 50px;
  margin-bottom: 20px;
}

#timer {
  font-size: 200px;
  line-height: 1;
  margin-bottom: 40px;
}
</style>
