<template>
  <layout-component>
    <template #header>
      <header-component />
    </template>
    <template #resume>
      <resume-component
        :label="'Ahorro total'"
        :totalAmount="100000"
        :amount="amount"
      >
        <template #graphic>GRAPHIC</template>
        <template #action>
          <action-component />
        </template>
      </resume-component>
    </template>
    <template #movements>
      <movements-component :movements="movements" />
    </template>
  </layout-component>
</template>

<script>
import HeaderComponent from "./HeaderComponent.vue";
import LayoutComponent from "./LayoutComponent.vue";
import ResumeComponent from "./ResumeComponent.vue";
import MovementsComponent from "./MovementsComponent.vue";
import ActionComponent from "./ActionComponent.vue";

export default {
  components: {
    LayoutComponent,
    HeaderComponent,
    ResumeComponent,
    MovementsComponent,
    ActionComponent,
  },
  data() {
    return {
      label: null,
      amount: null,
      movements: [
        {
          id: 1,
          title: "Movimiento",
          description: "Deposito de salario",
          amount: 1000,
        },
        {
          id: 2,
          title: "Movimiento 1",
          description: "Deposito de honorarios",
          amount: 500,
        },
        {
          id: 3,
          title: "Movimiento 3",
          description: "Comida",
          amount: -100,
        },
        {
          id: 4,
          title: "Movimiento 4",
          description: "Colegiatura",
          amount: 1000,
        },
        {
          id: 5,
          title: "Movimiento 5",
          description: "Reparación equipo",
          amount: 1000,
        },
        {
          id: 6,
          title: "Movimiento",
          description: "Deposito de salario",
          amount: 1000,
        },
        {
          id: 7,
          title: "Movimiento 1",
          description: "Deposito de honorarios",
          amount: 500,
        },
        {
          id: 8,
          title: "Movimiento 3",
          description: "Comida",
          amount: -100,
        },
        {
          id: 9,
          title: "Movimiento 4",
          description: "Colegiatura",
          amount: 1000,
        },
        {
          id: 10,
          title: "Movimiento 5",
          description: "Reparación equipo",
          amount: 1000,
        },
      ],
    };
  },
};
</script>
