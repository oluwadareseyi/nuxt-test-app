<template>
  <main class="container">
    <section
      class="image"
      :style="`background: url(/${currentItem.img}) no-repeat center center`"
    ></section>
    <section class="details">
      <h1>{{ currentItem.item }}</h1>
      <h3>Price: ${{ currentItem.price.toFixed(2) }}</h3>
      <div class="quantity">
        <input type="number" v-model="quantity" min="1" />
        <button @click="addToCart" class="primary">
          Add to cart - {{ totalCart }}
        </button>
      </div>
      <fieldset>
        <legend>
          <h3>Add ons</h3>
        </legend>
        <div v-for="addon in currentItem.addOns" :key="addon">
          <input
            type="checkbox"
            name="addon"
            :id="addon"
            :value="addon"
            v-model="itemAddons"
          />
          <label :for="addon">{{ addon }}</label>
        </div>
      </fieldset>
      <toast v-if="cartSubmitted">
        Order Submitted <br />
        check out more <nuxt-link to="/restaurants">resaturants</nuxt-link>
      </toast>
    </section>
    <section class="desc">{{ currentItem.description }}</section>
  </main>
</template>

<script>
import { mapState } from "vuex";
import Toast from "@/components/Toast.vue";
import { reactive, toRefs } from "@nuxtjs/composition-api";

export default {
  components: {
    Toast
  },
  setup() {
    const state = reactive({
      cartSubmitted: false,
      quantity: 1,
      itemAddons: []
    });

    return {
      ...toRefs(state)
    };
  },
  data() {
    return {
      id: this.$route.params.id
    };
  },
  computed: {
    ...mapState(["fooddata"]),
    currentItem() {
      const item = this.fooddata.find(el => {
        const currentMenu = el.menu.find(item => item.id === this.id);
        if (currentMenu) {
          return true;
        }
      });

      return item.menu.find(item => item.id === this.id);
    },
    totalCart() {
      return (this.currentItem.price * +this.quantity).toFixed(2);
    }
  },
  methods: {
    addToCart() {
      let formOutput = {
        item: this.currentItem.item,
        quantity: this.quantity,
        addOn: this.itemAddons,
        totalCart: this.totalCart
      };
      this.cartSubmitted = true;
      this.$store.commit("addToCart", formOutput);
    }
  }
};
</script>

<style lang="scss" scoped>
.container {
  margin: 100px auto;
  display: grid;
  grid-template-columns: 400px 1fr;
  grid-template-rows: 400px 1fr;
  grid-gap: 60px;
  line-height: 2;
  max-width: 1000px;
  padding: 0 20px;
}

.image {
  grid-area: 1 / 1 / 2 / 2;
  background-size: cover;
}
.details {
  grid-area: 1 / 2 / 2 / 3;
  position: relative;
}
.desc {
  grid-area: 2 / 1 / 3 / 2;
}
</style>
