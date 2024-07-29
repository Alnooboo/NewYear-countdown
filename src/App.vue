<script setup>
import CountdownHeader from "@/components/CountdownHeader.vue";
import CountdownSegment from "@/components/CountdownSegment.vue";
import { ref } from "vue";

const newYear = new Date("Jan 1, 2025").getTime();

const days = ref(0);
const hours = ref(0);
const min = ref(0);
const seconds = ref(0);

const secondsToMin = 1000 * 60 * 60;

setInterval(() => {
  const timeNow = new Date().getTime();

  const timeDiff = newYear - timeNow;

  days.value = Math.floor(timeDiff / (secondsToMin * 24));
  hours.value = Math.floor((timeDiff % (secondsToMin * 24)) / secondsToMin);
  min.value = Math.floor((timeDiff % secondsToMin) / (1000 * 60));
  seconds.value = Math.floor((timeDiff % (1000 * 60)) / 1000);
}, 1000);
</script>
<template>
  <div class="app-wrapper">
    <div class="countdown-box">
      <CountdownHeader />
      <main class="flex justify-center">
        <CountdownSegment data-test="days" label="days" :number="days" />
        <CountdownSegment data-test="hours" label="hours" :number="hours" />
        <CountdownSegment data-test="minutes" label="minutes" :number="min" />
        <CountdownSegment
          data-test="seconds"
          label="seconds"
          :number="seconds"
        />
      </main>
    </div>
  </div>
</template>

<style scoped>
.app-wrapper {
  @apply flex items-center justify-center w-full h-full p-10;
}
.countdown-box {
  @apply shadow-md relative bg-white p-5 rounded-lg border-gray-100 border-[1px];
}
body {
  @apply bg-gray-100;
}
</style>
