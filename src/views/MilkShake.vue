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
  ///MilkShake
  {
    nome: "Milkshake Chocolate",
    descricao: "Cremoso com chantilly, raspas de chocolate, calda e canudo de baunilha",
    preco: 10.80,
    imagem: "public/images/milkshakechocolate.png",
    novo: false,
  },
  {
    nome: "Milkshake Morango",
    descricao: "Cremoso com morangos frescos, calda e chantilly",
    preco: 13.00,
    imagem: "public/images/milkshakemorango.png",
    novo: false,
  },
  {
    nome: "Milkshake Misto",
    descricao: "Milkshake de Morango e Chocolate",
    preco: 17.80,
    imagem: "public/images/milkshakemisto.png",
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