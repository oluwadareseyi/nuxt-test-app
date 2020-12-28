<template>
  <main class="container">
    <app-header />
    <resturant-info :dataSource="fooddata" />
  </main>
</template>

<script>
import AppHeader from "@/components/AppHeader.vue";
import ResturantInfo from "@/components/ResturantInfo.vue";
import { mapState } from "vuex";

export default {
  components: {
    AppHeader,
    ResturantInfo
  },
  computed: {
    ...mapState(["fooddata"])
  }
};
</script>

<style></style>
