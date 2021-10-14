<template>
  <div v-if="!isEdit" class="card">
    <p class="text" @click="switchIsEdit">{{ title }}</p>
    <button @click="remove">Remove</button>
  </div>
  <div v-else class="card">
    <input v-model="editTitle" type="text" placeholder="title" required />
    <button @click="edit">Edit</button>
  </div>
</template>

<script>
import { ref, watch } from 'vue';
export default {
  name: 'Todo',
  props: ['title', 'index'],
  emits: ['deleteTodo', 'editTodo'],
  setup(props, { emit }) {
    const isEdit = ref(false);
    const editTitle = ref(props.title);

    function switchIsEdit() {
      isEdit.value = !isEdit.value;
    }

    function remove() {
      emit('deleteTodo', props.index);
    }

    function edit() {
      switchIsEdit();
      emit('editTodo', { title: editTitle.value, index: props.index });
    }

    watch(
      () => props.title,
      () => (editTitle.value = props.title)
    );

    return {
      isEdit,
      editTitle,
      edit,
      remove,
      switchIsEdit
    };
  }
};
</script>

<style>
.card {
  display: flex;
  justify-content: space-between;
}

.card > div {
  width: 100%;
}

div > .text {
  width: 100%;
  text-align: left;
}
</style>
