<template>
  <div class="col-sm-6 col-md-4 mb-3">
    <div class="card">
      <div class="card-header">
        <h3>
          {{stock.name}}
          <small>(Price: {{stock.price}}} | Quantity: {{stock.quantity}})</small>
        </h3>
      </div>
      <div class="card-body">
        <div class="float-left">
          <input type="number" class="form-control" placeholder="Quantity" v-model="quantity" :class="{danger: insufficientQuantity}" />
        </div>
        <div class="float-right">
          <button
            class="btn btn-success"
            @click="sellStock"
            :disabled="insufficientQuantity || quantity <= 0 || !Number.isInteger(+quantity)"
          >{{ insufficientQuantity ? 'Not enought stock' : 'Sell'}}</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { mapActions } from "vuex";

export default {
  props: ["stock"],
  data() {
    return {
      quantity: 0
    };
  },
  computed: {
    insufficientQuantity() {
      return this.quantity > this.stock.quantity;
    }
  },
  methods: {
    ...mapActions({
      placeSellOrder: "sellStock"
    }),
    sellStock() {
      const order = {
        stockId: this.stock.id,
        stockPrice: this.stock.price,
        quantity: this.quantity
      };
      this.placeSellOrder(order);
      this.quantity = 0;
    }
  }
};
</script>

<style scoped>
    .danger {
        border: 1px solid red;
    }
</style>