<script setup>
import { reactive, onMounted } from "vue";
import ChatMessages from "./ChatMessages.vue";
import ChatForm from "./ChatForm.vue";

const state = reactive({
  messages: [],
});

async function fetchMessages() {
  try {
    const response = await fetch("https://messages-q7oe.onrender.com");
    const data = await response.json();
    state.messages = data.data.messages.reverse(); // Reverse for newest first
  } catch (error) {
    console.error("Error fetching messages:", error);
  }
}

function addMessage(newMessage) {
  if (!newMessage || !newMessage.user || !newMessage.text) {
    console.error("Invalid message data:", newMessage);
    return;
  }

  const messageToSend = {
    message: {
      user: newMessage.user,
      text: newMessage.text,
    },
  };

  // Update local state immediately
  state.messages.unshift(newMessage);

  // Send to API
  fetch("https://les3mongodb-y1hu.onrender.com/api/v1/messages", {
    method: "POST",
    headers: {
      "Content-Type": "application/json",
    },
    body: JSON.stringify(messageToSend),
  })
    .then((res) => res.json())
    .then((data) => {
      console.log("Message saved:", data);
    })
    .catch((err) => {
      console.error("Error sending message:", err);
    });
}

onMounted(() => {
  fetchMessages();
});
</script>

<template>
  <div>
    <ChatMessages :messages="state.messages" />
    <ChatForm @sendMessage="addMessage" />
  </div>
</template>
