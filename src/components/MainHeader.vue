<script setup>
  import { ref } from 'vue';

  const model = defineModel({required: true});
  const props = defineProps({
    successfullLogin: {
      type: Boolean,
      required: true
    }
  });

  const emit = defineEmits(['login']);

  const email = ref('');

  const onSubmit = () => {
    email.value = model.value;
    emit('login', email.value);
  }

</script>

<template>
  <header>
    <p>website name</p>
    <form v-if="!successfullLogin" @submit.prevent="onSubmit">
      <input type="email" name="email" id="email" v-model="model">
      <input type="password" name="password" id="password">
      <button type="submit">Log in</button>
    </form>
    <p v-else>{{ email }}</p>
  </header>
</template>

<style lang="scss" scoped>
  header {
    background-color: #111111;
    padding: 1rem;
    width: 100%;

    display: flex;
    place-content: space-between;
    place-items: center;

    form {
      display: flex;
      gap: .5rem;
    }
  }
</style>