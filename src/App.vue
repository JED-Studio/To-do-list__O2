<script>
import { defineComponent, ref } from 'vue'
import AppFilters from './components/AppFilters.vue'
import AppMain from './components/AppMain.vue'

export default defineComponent({
  components: {
    AppFilters,
    AppMain,
  },

  setup() {
    const filter = ref('all')
    const appRouter = ref(false)
    const itemAll = ref(0)
    const itemActive = ref(0)
    const itemDone = ref(0)

    const updateFilter = (newFilter) => {
      filter.value = newFilter
      appRouter.value = false
    }

    const toggleSwiper = () => {
      appRouter.value = true
    }

    return {
      filter,
      toggleSwiper,
      appRouter,
      updateFilter,
      itemAll,
      itemActive,
      itemDone,
    }
  },
})
</script>

<template>
  <div class="to-do-list-o2__app">
    <AppFilters
      :filterd="filter"
      :itemAll="itemAll"
      :itemActive="itemActive"
      :itemDone="itemDone"
      @update:filter="updateFilter"
      @toggleSwiper="toggleSwiper"
    />
    <AppMain
      :filter="filter"
      :appRouter="appRouter"
      @itemAll="itemAll = $event"
      @itemActive="itemActive = $event"
      @itemDone="itemDone = $event"
    />
  </div>
</template>

<style scoped>
.to-do-list-o2__app {
  display: flex;
  height: 100vh;
}
</style>
