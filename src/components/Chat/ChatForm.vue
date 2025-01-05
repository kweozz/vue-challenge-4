<script setup>
import { ref } from "vue";

const name = ref("User");
const messageText = ref("");

const emit = defineEmits(["sendMessage"]);

function sendMessage() {
  if (messageText.value.trim() !== "") {
    const newMessage = {
      user: name.value,
      text: messageText.value,
    };
    emit("sendMessage", newMessage);
    messageText.value = ""; // Clear input
  }
}
</script>

<template>
  <div class="form">
    <div class="input-group">
      <input
        v-model="messageText"
        type="text"
        placeholder="Add a comment..."
        class="input"
      />
    </div>
    <button @click="sendMessage" class="send-btn">Post</button>
  </div>
</template>

<style scoped>
.form {
  display: flex;
  align-items: center;
  gap: 10px;
  padding: 10px;
  border-top: 1px solid #ddd;
}

.input-group {
  display: flex;
  align-items: center;
  flex: 1;
  background-color: #f2f2f2;
  border-radius: 20px;
  padding: 5px 10px;
}


.input {
  flex: 1;
  border: none;
  background-color: transparent;
  outline: none;
  padding: 5px;
  font-size: 1rem;
  color: #333;
}

.send-btn {
  padding: 8px 16px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 20px;
  font-size: 0.9rem;
  cursor: pointer;
  transition: background-color 0.3s;
}

.send-btn:hover {
  background-color: #0056b3;
}

.send-btn:active {
  background-color: #003f7f;
}
</style>
