<script lang='ts'>
  import { ref, Ref } from 'vue';
  export default {
    name: 'app',
    data() {
      const startDate: Date = new Date('2024-05-01T07:00:00+02:00')
      const timeDifferenceString: Ref<string> = ref<string>("")
      return {
        startDate, timeDifferenceString
      }
    },
    methods: {
      updateTimer() {
        const now: Date = new Date()
        const timeDifferenceToStartDate: number = now.getTime() - this.startDate.getTime()
        const timeDifferenceFormattedString: string = this.formatTimeDifference(timeDifferenceToStartDate)
        this.timeDifferenceString = timeDifferenceFormattedString
      },
      formatTimeDifference(timeDiff: number): string {
        const days: number = Math.floor(timeDiff / (1000 * 60 * 60 * 24))
        const hours: number = Math.floor(timeDiff % (1000 * 60 * 60 * 24) / (1000 * 60 * 60))
        const hoursString: string = hours < 10 ? `0${hours}` : `${hours}`
        const minutes: number = Math.floor(timeDiff % (1000 * 60 * 60) / (1000 * 60))
        const minutesString: string = minutes < 10 ? `0${minutes}` : `${minutes}`
        const seconds: number = Math.floor(timeDiff % (1000 * 60) / (1000))
        const secondsString: string = seconds < 10 ? `0${seconds}` : `${seconds}`
        const timeDifferenceString: string = `${days}:${hoursString}:${minutesString}:${secondsString}`
        return timeDifferenceString
      }
    },
    mounted() {
      // initially update the timer
      this.updateTimer()
      setInterval(this.updateTimer, 1000)
    }
  }
</script>

<template>
  <div class='w-full h-full flex flex-col items-center justify-center'>
    <h1 class='text-8xl font-bold font-mono mb-2'>{{ timeDifferenceString }}</h1>
  </div>
</template>
