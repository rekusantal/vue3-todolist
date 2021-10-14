<template>
  <div class="form">
    <input v-model="newTitle" type="text" placeholder="title" required />
    <button type="button" @click="submit">SUBMIT</button>
  </div>
</template>

<script>
import { ref } from 'vue';

export default {
  name: 'RInput',
  emits: ['addTodo'],
  setup(props, { emit }) {
    const newTitle = ref('');
    function submit() {
      emit('addTodo', newTitle.value);
      newTitle.value = '';
    }
    return {
      submit,
      newTitle
    };
  }
};
</script>

<style scoped>
.form {
  display: flex;
  justify-content: space-between;
}
</style>
