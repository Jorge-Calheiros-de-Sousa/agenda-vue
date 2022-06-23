<template>
  <div>
    <b-sidebar
      id="day"
      :title="'Dia: ' + dia.numero + ' de ' + mes.nome + ' de ' + ano"
      shadow
    >
      <b-card header="Feriado" v-if="dia.feriado">
        <b-list-group>
          <b-list-group-item>
            <b-icon icon="exclamation-circle-fill" variant="primary"></b-icon>
            {{ dia.feriado }}</b-list-group-item
          >
        </b-list-group>
      </b-card>
      <b-card header="Tarefas" v-if="dia.tarefas">
        <b-list-group>
          <b-list-group-item v-for="tarefa in dia.tarefas" :key="tarefa.id">
            <b-icon
              icon="exclamation-circle-fill"
              :variant="tarefa.cor"
            ></b-icon>
            {{ tarefa.titulo }}
            <b-card-body>
              {{ tarefa.descricao }}
            </b-card-body>
          </b-list-group-item>
        </b-list-group>
      </b-card>
    </b-sidebar>
  </div>
</template>

<script>
export default {
  props: {
    dia: {},
    ano: {},
    mes: {},
  },
};
</script>

<style>
</style>