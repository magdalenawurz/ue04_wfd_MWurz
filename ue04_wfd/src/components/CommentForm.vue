<template>
  <form @submit.prevent="submitComment" class="form">
    <label>
      Name:
      <input v-model="name" type="text" placeholder="Ihr Name" />
    </label>

    <label>
      Nachricht:
      <textarea v-model="message" placeholder="Ihre Nachricht"></textarea>
    </label>

    <button type="submit">Kommentar hinzufügen</button>

    <div v-if="error" class="error">{{ error }}</div>
  </form>
</template>

<script setup lang="ts">
import { ref } from "vue";

interface CommentObject {
  name: string;
  message: string;
  date: string;
}

// Event wird beim hinzufügen eines Kommentars ausgelöst
const emit = defineEmits<{
  (e: "add", comment: CommentObject): void
}>();

const name = ref("");
const message = ref("");
const error = ref("");

// Kommentar absenden
function submitComment() {
  if (!name.value.trim() || !message.value.trim()) {
    error.value = "Bitte Name und Nachricht ausfüllen.";
    return;
  }

  const newComment: CommentObject = {
    name: name.value,
    message: message.value,
    date: new Date().toLocaleString()
  };

  emit("add", newComment);

  // Eingabefelder leeren
  name.value = "";
  message.value = "";
  error.value = "";
}
</script>

<style scoped>
.form {
  display: flex;
  flex-direction: column;
  gap: 10px;
  margin-bottom: 20px;
}

input,
textarea {
  width: 100%;
  padding: 6px;
  font-size: 1rem;
}

button {
  width: 180px;
  cursor: pointer;
}

.error {
  color: red;
  font-size: 0.9rem;
}
</style>