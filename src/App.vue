<template>

  <div id="app" class="container">

    <div class="progress-circle__container">

    <span class="progress-circle__percent">{{ percent }}%</span>

      <svg class="progress-circle" viewBox="0 0 100 100" version="1.1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">

          <g>

            <circle cx="50" cy="50" r="40" style="fill:none;stroke:rgb(190,220,231);stroke-width:6.15px;"/>

            <circle class="progress-circle__path" cx="50" cy="50" r="40" style="fill:none;stroke:rgb(95,132,198);stroke-width:6.15px;transform-origin:50% 50%" :stroke-dasharray="circle" transform="rotate(-90)" />

          </g>
     
      </svg>

    </div>

    <a href="#" class="progress-circle__button" @click="randomNumber">Generate New Percentage</a>

  </div>

</template>

<script>

export default {
  name: 'app',
  data() {
    return {
      percent: 0,
      timerInterval: null
    }
  },
  methods: {
    randomNumber() {
      this.percent = Math.floor(Math.random() * (100 - 1 + 1)) + 1;
    },
    onInterval() {
      this.percent += 1
      if (this.percent == 100) {
        clearInterval(this.timerInterval)
      }
    }
  },
  computed: {
    circle() {
      return ((this.percent / 100) * 80 * Math.PI) + ',9999';
    }
  },
  mounted() {
    this.timerInterval = setInterval(this.onInterval, 50)
  }
}
</script>

<style lang="scss">

@import url('https://fonts.googleapis.com/css?family=Montserrat');

body {
  font-family: 'Montserrat', sans-serif;
}

.progress-circle {
  max-width:100px;
  max-height:100px;
  width:100%;
  
  &__percent {
    position:absolute;
    top:50%;
    left:50%;
    transform: translate(-50%,-50%);
  }
  
  &__container {
    display:inline-block;
    position:relative;
  }
  
  &__path {
   // transition: 0.5s ease-in-out all;
  }
  
  &__button {
    text-decoration:none;
    margin-top: 24px;
    margin-left:24px;
    background: #008080;
    color:white;
    padding: 18px 24px;
    border-radius: 4px;
    transition: 0.25s linear background;
    
    &:hover {
      cursor: pointer;
      background: darken(#008080, 5%);
      transition: 0.25s linear background;
    }
  }
  
}

.container {
  display: flex;
  min-height: 100vh;
  align-items: center;
  justify-content: center;
  flex-direction: column;
}

@media screen and (min-width:500px) {
  .container {
    flex-direction: row;
  }
  .progress-circle__button {
    margin-top:0;
  }
}

</style>
