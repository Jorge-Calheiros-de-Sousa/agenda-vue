<template>
  <div>
    <div class="d-flex flex-row-reverse">
      <b-button v-b-toggle.form-sidebar>Cadastrar</b-button>
    </div>
    <b-sidebar id="form-sidebar" title="Cadastrar" right shadow>
      <div class="px-3 py-2">
        <b-form>
          <b-form-group id="input-group-1" label="Titulo" label-for="input-1">
            <b-form-input
              id="input-1"
              v-model="form.titulo"
              type="text"
              placeholder="Digite o titulo"
              required
            ></b-form-input>
          </b-form-group>

          <b-form-group
            id="input-group-2"
            label="Your Name:"
            label-for="input-2"
          >
            <b-form-input
              id="input-2"
              v-model="form.descricao"
              placeholder="Digite a descrição"
              required
            ></b-form-input>
          </b-form-group>

          <b-form-group id="input-group-3" label="Cor:" label-for="input-3">
            <b-form-select
              id="input-3"
              v-model="form.cor"
              :options="options"
              required
            ></b-form-select>
          </b-form-group>

          <b-form-group
            id="input-group-1"
            label="Data: "
            label-for="input-1"
            class="my-2"
          >
            <b-form-input
              id="input-1"
              v-model="form.data"
              type="date"
              required
            ></b-form-input>
          </b-form-group>

          <b-button
            type="button"
            @click="$emit('submit', form)"
            variant="primary"
            >Submit</b-button
          >
          <b-button type="reset" variant="danger" class="mx-2">Reset</b-button>
        </b-form>
      </div>
    </b-sidebar>
  </div>
</template>

<script>
export default {
  props: {
    form: {
      titulo: "",
      descricao: "",
      data: "",
      cor: "",
    },
  },
  data: function () {
    return {
      options: [
        { text: "Azul", value: "primary" },
        { text: "Vermelho", value: "danger" },
        { text: "Verde", value: "success" },
      ],
    };
  },
};
</script>

<style>
</style>