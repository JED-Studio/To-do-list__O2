<script>
import { defineComponent, ref } from 'vue'

export default defineComponent({
  props: {
    text: String,
    id: Number,
    completed: Boolean,
  },

  setup(props, { emit }) {
    const isEditing = ref(false)
    const editedText = ref(props.text)

    const edit = () => {
      isEditing.value = !isEditing.value
      if (isEditing.value) {
        editedText.value = props.text
      } else {
        emit('update-text', props.id, editedText.value)
      }
    }

    const remove = () => {
      emit('remove', props.id)
    }

    const toggleCheckbox = () => {
      emit('toggle-checkbox', props.id)
    }

    return {
      isEditing,
      editedText,
      remove,
      edit,
      toggleCheckbox,
    }
  },
})
</script>

<template>
  <li class="to-do-list-o2__task">
    <div class="to-do-list-o2__checkbox-p">
      <input type="checkbox" name="checkbox" @click="toggleCheckbox()" />
      <p v-if="!isEditing">{{ text }}</p>
      <input v-else v-model="editedText" @keyup.enter="edit" />
    </div>
    <div class="to-do-list-o2__time-icons">
      <p class="to-do-list-o2__time">03:00-16:00</p>
      <div class="to-do-list-o2__icons">
        <i class="bi bi-pencil" @click="edit()"></i>
        <i class="bi bi-trash3" @click="remove()"></i>
      </div>
    </div>
  </li>
</template>

<style>
.to-do-list-o2__task {
  padding: 5px;
  background-color: white;
  display: flex;
  align-items: center;
  justify-content: space-between;
  border-radius: 5px;
  margin-bottom: 10px;
}

.to-do-list-o2__checkbox-p {
  display: flex;
}

.to-do-list-o2__time {
  background-color: gray;
  border-radius: 5px;
}

.to-do-list-o2__time-icons {
  display: flex;
  gap: 10px;
}

.to-do-list-o2__icons {
  display: flex;
  gap: 10px;
}
</style>
