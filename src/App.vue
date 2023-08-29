<template>
  <Suspense>
    <template #default>
      <home />
    </template>
    <template #fallback>
      <splash-screen />
    </template>
  </Suspense>
</template>

<script>
import { Suspense, defineAsyncComponent } from "vue";
import SplashScreen from "./components/SplashScreen.vue";

export default {
  components: {
    Home: defineAsyncComponent(
      () =>
        new Promise((resolve) => {
          setTimeout(() => {
            resolve(import("./components/HomeComponent.vue"));
          }, 1000);
        })
    ),
    Suspense,
    SplashScreen,
  },
};
</script>

<style>
html,
body,
.app {
  min-height: 100vh;
  margin: 0;
  font-family: Arial, Helvetica, sans-serif;
}

* {
  --brand-green: #04b500;
  --brand-blue: #0689b0;
}
</style>
