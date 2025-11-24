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
            class="h-79 w-full object-cover"
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


  //HAMBÚRGUERES
  {
    nome: "Cheeseburger Clássico",
    descricao: "Carne 150g, queijo cheddar, alface e tomate.",
    preco: 22.9,
    imagem: "https://images.unsplash.com/photo-1550547660-d9450f859349",
    novo: false,
  },
  {
    nome: "Bacon Burger",
    descricao: "Carne suculenta, bacon crocante e molho especial.",
    preco: 26.9,
    imagem: "https://ogimg.infoglobo.com.br/in/23479725-1b1-ff2/FT1086A/20180511DonninhaFotoVitor-Faria-media-1.jpg",
    novo: true,
  },
  {
    nome: "Duplo Smash",
    descricao: "Dois burgers 100g, queijo e molho da casa.",
    preco: 29.9,
    imagem: "https://images.unsplash.com/photo-1551782450-a2132b4ba21d",
    novo: false,
  },
  {
    nome: "Veggie Burger",
    descricao: "Hambúrguer vegetal, maionese verde e salada fresca.",
    preco: 24.5,
    imagem: "https://s2-vogue.glbimg.com/HSrfFZSHwlmhebQ1GW145kRU_Ow=/0x0:620x466/984x0/smart/filters:strip_icc()/i.s3.glbimg.com/v1/AUTH_5dfbcf92c1a84b20a5da5024d398ff2f/internal_photos/bs/2022/V/i/sHBuE9TCAU2AXQjMwEcQ/2016-04-04-veggie-2.jpg",
    novo: false,
  },
  {
    nome: "Cheddar Melt",
    descricao: "Carne 180g, cheddar cremoso e cebola caramelizada.",
    preco: 27.9,
    imagem: "https://img.freepik.com/fotos-gratis/vida-morta-de-um-delicioso-hamburguer-americano_23-2149637307.jpg?semt=ais_incoming&w=740&q=80",
    novo: false,
  },

  {
    nome: "Picanha Burguer",
    descricao: "Picanha grelhada, queijo prato e molho barbecue.",
    preco: 31.9,
    imagem: "https://ricksfoodservices.com/wp-content/uploads/2021/08/hamburguer-de-picanha.jpg",
    novo: true,},



  //BATATAS FRITAS
  {
    nome: "Batata Clássica",
    descricao: "Porção de batata frita tradicional.",
    preco: 14.9,
    imagem: "https://gastronomiacarioca.zonasul.com.br/wp-content/uploads/2023/05/batata_frita_destaque_ilustrativo_zona_sul.jpg",
    novo: false,
  },
  {
    nome: "Batata com Cheddar e Bacon",
    descricao: "Porção generosa com cheddar cremoso e bacon crocante.",
    preco: 19.9,
    imagem: "https://softpig.com.br/wp-content/uploads/2023/10/Batata-frita-com-cheddar-e-bacon-Receita-softpig.jpg",
    novo: true,
  },
  {
    nome: "Batata Rústica",
    descricao: "Batata artesanal com casca e toque de alecrim.",
    preco: 17.9,
    imagem: "https://www.seara.com.br/wp-content/uploads/2025/09/batatarustica1200.jpg",
    novo: false,
  },



  ///MilkShake
  {
    nome: "Milkshake Chocolate",
    descricao: "Cremoso com chantilly, raspas de chocolate, calda e canudo de baunilha",
    preco: 10.80,
    imagem: "src/assets/images/milkshakechocolate.png",
    novo: false,
  },
  {
    nome: "Milkshake Morango",
    descricao: "Cremoso com morangos frescos, calda e chantilly",
    preco: 13.00,
    imagem: "src/assets/images/milkshakemorango.png",
    novo: false,
  },
  {
    nome: "Milkshake Misto",
    descricao: "Milkshake de Morango e Chocolate",
    preco: 17.80,
    imagem: "src/assets/images/milkshakemisto.png",
    novo: false,
  },


  //BEBIDAS
  {
    nome: "Cerveja Heineken",
    descricao: "CERVEJA HEINEKEN 330ML",
    preco: 9.9,
    imagem: "src/assets/images/cervejaheineken.png",
    novo: false,
  },
  {
    nome: "Cerveja Corona",
    descricao: "CERVEJA CORONA 350ML",
    preco: 9.9,
    imagem: "src/assets/images/cervejacorona.png",
    novo: false,
  },
  {
    nome: "Cerveja Eisenbahn",
    descricao: "CERVEJA EISENBAHN 600ML",
    preco: 9.9,
    imagem: "src/assets/images/cervejaeisebahn.png",
    novo: false,
  },
  {
    nome: "Cerveja Budweiser",
    descricao: "CERVEJA BUDWEISER 330ML",
    preco: 9.9,
    imagem: "src/assets/images/cervejabudweiser.png",
    novo: false,
  },
  {
    nome: "Refrigerante Lata",
    descricao: "COCA-COLA / GUARANÁ / PEPSI (350ml).",
    preco: 6.0,
    imagem: "src/assets/images/latinhas.png",
    novo: false,
  },
  {
    nome: "Suco Natural de Laranja",
    descricao: "SUCO NATURAL FEITO NA HORA",
    preco: 8.5,
    imagem: "src/assets/images/sucolaranja.png",
    novo: false,
  },
  
  {
    nome: "Água Mineral",
    descricao: "ÁGUA MINERAL VIENA 500ML",
    preco: 4.0,
    imagem: "src/assets/images/aguaviena.png",
    novo: false,
  },
  {
    nome: "Refrigerante 1L",
    descricao: "COCA-COLA / GUARANÁ ANTARTICA",
    preco: 8.0,
    imagem: "src/assets/images/refrigerantes1litro.png",
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