<template>
  <div style="padding: 5%; flex-flow: column;">
    <!-- class="flex flex-center" -->

    <div id="bern"></div>

    <div style="width: 300px; margin-top: 50px;" class="flex justify-center">
      <h5 class="full-width flex flex-center" style="color: white;">
        {{ title }}
      </h5>
      <h4
        style="font-size: 6vh; margin-top: 20px; color: white; font-weight: bold"
      >
        {{ minutes }}:{{ seconds }}
      </h4>
    </div>
    <div style="width: 300px; justify-content: space-evenly" class="flex ">
      <q-btn
        v-if="!timer"
        icon="play_arrow"
        text-color="white"
        color="grey-7"
        class="q-pa-md"
        @click="startTimer"
      />
      <q-btn
        text-color="white"
        color="grey-7"
        v-if="timer"
        icon="pause"
        class="q-pa-md"
        @click="stopTimer"
      />
      <q-btn
        text-color="white"
        color="grey-7"
        icon="refresh"
        class="q-pl-md q-pr-md"
        @click="resetTimer"
      />
    </div>
  </div>
</template>

<script>
import { mapState } from "vuex";
import { mapActions } from "vuex";

export default {
  data() {
    return {
      timer: null,
      totalTime: 0,
      resetButton: false,
      title: "Let's get going!"
    };
  },
  // ========================
  methods: {
    startTimer: function() {
      this.timer = setInterval(() => this.countdown(), 1000);
      this.resetButton = true;
      this.title = "Let's get going!";
      var bernWaling = document.getElementById("bern");
      bernWaling.classList.add("bern");
    },

    stopTimer: function() {
      clearInterval(this.timer);
      this.timer = null;
      this.resetButton = true;
      this.title = "Alomst there!";
      var bernWaling = document.getElementById("bern");
      bernWaling.classList.remove("bern");
    },

    resetTimer: function() {
      this.totalTime = 0;
      clearInterval(this.timer);
      this.timer = null;
      this.resetButton = false;
      this.title = "Let's get going!";
      var bernWaling = document.getElementById("bern");
      bernWaling.classList.remove("bern");
    },

    padTime: function(time) {
      return (time < 10 ? "0" : "") + time;
    },
    countdown: function() {
      if (this.totalTime <= 25 * 60) {
        this.totalTime++;
      } else {
        this.totalTime = 0;
        alert("Finished");
        this.resetTimer();
      }
    }
  },
  // ========================
  computed: {
    minutes: function() {
      const minutes = Math.floor(this.totalTime / 60);
      return this.padTime(minutes);
    },
    seconds: function() {
      const seconds = this.totalTime - this.minutes * 60;
      return this.padTime(seconds);
    }
  }
};
</script>

<style>
#bern {
  width: 112px;
  height: 156px;
  margin: auto;
  background: url(https://i.imgur.com/ifk0SLH.png) repeat-x;
  position: relative;
  bottom: 0px;
}

.bern {
  animation: walk 0.8s steps(6) infinite;
}

@keyframes walk {
  0% {
    background-position: 0;
  }
  100% {
    background-position: -672px;
  }
}
</style>
