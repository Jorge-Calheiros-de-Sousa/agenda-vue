<template>
  <div>
    <b-sidebar
      id="day"
      :title="'Dia: ' + info.numero + ' de ' + info.mes + ' de ' + info.ano"
      shadow
    >
      <b-card header="Tarefas" v-if="info.tarefas">
        <b-list-group>
          <b-list-group-item v-for="tarefa in info.tarefas" :key="tarefa.id">
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
    info: {
      numero: 0,
      mes: "",
      ano: 0,
      tarefas: [],
    },
  },
};
</script>

<style>
</style>