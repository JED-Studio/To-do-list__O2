<script>
import { defineComponent, ref, onMounted, onBeforeUnmount, computed } from 'vue'

export default defineComponent({
  setup() {
    const now = ref(new Date())

    const nowTime = () => {
      now.value = new Date()
    }

    let nowInterval

    const nowUp = onMounted(() => {
      nowTime()
      nowInterval = setInterval(nowTime, 1000)
    })

    const nowUnmounted = onBeforeUnmount(() => {
      clearInterval(nowInterval)
    })

    const formattedTime = computed(() => {
      const options = { hour: '2-digit', minute: '2-digit', hour12: false }
      return now.value.toLocaleTimeString('ru-RU', options)
    })

    return {
      formattedTime,
      now,
      nowUp,
      nowInterval,
      nowUnmounted,
    }
  },
})
</script>

<template>
  <h2 class="to-do-list-o2__title-1">Good Morning, Roma!</h2>
  <p class="to-do-list-o2__date">
    Today, Wed 6 July 2024{{ formattedMonth }}{{ formatteNumber }} {{ formattedYear
    }}{{ formattedTime }}
  </p>
</template>

<style>
.to-do-list-o2__title-1 {
  margin-bottom: 10px;
}

.to-do-list-o2__date {
  color: #858585;
  margin-bottom: 2rem;
}
</style>
