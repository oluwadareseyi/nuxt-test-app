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
        <button class="primary">
          Add to cart - {{ totalCart.toFixed(2) }}
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
    </section>
    <section class="desc">{{ currentItem.description }}</section>
  </main>
</template>

<script>
import { mapState } from "vuex";

export default {
  data() {
    return {
      id: this.$route.params.id,
      quantity: 1,
      itemAddons: []
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
      return this.currentItem.price * +this.quantity;
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
