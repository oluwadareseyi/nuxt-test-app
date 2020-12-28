<template>
  <main class="container restaurant">
    <div class="restaurantheading">
      <h1>Restaurants:</h1>
      <app-select @change="selectedResturant = $event" />
    </div>
    <resturant-info :dataSource="filteredResturants" />
  </main>
</template>

<script>
import ResturantInfo from "@/components/ResturantInfo.vue";
import AppSelect from "@/components/AppSelect.vue";
import { mapState } from "vuex";

export default {
  components: {
    ResturantInfo,
    AppSelect
  },
  data() {
    return {
      selectedResturant: ""
    };
  },
  computed: {
    ...mapState(["fooddata"]),
    filteredResturants() {
      if (this.selectedResturant) {
        return this.fooddata.filter(el => {
          let name = el.name.toLowerCase();
          return name.includes(this.selectedResturant);
        });
      }

      return this.fooddata;
    }
  }
};
</script>

<style lang="scss" scoped></style>
