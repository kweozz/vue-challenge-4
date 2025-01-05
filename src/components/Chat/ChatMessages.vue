<script setup>
import { defineProps } from "vue";

const props = defineProps({
  messages: {
    type: Array,
    required: true,
  },
});
</script>

<template>
  <div class="comments">
    <ul>
      <li v-for="(message, index) in messages" :key="index">
        <div class="message-content">
          <strong class="username">{{ message.user }}</strong>
          <p class="message-text">{{ message.text }}</p>
        </div>
      </li>
    </ul>
  </div>
</template>

<style scoped>
.comments {
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 10px;
  height: 300px;
  overflow-y: auto;
  background-color: #f9f9f9;
}

.comments ul {
  list-style: none;
  padding: 0;
  margin: 0;
}

.comments li {
  display: flex;
  align-items: flex-start;
  margin-bottom: 15px;
  padding-bottom: 10px;
  border-bottom: 1px solid #eee;
}

.comments li:last-child {
  border-bottom: none;
}


.message-content {
  max-width: 85%;
}

.username {
  font-weight: bold;
  font-size: 0.9rem;
  color: #333;
  margin-bottom: 3px;
  display: block;
}

.message-text {
  font-size: 0.9rem;
  color: #555;
  word-wrap: break-word;
}
</style>
