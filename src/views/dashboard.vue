<template>
  <div class="p-6">
    <h1 class="text-3xl font-bold mb-6 text-center"></h1>

    <!--ABA DE CATEGORIAS -->
    <div class="flex justify-center mb-6">
      <select v-model="categoriaSelecionada" class="select select-primary w-full max-w-xs">
        <option value="todas">Todas as Categorias</option>
        <option v-for="(cat, i) in categorias" :key="i" :value="cat">
          {{ cat }}
        </option>
      </select>
    </div>
    <!-- FIM DA ABA -->

    <!-- Grade de produtos -->
    <div class="grid gap-6 md:grid-cols-2 lg:grid-cols-3">
      <div
        v-for="(item, index) in cardapioFiltrado"
        :key="index"
        class="card bg-base-100 shadow-md hover:shadow-xl transition-all duration-300"
      >
        <figure>
          <img
            :src="item.imagem"
            :alt="item.nome"
            class="h-56 w-full object-cover"
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
import { ref, computed } from 'vue'
import { carrinho } from '@/store/carrinho'

const mensagem = ref('')

// FUNÇÃO DE ADICIONAR AO CARRINHO

const adicionarAoCarrinho = (item) => {
  carrinho.adicionar(item)
  mensagem.value = `${item.nome} foi adicionado ao carrinho!`
  setTimeout(() => (mensagem.value = ''), 2000)
}

// CARDÁPIO

const cardapio = [
  //HAMBÚRGUERES
  {
    categoria: "hambúrgueres",
    nome: "Cheeseburger Clássico",
    descricao: "Carne 150g, queijo cheddar, alface e tomate.",
    preco: 22.9,
    imagem: "https://images.unsplash.com/photo-1550547660-d9450f859349",
    novo: false,
  },
  {
    categoria: "hambúrgueres",
    nome: "Bacon Burger",
    descricao: "Carne suculenta, bacon crocante e molho especial.",
    preco: 26.9,
    imagem: "https://ogimg.infoglobo.com.br/in/23479725-1b1-ff2/FT1086A/20180511DonninhaFotoVitor-Faria-media-1.jpg",
    novo: true,
  },

  // Batatas
  {
    categoria: "Batatas Fritas",
    nome: "Batata Clássica",
    descricao: "Porção de batata frita tradicional.",
    preco: 14.9,
    imagem: "https://gastronomiacarioca.zonasul.com.br/wp-content/uploads/2023/05/batata_frita_destaque_ilustrativo_zona_sul.jpg",
    novo: false,
  },

  // Milkshake
  {
    categoria: "MilkShakes",
    nome: "Milkshake Chocolate",
    descricao: "Cremoso, com cobertura e chantilly.",
    preco: 12.9,
    imagem: "https://receitas.wap.ind.br/wp-content/uploads/2025/03/milkshake-de-chocolate.jpg",
    novo: false,
  },

  // Bebidas
  {
    categoria: "Bebidas",
    nome: "Refrigerante lata",
    descricao: "Coca-Cola, Guaraná ou Pepsi (350ml).",
    preco: 6.0,
    imagem: "https://st4.depositphotos.com/1063437/29839/i/1600/depositphotos_298390728-stock-photo-a-glass-and-a-can.jpg",
    novo: false,
  },
  {
    categoria: "Bebidas",
    nome: "Suco Natural de Laranja",
    descricao: "Suco natural espremido na hora.",
    preco: 8.5,
    imagem: "https://veja.abril.com.br/wp-content/uploads/2024/02/suco-laranja.jpg?crop=1&resize=1212,909",
    novo: false,
  },
]

// CATEGORIAS

const categoriaSelecionada = ref("todas")

const categorias = [...new Set(cardapio.map(i => i.categoria))]
categorias.unshift("todas")

// FILTRO DO CARDÁPIO

const cardapioFiltrado = computed(() => {
  if (categoriaSelecionada.value === "todas") return cardapio
  return cardapio.filter(item => item.categoria === categoriaSelecionada.value)
})
</script>


<style scoped>
.toast {
  z-index: 50;
}
</style>







<style lang="scss" scoped></style>