<template>
  <!-- Layout principal -->
  <div class="flex">
    <div class="w-64" v-show="sidebarAberto">
      <logo />
      <menu-lateral />
    </div>

    <div class="flex flex-col flex-1 overflow-hidden">      
      <nav-bar v-model:estaAberto="sidebarAberto" />
      <main class="flex-1 overflow-y-auto p-6">
        <router-view></router-view>
      </main>
    </div>
  </div>
</template>

<script setup>
import { RouterView } from "vue-router";
import menuLateral from "@/components/menuLateral.vue";
import logo from "@/components/logo.vue";
import navBar from "@/components/navBar.vue";
import { onMounted, ref } from "vue";

const sidebarAberto = ref(true);

onMounted(() => {});
</script>

<style lang="scss" scoped></style>
