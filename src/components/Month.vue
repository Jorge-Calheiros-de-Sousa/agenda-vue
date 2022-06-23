<template>
  <div>
    <b-card v-for="mes in meses" :key="mes.numeroDoMes">
      {{ mes.nome }}
      <div class="--d-grid-mouth my-2">
        <span
          class="min-width text-center"
          v-for="semana in semanas"
          :key="semana"
          >{{ semana }}</span
        >
      </div>
      <div class="--d-grid-mouth">
        <b-card
          v-for="dia in mes.dias"
          :key="dia.numero"
          class="min-width --heigth-130px"
          @click="$emit('onClickMonth', dia, mes)"
          v-b-toggle.day
        >
          <b-container class="text-center my-2">
            {{ dia.numero }}
          </b-container>
          <b-card-text class="--heigth-69px scroll-bar-custom overflow-auto">
            <div
              v-if="dia.feriado"
              class="bg-info rounded text-center"
              style="color: white"
            >
              {{ dia.feriado }}
            </div>
            <div
              v-for="tarefa in dia.tarefas"
              :key="tarefa.id"
              :class="' my-2 rounded text-center bg-' + tarefa.cor"
              style="color: white"
            >
              {{ tarefa.titulo }}
            </div>
          </b-card-text>
        </b-card>
      </div>
    </b-card>
  </div>
</template>

<script>
export default {
  props: {
    meses: [],
  },
  data: function () {
    return {
      semanas: [
        "Segunda",
        "Terça",
        "Quarta",
        "Quinta",
        "Sexta",
        "Sabado",
        "Domingo",
      ],
    };
  },
};
</script>

<style>
.--heigth-130px {
  height: 130px;
}
.--heigth-69px {
  height: 69px;
}

.scroll-bar-custom::-webkit-scrollbar {
  width: 1px;
}

.--d-grid-mouth {
  display: grid !important;
  grid-template-columns: repeat(7, 172px) !important;
  gap: 10px;
}
.min-width {
  min-width: 150px !important;
}
</style>