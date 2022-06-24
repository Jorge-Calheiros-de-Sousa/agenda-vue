<template>
  <div>
    <nav-bar />
    <b-form-select v-model="anoAtual" :options="optionsAnos"></b-form-select>
    <side-form @submit="submit" />
    <side-bar :info="infoSideBar" />
    <b-container class="my-3">
      <month
        :anoAtual="anoAtual"
        :tarefas="data"
        @onClickMonth="infoToSideBar"
      />
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
    infoToSideBar(info) {
      this.infoSideBar = info;
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
      infoSideBar: {},
      anoAtual: new Date().getFullYear(),
      data: [],
      optionsAnos: [
        { value: 2024, text: "2024" },
        { value: 2023, text: "2023" },
        { value: 2022, text: "2022" },
      ],
    };
  },
  mounted() {
    this.getData();
  },
};
</script>

<style>
</style>