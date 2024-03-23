<script setup>
  import { ref, computed } from 'vue';
  import MainHeader from './components/MainHeader.vue';
  import MainInput from './components/MainInput.vue';
  
  const email = ref('');
  const messages = ref([]);
  const loginButtonPressed = ref(false);

  const successfullLogin = computed(
    () => email.value !== '' && loginButtonPressed.value
    );

  const addAiMessage = () => {
    const payload = {
      message: 'robot message',
      isUser: false
    }

    addMessage(payload);
  }

  const addMessage = (payload) => {
    messages.value = [...messages.value, payload];
  }

</script>

<template>
  <div class="main">
    <main-header 
      v-model="email" 
      :successfullLogin="successfullLogin" 
      @login="() => { loginButtonPressed = true}">
    </main-header>

  <div v-if="successfullLogin">
    <button @click="addAiMessage">addAiMessage</button>
    <ul>
      <li
        class="message" 
        v-for="(message, index) in messages" 
        :key="index" 
        :class="message.isUser ? 'user-message' : 'ai-message'">
        <p>{{ message.message }}</p>
        <small v-if="message.isUser">{{ email }}</small>
        <small v-else>ai generated message</small>
      </li>
    </ul>
  </div>
  <div v-else class="placeholder">
    Log in to start
  </div>

    <main-input
      v-if="successfullLogin"
      :user="email"
      v-model="messages"
      class="input"
      @addMessage="addMessage">
    </main-input>
  </div>
  
</template>

<style scoped>

  .placeholder {
    position: absolute;
    top: 50%;
    left: 50%;
  }

  .main {
    display: flex;
    flex-direction: column;
    place-content: space-between;
    height: 100%;
    overflow: hidden;

    ul {
      overflow-y: scroll;
      max-height: 500px;
      list-style: none;
      display: flex;
      flex-direction: column;
      
      gap: 1rem;

      li.message {
        width: fit-content;
        display: flex;
        flex-direction: column;
        place-items: flex-end;

        p {
          min-width: 150px;
          display: block;
          border-radius: 18px;
          margin: 0;
          padding: .5rem 1rem;
          text-align: start;
        }
      }

      li.ai-message{
        p{
          background-color: darkslateblue;
        }
      }
      li.user-message{
        align-self: flex-end;
        p{
          background-color: green;
        }
      }
    }
  }
</style>
