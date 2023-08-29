<template>
  <main>
    <p>{{ labelVisual }}</p>
    <h1>{{ amountCurrency }}</h1>
    <div class="graphic">
      <slot name="graphic" />
    </div>
    <div class="action">
      <slot name="action" />
    </div>
  </main>
</template>

<script>
const currencyFormater = new Intl.NumberFormat("es-PE", {
  style: "currency",
  currency: "PEN",
});

export default {
  props: {
    totalLabel: {
      type: String,
    },
    label: {
      type: String,
      default: "",
    },
    totalAmount: {
      type: Number,
      default: 0,
    },
    amount: {
      type: Number,
      default: 0,
    },
  },
  computed: {
    labelVisual() {
      return this.label ? this.label : this.totalLabel;
    },
    amountVisual() {
      return this.amount ? this.amount : this.totalAmount;
    },
    amountCurrency() {
      return currencyFormater.format(this.amountVisual);
    },
  },
};
</script>

<style scoped>
main {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  width: 100%;
}
h1,
p {
  margin: 0;
  text-align: center;
}
h1 {
  margin-top: 14px;
  color: var(--brand-green);
}
.graphic {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  padding: 48px 24px;
  box-sizing: border-box;
}
</style>
