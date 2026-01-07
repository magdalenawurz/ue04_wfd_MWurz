<template>
  <div id="main">
    <Header />
    <CommentList />
  </div>
</template>

<script setup>
import Header from "@/components/Header.vue";
import CommentList from "@/components/CommentList.vue";
</script>

<style>
#main {
  margin: auto;
  width: 700px;
  padding: 20px;
  font-family: sans-serif;
}
</style>