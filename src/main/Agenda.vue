<template>
  <div>
    <nav-bar />
    <b-form-select v-model="anoAtual" :options="optionsAnos"></b-form-select>
    <b-form-select v-model="mesAtual" :options="optionsMes"></b-form-select>
    <side-form :form="form" @submit="submit" />
    <side-bar :dia="diaSideBar" :mes="mesSideBar" :ano="anoAtual" />
    <b-container class="my-3">
      <month :meses="transformData" @onClickMonth="infoToSideBar" />
    </b-container>
  </div>
</template>

<script>
import NavBar from "../components/NavBar.vue";
import Month from "../components/Month.vue";
import SideBar from "../components/SideBar.vue";
import SideForm from "../components/SideForm.vue";
export default {
  components: { NavBar, Month, SideBar, SideForm },
  methods: {
    infoToSideBar(dia, nomeMes) {
      this.diaSideBar = dia;
      this.mesSideBar = nomeMes;
    },
    getData() {
      this.data = require("../data/data.json");
    },
    submit(form) {
      console.log("submit");
    },
  },
  data: function () {
    return {
      diaSideBar: {},
      mesSideBar: {},
      anoAtual: 2022,
      data: [],
      mesAtual: 1,
      optionsAnos: [
        { value: 2024, text: "2024" },
        { value: 2023, text: "2023" },
        { value: 2022, text: "2022" },
      ],
      optionsMes: [
        { value: 1, text: "Janeiro" },
        { value: 2, text: "Fevereiro" },
      ],
      form: {
        titulo: "",
        descricao: "",
        data: "",
        cor: "",
      },
    };
  },
  computed: {
    transformData() {
      const data = this.data.filter(
        (data) => data.numeroDoMes === this.mesAtual
      );
      return data;
    },
  },
  mounted() {
    this.getData();
  },
};
</script>

<style>
</style>