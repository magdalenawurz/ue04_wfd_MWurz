<template>
  <div class="comment-list">
    <!-- Formular zum Hinzufügen neuer Kommentare -->
    <CommentForm @add="addComment" />

    <!-- Nachricht anzeigen wenn keine Kommentare vorhanden sind -->
    <div v-if="comments.length === 0" class="no-comments">
      Keine Kommentare vorhanden.
    </div>

    <!-- Kommentarliste -->
    <div v-else>
      <Comment
          v-for="(comment, index) in comments"
          :key="index"
          :name="comment.name"
          :message="comment.message"
          :date="comment.date"
          :index="index"
          @remove="removeComment"
      />
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted, watch } from "vue";
import CommentForm from "@/components/CommentForm.vue";
import Comment from "@/components/Comment.vue";

interface CommentObject {
  name: string;
  message: string;
  date: string;
}

// Array für Kommentare
const comments = ref<CommentObject[]>([]);

// Kommentare aus localStorage laden, falls vorhanden
onMounted(() => {
  const stored = localStorage.getItem("comments");
  if (stored) {
    comments.value = JSON.parse(stored);
  }
});

// Änderungen automatisch im localStorage speichern
watch(
    comments,
    (newVal) => {
      localStorage.setItem("comments", JSON.stringify(newVal));
    },
    { deep: true }
);

// Neuen Kommentar hinzufügen zum Anfang der Listej
function addComment(newComment: CommentObject) {
  comments.value.unshift(newComment);
}

// Kommentar löschen (index aus Event)
function removeComment(index: number) {
  comments.value.splice(index, 1);
}
</script>

<style scoped>
.comment-list {
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.no-comments {
  font-style: italic;
  color: #555;
  margin-top: 10px;
}
</style>