<template>
  <div>
    <b-card>
      <div class="d-flex align-items-center justify-content-around">
        <div class="d-flex align-items-center">
          <b-icon
            icon="arrow-bar-left"
            @click="changeMonth(-1)"
            style="cursor: pointer"
          ></b-icon>
          <div class="--w-100 text-center">{{ meses[indexMes] }}</div>
          <b-icon
            icon="arrow-bar-right"
            @click="changeMonth(1)"
            style="cursor: pointer"
          ></b-icon>
        </div>
      </div>
      <div class="--d-grid-mouth my-2">
        <b-card v-for="semana in semanas" :key="semana">
          <b-card-text class="text-center">
            {{ semana }}
          </b-card-text>
        </b-card>
        <b-card
          v-for="(dia, indice) in getDays"
          :key="indice"
          :class="isToday(dia.numero)"
          @click="
            $emit('onClickMonth', {
              numero: dia.numero,
              mes: meses[indexMes],
              ano: anoAtual,
              tarefas: dia.tarefas,
            })
          "
          v-b-toggle.day
        >
          <b-container class="text-center my-2">
            {{ dia.numero }}
          </b-container>
          <b-card-text class="--heigth-68px scroll-bar-custom overflow-auto">
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
      <!-- <div class="--d-grid-mouth">
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
      </div> -->
    </b-card>
  </div>
</template>

<script>
export default {
  props: {
    anoAtual: {},
    tarefas: [],
  },
  data: function () {
    return {
      semanas: [
        "Domingo",
        "Segunda",
        "Terça",
        "Quarta",
        "Quinta",
        "Sexta",
        "Sabado",
      ],
      meses: [
        "Janeiro",
        "Fevereiro",
        "Março",
        "Abril",
        "Maio",
        "Junho",
        "Julho",
        "Agosto",
        "Setembro",
        "Outubro",
        "Novembro",
        "Dezembro",
      ],
      indexMes: new Date().getMonth(),
    };
  },
  methods: {
    changeMonth(number) {
      this.indexMes = this.indexMes + number;
      if (this.indexMes < 0) {
        this.indexMes = this.meses.length - 1;
      }
      if (this.meses.length === this.indexMes) {
        this.indexMes = 0;
      }
    },
    isToday(dia) {
      if (dia) {
        const dataAtual = new Date().toDateString();
        const data = new Date(this.anoAtual, this.indexMes, dia).toDateString();
        if (dataAtual === data) {
          return " bg-info";
        }
      }
    },
  },
  computed: {
    getDays() {
      const dias = [];
      const date = new Date(this.anoAtual, this.indexMes + 1, 0);
      const primeiroDia = new Date(this.anoAtual, this.indexMes, 1);
      const nomeSemana = this.semanas[primeiroDia.getDay()];
      const indexSemana = this.semanas.findIndex(
        (semana) => semana === nomeSemana
      );

      for (let index = 0; index <= indexSemana - 1; index++) {
        dias.push({
          numero: "",
          tarefas: [],
        });
      }
      for (let index = 1; index <= date.getDate(); index++) {
        const tarefas = this.tarefas.filter((tarefa) => {
          const tarefaData = new Date(tarefa.data).toDateString();
          const data = new Date(
            this.anoAtual,
            this.indexMes,
            index - 1
          ).toDateString();
          if (tarefaData === data) {
            return tarefa;
          }
        });
        dias.push({
          numero: index,
          tarefas: tarefas,
        });
      }
      return dias;
    },
  },
};
</script>

<style>
.--heigth-130px {
  height: 130px;
}
.--heigth-68px {
  height: 68px;
}

.--w-100 {
  width: 100px !important;
  padding: 0 10px 0 10px;
}

.scroll-bar-custom::-webkit-scrollbar {
  width: 1px;
}

.--d-grid-mouth {
  display: grid !important;
  grid-template-columns: repeat(7, 13.5%) !important;
  gap: 10px;
}
.min-width {
  min-width: 150px !important;
}
</style>