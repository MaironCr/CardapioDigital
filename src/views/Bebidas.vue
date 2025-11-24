<template>
  <div class="p-6">
    <h1 class="text-3xl font-bold mb-6 text-center"></h1>

    <!-- Grade de produtos -->
    <div class="grid gap-6 md:grid-cols-2 lg:grid-cols-3">
      <div
        v-for="(item, index) in cardapio"
        :key="index"
        class="card bg-base-100 shadow-md hover:shadow-xl transition-all duration-300"
      >
        <figure>
          <img
            :src="item.imagem"
            :alt="item.nome"
            class="h-100 w-full object-cover"
          />
        </figure>

        <div class="card-body">
          <h2 class="card-title">
            {{ item.nome }}
            <div v-if="item.novo" class="badge badge-secondary">Novo</div>
          </h2>

          <p>{{ item.descricao }}</p>

          <div class="card-actions justify-between items-center mt-2">
            <span class="font-bold text-lg">R$ {{ item.preco.toFixed(2) }}</span>

            <button class="btn btn-primary btn-sm" @click="adicionarAoCarrinho(item)">
              Pedir
            </button>
          </div>
        </div>
      </div>
    </div>

    <!-- Alerta visual -->
    <div
      v-if="mensagem"
      class="toast toast-top toast-center transition-all duration-500"
    >
      <div class="alert alert-success">
        <span>{{ mensagem }}</span>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { carrinho } from '@/store/carrinho'

const mensagem = ref('')

const adicionarAoCarrinho = (item) => {
  carrinho.adicionar(item)
  mensagem.value = `${item.nome} foi adicionado ao carrinho!`
  setTimeout(() => (mensagem.value = ''), 2000)
}

const cardapio = [
  // 🥤 BEBIDAS
  {
    nome: "Cerveja Heineken",
    descricao: "CERVEJA HEINEKEN 330ML",
    preco: 9.9,
    imagem: "public/images/cervejaheineken.png",
    novo: false,
  },
  {
    nome: "Cerveja Corona",
    descricao: "CERVEJA CORONA 350ML",
    preco: 9.9,
    imagem: "public/images/cervejacorona.png",
    novo: false,
  },
  {
    nome: "Cerveja Eisenbahn",
    descricao: "CERVEJA EISENBAHN 600ML",
    preco: 9.9,
    imagem: "public/images/cervejaeisebahn.png",
    novo: false,
  },
  {
    nome: "Cerveja Budweiser",
    descricao: "CERVEJA BUDWEISER 330ML",
    preco: 9.9,
    imagem: "public/images/cervejabudweiser.png",
    novo: false,
  },
  {
    nome: "Refrigerante Lata",
    descricao: "COCA-COLA / GUARANÁ / PEPSI (350ml).",
    preco: 6.0,
    imagem: "public/images/latinhas.png",
    novo: false,
  },
  {
    nome: "Suco Natural de Laranja",
    descricao: "SUCO NATURAL FEITO NA HORA",
    preco: 8.5,
    imagem: "public/images/sucolaranja.png",
    novo: false,
  },
  
  {
    nome: "Água Mineral",
    descricao: "ÁGUA MINERAL VIENA 500ML",
    preco: 4.0,
    imagem: "public/images/aguaviena.png",
    novo: false,
  },
  {
    nome: "Refrigerante 1L",
    descricao: "COCA-COLA / GUARANÁ ANTARTICA",
    preco: 8.0,
    imagem: "public/images/refrigerantes1litro.png",
    novo: false,
  },

]
</script>

<style scoped>
.toast {
  z-index: 50;
}
</style>
<script setup></script>

<style lang="scss" scoped></style>