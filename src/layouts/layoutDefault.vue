<template>
  <!-- Layout principal -->
  <div class="flex">
    <div class="w-64" v-show="sidebarAberto">
      <logo />
      <menuLateral />
    </div>


    <div class="flex flex-col flex-1 overflow-hidden">      
      <nav-bar v-model:estaAberto="sidebarAberto" />
      <main class="flex-1 overflow-y-auto p-6">
      </main>
    </div>
  </div>
</template>

<script setup>
import { RouterView } from "vue-router";
import menuLateral from "@/components/menuLateral.vue";
import logo from "@/components/logo.vue";
import navBar from "@/components/navBar.vue";
import { ref } from "vue";

const sidebarAberto = ref(false); // COMEÇA FECHADO
</script>

<style lang="scss" scoped></style>
