<template>
  <div class="m-4">
    <p>categories</p>
    <AppFormInput />
    <AppButton> Adicionar </AppButton>
  </div>
</template>

<script>
import AppButton from "~/components/Ui/AppButton";
import AppFormInput from "~/components/Ui/AppFormInput";

export default {
  name: "categoriesPage",

  components: {
    AppButton,
    AppFormInput,
  },

  data() {
    return {};
  },

  methods: {},
};
</script>

<style></style>
