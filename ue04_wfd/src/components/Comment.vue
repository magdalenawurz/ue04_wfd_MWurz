<template>
  <div class="comment" :class="backgroundClass">
    <div class="info">
      <strong>{{ name }}</strong>
      <span class="date">{{ date }}</span>
    </div>

    <p class="message">{{ message }}</p>

    <button @click="emitRemove">Entfernen</button>
  </div>
</template>

<script setup>
import { computed } from "vue";

const props = defineProps({
  name: String,
  message: String,
  date: String,
  index: Number
});

const emit = defineEmits(["remove"]);

const storedIndex = props.index;

function emitRemove() {
  emit("remove", storedIndex);
}

const backgroundClass = computed(() =>
    props.index % 2 === 0 ? "even" : "odd"
);
</script>

<style scoped>
.comment {
  border: 1px solid #ccc;
  border-radius: 6px;
  padding: 10px 15px;
  margin-bottom: 12px;
}

.even {
  background-color: #f8f8f8;
}

.odd {
  background-color: #e8e8e8;
}

.info {
  display: flex;
  justify-content: space-between;
  margin-bottom: 5px;
}
.date {
  color: #777;
}
button {
  margin-top: 10px;
  cursor: pointer;
}
</style>