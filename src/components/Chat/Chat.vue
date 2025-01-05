<script setup>
import { reactive, onMounted, watch } from "vue";
import ChatMessages from "./ChatMessages.vue";
import ChatForm from "./ChatForm.vue";

// Reactive state to hold messages
const state = reactive({
  messages: [],
});

// Function to fetch messages from the API
async function fetchMessages() {
  try {
    const response = await fetch("https://lab5-p379.onrender.com/api/v1/messages/");
    const data = await response.json();
    console.log("Fetched messages:", data); // Debugging log
    state.messages = data.data.messages.reverse(); // Reverse for newest first
  } catch (error) {
    console.error("Error fetching messages:", error);
  }
}

// Function to add a new message
function addMessage(newMessage) {
  if (!newMessage || !newMessage.user || !newMessage.text) {
    console.error("Invalid message data:", newMessage);
    return;
  }

  const messageToSend = {
    user: newMessage.user,
    text: newMessage.text,
  };

  // Update local state immediately
  state.messages.unshift(newMessage);

  // Send to API
  fetch("https://lab5-p379.onrender.com/api/v1/messages/", {
    method: "POST",
    headers: {
      "Content-Type": "application/json",
    },
    body: JSON.stringify(messageToSend),
  })
    .then((res) => res.json())
    .then((data) => {
      console.log("Message saved:", data);
      // Optionally fetch messages again to ensure state is updated
      fetchMessages();
    })
    .catch((err) => {
      console.error("Error sending message:", err);
    });
}

// Fetch messages when the component is mounted
onMounted(() => {
  fetchMessages();
});

// Watch for changes in the current video and clear messages
watch(() => currentVideo.value, () => {
  state.messages = [];
  fetchMessages();
});
</script>

<template>
  <div>
    <ChatMessages :messages="state.messages" />
    <ChatForm @sendMessage="addMessage" />
  </div>
</template>
