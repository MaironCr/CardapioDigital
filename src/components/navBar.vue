

<template>
  <div class="navbar bg-base-100 shadow-md px-4 sticky top-0 z-50">
    <!-- Botão do menu lateral -->
    <div class="flex-none">
      <button class="btn btn-square btn-ghost" @click="toggleSidebar">
        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="2" stroke="currentColor" class="w-6 h-6">
          <path stroke-linecap="round" stroke-linejoin="round" d="M4 6h16M4 12h16M4 18h16" />
        </svg>
      </button>
    </div>

    <!-- Logo -->
    <div class="flex-1">
      <h1 class="text-xl font-semibold tracking-tight">
       <router-link to='/'>
       <span class="text-primary">CARDÁPIO</span>
       </router-link>
        <span class="text-sm text-base-content/70"> | Cardápio digital</span>
      </h1>
    </div>

    <!-- Barra de pesquisa -->
    <div class="hidden md:flex flex-1 justify-center">
      <label class="input input-bordered flex items-center gap-2 w-80">
        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="2" stroke="currentColor" class="w-5 h-5 opacity-70">
          <path stroke-linecap="round" stroke-linejoin="round" d="M21 21l-4.35-4.35m0 0A7.5 7.5 0 104.5 4.5a7.5 7.5 0 0012.15 12.15z" />
        </svg>
        <input type="text" class="grow" placeholder="Pesquisar por alimento..." />
      </label>
    </div>

    <!-- Ações à direita -->
    <div class="flex-none gap-2">
      <!-- Tema -->
      <button class="btn btn-ghost btn-circle" @click="toggleTheme">
        <svg v-if="theme === 'light'" xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
          <path stroke-linecap="round" stroke-linejoin="round" d="M12 3v1m0 16v1m9-9h-1M4 12H3m15.364 6.364l-.707-.707M6.343 6.343l-.707-.707m12.728 0l-.707.707M6.343 17.657l-.707.707M16 12a4 4 0 11-8 0 4 4 0 018 0z" />
        </svg>
        <svg v-else xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
          <path stroke-linecap="round" stroke-linejoin="round" d="M21.752 15.002A9.718 9.718 0 0112 21a9.718 9.718 0 01-9.752-5.998A9.715 9.715 0 0112 3a9.715 9.715 0 019.752 12.002z" />
        </svg>
      </button>

      <!-- Notificações -->
      
      <button class="btn btn-ghost btn-circle">
      <router-link to="/notificações">
        <div class="indicator">
          <svg class="w-[31px] h-[31px]" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="none" viewBox="0 0 24 24">
          <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="1" d="M18.5 12A2.5 2.5 0 0 1 21 9.5V7a1 1 0 0 0-1-1H4a1 1 0 0 0-1 1v2.5a2.5 2.5 0 0 1 0 5V17a1 1 0 0 0 1 1h16a1 1 0 0 0 1-1v-2.5a2.5 2.5 0 0 1-2.5-2.5Z"/>
          </svg>
          <span class="badge badge-xs badge-primary indicator-item"></span>
        </div>
      </router-link>  
      </button>


      <!-- Carrinho de compras -->
      <router-link to="/carrinho" class="btn btn-ghost btn-circle">
        <div class="indicator">
          <svg class="w-[31px] h-[31px]" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="none" viewBox="0 0 24 24">
          <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="1" d="M5 4h1.5L9 16m0 0h8m-8 0a2 2 0 1 0 0 4 2 2 0 0 0 0-4Zm8 0a2 2 0 1 0 0 4 2 2 0 0 0 0-4Zm-8.5-3h9.25L19 7H7.312"/>
          </svg>
          <span
            v-if="itensCarrinho > 0"
            class="badge badge-sm badge-primary indicator-item">
            {{ itensCarrinho }}
          </span>



        </div>
      </router-link>

      <!-- Avatar -->
      <div class="dropdown dropdown-end">
        <label tabindex="0" class="btn btn-ghost btn-circle avatar">
          <div class="w-10 rounded-full">
            <img src="https://icon-library.com/images/no-profile-pic-icon/no-profile-pic-icon-7.jpg" alt="User avatar" />
          </div>
        </label>
        <ul tabindex="0" class="menu menu-sm dropdown-content mt-3 z-[1] p-2 shadow bg-base-100 rounded-box w-52">
          <li></li>
          <li><router-link to='/fazerlogin'><a class='login-link'>Fazer Login</a></router-link></li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";

const theme = ref("light");
const itensCarrinho = ref(); // teste (depois você pode integrar com store ou backend)

const props = defineProps({
  estaAberto: { type: Boolean, required: true },
});
const emit = defineEmits(["update:estaAberto"]);

function toggleSidebar() {
  emit("update:estaAberto", !props.estaAberto);
}

function toggleTheme() {
  theme.value = theme.value === "light" ? "dark" : "light";
  document.documentElement.setAttribute("data-theme", theme.value);
}
</script>
