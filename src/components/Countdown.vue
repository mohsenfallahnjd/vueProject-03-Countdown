<template>
  <div id="countdonw">
    <div class="block">
      <p class="digit">{{ days | two_digits }}</p>
      <p class="text">Days</p>
    </div>
    <div class="block">
      <p class="digit">{{ hours | two_digits }}</p>
      <p class="text">Hours</p>
    </div>
    <div class="block">
      <p class="digit">{{ minutes | two_digits }}</p>
      <p class="text">Minutes</p>
    </div>
    <div class="block">
      <p class="digit">{{ seconds | two_digits }}</p>
      <p class="text">Seconds</p>
    </div>
  </div>
</template>

<script>
export default {
  mounted() {
    window.setInterval(() => {
      this.now = Math.trunc(new Date().getTime() / 1000);
    }, 1000);
  },
  props: {
    date: {
      type: String
    }
  },
  data() {
    return {
      now: Math.trunc(new Date().getTime() / 1000)
    };
  },
  computed: {
    dateInMilliseconds() {
      return Math.trunc(Date.parse(this.date) / 1000);
    },
    seconds() {
      return Math.abs((this.dateInMilliseconds - this.now) % 60);
    },
    minutes() {
      return Math.abs(Math.trunc((this.dateInMilliseconds - this.now) / 60) % 60);
    },
    hours() {
      return Math.abs(Math.trunc((this.dateInMilliseconds - this.now) / 60 / 60) % 24);
    },
    days() {
      return Math.abs((Math.trunc((this.dateInMilliseconds - this.now) / 60 / 60 / 24)))
    }
  },
  filters: {
    two_digits: value => {
      if (value < 0) {
        return "00";
      }
      if (value.toString().length <= 1) {
        return `0${value}`;
      }
      return value;
    }
  }
};
</script>

<style scoped lang="scss">
@import url(https://fonts.googleapis.com/css?family=Roboto+Condensed:400|Roboto:100);
.block {
  display: inline-block;
  flex-direction: column;
  margin: 20px;
}
.text {
  color: #1abc9c;
  font-size: 25px;
  font-family: "Roboto Condensed", serif;
  font-weight: 40;
  text-align: center;
  margin-top: 10px;
  margin-bottom: 10px;
}
.digit {
  color: #ecf0f1;
  text-align: center;
  font-size: 130px;
  font-weight: 100;
  font-family: "Roboto", serif;
  margin: 10px;
}
</style>
