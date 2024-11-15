<template>
  <ion-app class="light-theme">
    <ion-router-outlet />
  </ion-app>
</template>

<script setup lang="ts">
import { IonApp, IonRouterOutlet } from '@ionic/vue';
</script>
<style scoped>
.light-theme {
  --ion-background-color: #ffffff;
  --ion-text-color: #000000;
  /* Atur warna komponen lain sesuai kebutuhan */
}
</style>