<template>
  <q-page class="flex flex-center bg-primary">
    <TimerControls />
  </q-page>
</template>

<script>
import TimerControls from "../components/TimerControls";

export default {
  name: "PageIndex",
  components: {
    TimerControls
  }
};
</script>
