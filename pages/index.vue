<template>
  <main class="container">
    <app-header />
    <resturant-info />
  </main>
</template>

<script>
import AppHeader from "@/components/AppHeader.vue";
import ResturantInfo from "@/components/ResturantInfo.vue";

export default {
  components: {
    AppHeader,
    ResturantInfo
  }
};
</script>

<style></style>
