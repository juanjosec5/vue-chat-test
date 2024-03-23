<script setup>
  import { ref } from 'vue';

  const emit = defineEmits(['addMessage'])

  defineProps({
    user: {
      type: String,
      required: true
    }
  })

  const message = ref('');

  const onSubmit = () => {
    const payload = {
      message: message.value,
      isUser: true
    };

    emit('addMessage', payload);
    
    message.value = '';
  }
</script>

<template>
  <form class="input-wrapper" @submit.prevent="onSubmit">
    <input type="text" value="user" v-model="message">
    <button>send</button>
  </form>
</template>

<style lang="scss" scoped>
  .input-wrapper {
    padding: 1rem;
    width: 100%;
    display: flex;
    gap: 1rem;
    
    input {
      flex: 1 0 auto;
    }

    button {
      padding: .5rem 1rem;
    }
  }
</style>