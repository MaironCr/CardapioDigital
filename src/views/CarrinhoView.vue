<template>
  <div class="p-6 max-w-3xl mx-auto">
    <h1 class="text-3xl font-bold mb-6 text-center">🛒 Meu Carrinho</h1>

    <div v-if="carrinho.itens.length">
      <div
        v-for="(item, i) in carrinho.itens"
        :key="i"
        class="flex justify-between items-center mb-4 p-3 bg-base-200 rounded-lg"
      >
        <div>
          <p class="font-semibold">{{ item.nome }} (x{{ item.quantidade }})</p>
          <p class="text-sm text-gray-500">R$ {{ item.preco.toFixed(2) }}</p>
        </div>
        <button class="btn btn-error btn-sm" @click="carrinho.remover(item)">Remover</button>
      </div>

      <div class="text-right mt-6">
        <h2 class="text-xl font-bold">Total: R$ {{ carrinho.total.toFixed(2) }}</h2>
        
        <!-- ABRIR MODAL -->
        <button class="btn btn-primary mt-3" @click="abrirModal">
          Finalizar Pedido
        </button>
      </div>
    </div>

    <div v-else class="text-center text-gray-500 mt-10">
      Seu carrinho está vazio 😢
    </div>

    <!-- MODAL -->
    <dialog ref="modalFinalizar" class="modal">
      <div class="modal-box">
        <h3 class="text-lg font-bold mb-5">Finalizar Pedido</h3>

        <div class="form-control mb-5">
          <label class="label">Número da Mesa </label>
          <input type="number" class="input input-bordered" v-model="mesa" placeholder="xxxx" />
        </div>

        <div class="form-control mb-3">
          <label class="label">Nome do Cliente</label>
          <input type="text" class="input input-bordered" v-model="cliente" placeholder="- - - -" />
        </div>

        <div class="modal-action">
          <button class="btn" @click="fecharModal">Cancelar</button>
          <button class="btn btn-success" @click="enviarPedido">Enviar para cozinha</button>
        </div>
      </div>
    </dialog>

  </div>
</template>

<script setup>
import { ref } from 'vue'
import { carrinho } from '@/store/carrinho'

// STATE
const mesa = ref('')
const cliente = ref('')
const modalFinalizar = ref(null)

// FUNÇÕES
const abrirModal = () => {
  modalFinalizar.value.showModal()
}

const fecharModal = () => {
  modalFinalizar.value.close()
}

const enviarPedido = () => {
  if (!mesa.value || !cliente.value) {
    alert("Preencha a mesa e o nome do cliente!")
    return
  }

  const pedido = {
    mesa: mesa.value,
    cliente: cliente.value,
    itens: carrinho.itens,
    total: carrinho.total,
    hora: new Date().toLocaleString()
  }

  console.log("📦 Pedido enviado para cozinha:", pedido)

  // SE QUISER ENVIAR PARA FIREBASE OU API:
  // await api.post("/cozinha", pedido)

  alert("Pedido enviado para a cozinha!")

  // limpar
  mesa.value = ''
  cliente.value = ''

  // fechar modal
  fecharModal()

  // esvaziar carrinho
  carrinho.limpar()
}
</script>
