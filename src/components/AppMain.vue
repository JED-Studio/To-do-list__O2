<script>
import { defineComponent, ref, computed, watch, onMounted } from 'vue'
import AppMainList from './AppMainList.vue'
import AppMainTime from './AppMainTime.vue'

export default defineComponent({
  components: {
    AppMainList,
    AppMainTime,
  },

  props: {
    filter: String,
    appRouter: Boolean,
  },

  setup(props, { emit }) {
    const items = ref([])
    const textAdd = ref('')

    const loadItems = () => {
      const storedItems = localStorage.getItem('items')
      if (storedItems) {
        items.value = JSON.parse(storedItems)
      }
    }

    const push = () => {
      items.value.push({
        id: Date.now(),
        text: textAdd.value,
        completed: false,
      })
      textAdd.value = ''
      localStorage.setItem('items', JSON.stringify(items.value))
    }

    const removeItem = (id) => {
      items.value = items.value.filter((item) => item.id !== id)
      localStorage.setItem('items', JSON.stringify(items.value))
    }

    const filteredTasks = computed(() => {
      if (props.filter === 'active') {
        return items.value.filter((item) => !item.completed)
      } else if (props.filter === 'done') {
        return items.value.filter((item) => item.completed)
      }
      return items.value
    })

    const updateText = (id, newText) => {
      const item = items.value.find((item) => item.id === id)
      if (item) {
        item.text = newText
      }
    }

    const toggleCheckbox = (id) => {
      const item = items.value.find((item) => item.id === id)
      if (item) {
        item.completed = !item.completed
      }
    }

    const itemAll = computed(() => items.value.length)

    const itemActive = computed(() => items.value.filter((item) => !item.completed).length)

    const itemDone = computed(() => items.value.filter((item) => item.completed).length)

    onMounted(() => {
      loadItems()
    })

    watch([itemAll, itemActive, itemDone], ([newItemAll, newItemActive, newItemDone]) => {
      emit('itemAll', newItemAll)
      emit('itemActive', newItemActive)
      emit('itemDone', newItemDone)
    })

    return {
      push,
      items,
      itemAll,
      textAdd,
      itemDone,

      itemActive,
      updateText,
      removeItem,

      filteredTasks,
      toggleCheckbox,
    }
  },
})
</script>

<template>
  <main v-if="!appRouter" class="to-do-list-o2__main">
    <div class="to-do-list-o2__main-flex">
      <AppMainTime />

      <ul class="to-do-list-o2__tasks">
        <TransitionGroup name="list" tag="ul">
          <AppMainList
            v-for="item in filteredTasks"
            :key="item.id"
            :text="item.text"
            :id="item.id"
            :completed="item.completed"
            @remove="removeItem"
            @toggle-checkbox="toggleCheckbox"
            @update-text="updateText"
          />
        </TransitionGroup>
      </ul>
    </div>
    <div class="to-do-list-o2__add">
      <div class="to-do-list-o2__chat">
        <i class="bi bi-x-lg"></i>

        <input class="to-do-list-o2__input" name="text" v-model="textAdd" @keyup.enter="push" />
        <i class="bi bi-send" @click="push"></i>
      </div>
    </div>
  </main>
  <main v-if="appRouter" class="to-do-list-o2__main">velvklebm lekmblek</main>
</template>

<style>
.list-move, /* apply transition to moving elements */
.list-enter-active,
.list-leave-active {
  transition: all 0.5s ease;
}

.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: translateX(30px);
}

.list-leave-active {
  position: absolute;
}

.to-do-list-o2__main {
  width: 100%;
  padding: 4rem 9rem;

  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.to-do-list-o2__tasks > li {
  margin-bottom: 10px;
  padding: 10px;
  background-color: white;
  border-radius: 5px;
}

.to-do-list-o2__add {
}

.bi-x-lg {
  position: absolute;
  color: white;
  top: 13px;
  left: 17px;
  transition: transform 0.2s linear;
}

.bi-x-lg:hover {
  transform: rotate(45deg);
}

.bi-send {
  position: absolute;
  color: white;
  top: 13px;
  right: 20px;
  transition: transform 0.2s linear;
}

.to-do-list-o2__chat {
  width: 100%;
  max-width: 21rem;
  position: relative;
  display: flex;
}

.to-do-list-o2__input {
  width: 100%;
  background-color: black;
  padding: 15px 15px 15px 40px;
  border-radius: 25px;
  border: none;
  color: white;
  transition:
    box-shadow 0.2s linear,
    background-color 0.2s linear,
    color 0.2s linear,
    fill 0.2s linear;
}

.to-do-list-o2__input:hover {
  box-shadow: 0px 0px 10px 0px rgba(0, 0, 0, 0.555);
}

.to-do-list-o2__input:focus {
  outline: none;
}

.to-do-list-o2__time-icons {
  display: flex;
}
</style>
