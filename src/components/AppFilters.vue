<script>
import { defineComponent } from 'vue'

export default defineComponent({
  props: {
    filterd: String,
    itemAll: Number,
    itemActive: Number,
    itemDone: Number,
  },

  setup(props, { emit }) {
    const changeFilter = (newFilter) => {
      emit('update:filter', newFilter)
    }

    const toggleSwiper = () => {
      emit('toggleSwiper')
    }

    return { changeFilter, toggleSwiper }
  },
})
</script>

<template>
  <aside class="to-do-list-o2__sidebar">
    <h2 class="to-do-list-o2__title">Private</h2>
    <ul class="to-do-list-o2__filters">
      <li :class="{ gold: filterd === 'all' }" @click="changeFilter('all')">
        All
        <p>{{ itemAll }}</p>
      </li>
      <li :class="{ gold: filterd === 'active' }" @click="changeFilter('active')">
        Active
        <p>{{ itemActive }}</p>
      </li>
      <li :class="{ gold: filterd === 'done' }" @click="changeFilter('done')">
        Done
        <p>{{ itemDone }}</p>
      </li>
      <li @click="toggleSwiper()">Swiper</li>
    </ul>
  </aside>
</template>

<style scoped>
.to-do-list-o2__filters li {
  display: flex;
  justify-content: space-between;
}

.to-do-list-o2__filters li > p {
  background-color: #cfcfcf;
  color: black;
  border-radius: 10px;
  padding: 0 4px;
  transition:
    background-color 0.2s linear,
    color 0.2s linear,
    fill 0.2s linear;
}

.to-do-list-o2__sidebar {
  background-color: white;
  width: 100%;
  max-width: 20rem;

  border-radius: 5px;
  padding: 45px 20px;
}

.to-do-list-o2__title {
  margin-bottom: 2rem;
}

.to-do-list-o2__filters > li {
  padding: 10px;
  border-radius: 5px;
  margin-bottom: 10px;
  transition:
    background-color 0.2s linear,
    color 0.2s linear,
    fill 0.2s linear;
}

.to-do-list-o2__filters > li:hover {
  background-color: #f4f4f4;
}

.gold {
  background-color: #f4f4f4;
}

.to-do-list-o2__filters > li:hover p {
  background-color: #ffffff;
}
</style>
