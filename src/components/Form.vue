<template>
  <div class="container mb-5 px-5">
    <div class="form-group">
      <label for="titulo">Titulo</label>
      <input
        type="text"
        class="form-control"
        id="titulo"
        placeholder="Digite o titulo..."
        v-model="titulo"
      />
    </div>
    <br />
    <div class="form-group">
      <label for="descricao">Descrição</label>
      <textarea
        class="form-control"
        id="descricao"
        rows="3"
        placeholder="Digite a descrição..."
        v-model="descricao"
      ></textarea>
    </div>
    <br />
    <div class="text-center">
      <button class="btn btn-danger" @click="closeForm">Cancelar</button>
      <span class="mx-3"></span>
      <button class="btn btn-primary" @click="create" v-if="posEdit === null">
        Cadastrar
      </button>
      <button class="btn btn-primary" @click="update" v-else>
        Atualizar
      </button>
    </div>
  </div>
</template>

<script>
import { computed } from "@vue/reactivity";
import { useStore } from "vuex";

export default {
  setup() {
    const store = useStore();

    return {
      posEdit: computed(() => store.state.tarefa.posEdit),
      titulo: computed({
        get: () => store.state.tarefa.tarefa.titulo,
        set: (value) => (store.state.tarefa.tarefa.titulo = value),
      }),
      descricao: computed({
        get: () => store.state.tarefa.tarefa.descricao,
        set: (value) => (store.state.tarefa.tarefa.descricao = value),
      }),
      closeForm: () => store.commit("tarefa/closeForm"),
      create: () => store.commit("tarefa/create"),
      update: () => store.commit("tarefa/update"),
    };
  },
};
</script>