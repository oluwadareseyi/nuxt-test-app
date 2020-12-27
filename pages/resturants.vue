<template>
  <div>
    <h1>Resturants:</h1>
    <resturant-info />
  </div>
</template>

<script>
import ResturantInfo from "@/components/ResturantInfo.vue";

export default {
  components: {
    ResturantInfo
  }
};
</script>

<style lang="scss" scoped>
h1 {
  padding: 20px 100px;
}
</style>
