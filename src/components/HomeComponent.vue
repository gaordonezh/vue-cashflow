<template>
  <layout-component>
    <template #header>
      <header-component />
    </template>
    <template #resume>
      <resume-component
        :total-label="'Ahorro total'"
        :label="label"
        :totalAmount="100000"
        :amount="amount"
      >
        <template #graphic>
          <graphic-component :amounts="amounts" />
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
      movements: [
        {
          id: 1,
          title: 'Movimiento',
          description: 'Deposito de salario',
          amount: 100,
          date: new Date(),
        },
      ],
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
        const lastMovements = lastDays.slice(0, i);
        return lastMovements.reduce((suma, movement) => (suma += movement), 0);
      });
    },
  },
  methods: {
    create(movement) {
      this.movements.push(movement);
    },
    remove(id) {
      const index = this.movements.findIndex((item) => item.id === id);
      this.movements.splice(index, 1);
    },
  },
};
</script>
