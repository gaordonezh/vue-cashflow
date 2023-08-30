<template>
  <layout-component>
    <template #header>
      <header-component />
    </template>
    <template #resume>
      <resume-component
        :total-label="'Ahorro total'"
        :label="label"
        :totalAmount="totalAmount"
        :amount="amount"
      >
        <template #graphic>
          <graphic-component
            :amounts="amounts"
            @select="select"
          />
        </template>
        <template #action>
          <action-component @create="create" />
        </template>
      </resume-component>
    </template>
    <template #movements>
      <movements-component
        :movements="movements"
        @remove="remove"
      />
    </template>
  </layout-component>
</template>

<script>
import HeaderComponent from './HeaderComponent.vue';
import LayoutComponent from './LayoutComponent.vue';
import ResumeComponent from './ResumeComponent.vue';
import MovementsComponent from './MovementsComponent.vue';
import ActionComponent from './ActionComponent.vue';
import GraphicComponent from './GraphicComponent.vue';

export default {
  components: {
    LayoutComponent,
    HeaderComponent,
    ResumeComponent,
    MovementsComponent,
    ActionComponent,
    GraphicComponent,
  },
  data() {
    return {
      label: null,
      amount: null,
      movements: [],
    };
  },
  computed: {
    amounts() {
      const lastDays = this.movements
        .filter((item) => {
          const today = new Date();
          const oldDate = today.setDate(today.getDate() - 30);
          return item.date >= oldDate;
        })
        .map((item) => item.amount);

      return lastDays.map((m, i) => {
        const lastMovements = lastDays.slice(0, i + 1);
        return lastMovements.reduce((suma, movement) => (suma += movement), 0);
      });
    },
    totalAmount() {
      return this.movements.reduce((sum, next) => (sum += next.amount), 0);
    },
  },
  mounted() {
    const list = JSON.parse(localStorage.getItem('movements'));
    this.movements = (list || []).map((item) => ({
      ...item,
      date: new Date(item.date),
    }));
  },
  methods: {
    create(movement) {
      this.movements.push(movement);
      this.save();
    },
    remove(id) {
      const index = this.movements.findIndex((item) => item.id === id);
      this.movements.splice(index, 1);
      this.save();
    },
    save() {
      localStorage.setItem('movements', JSON.stringify(this.movements));
    },
    select(item) {
      this.amount = item;
    },
  },
};
</script>
