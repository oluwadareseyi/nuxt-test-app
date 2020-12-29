<template>
  <nav>
    <ul>
      <li>
        <nuxt-link to="/" exact>
          <app-logo />
        </nuxt-link>
      </li>
      <li>
        <nuxt-link to="/restaurants" exact>Restaurants</nuxt-link>
      </li>
    </ul>
    <div class="smallnum" v-if="totalQuantity > 0">{{ totalQuantity }}</div>
    <nuxt-link to="/cart">Cart</nuxt-link>
  </nav>
</template>

<script>
import AppLogo from "@/components/AppLogo.vue";
import { mapGetters } from "vuex";

export default {
  components: {
    AppLogo
  },
  computed: {
    ...mapGetters(["totalQuantity"])
  }
};
</script>

<style lang="scss" scoped></style>
