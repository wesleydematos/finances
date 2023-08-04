<template>
  <div class="my-4 mt-10 space-y-4">
    <div class="grid sm:grid-cols-2 md:grid-cols-4 gap-5">
      <div>
        <AppFormLabel>Data da transação</AppFormLabel>
        <AppFormInput v-model="localTransaction.date" type="date" />
      </div>

      <div>
        <AppFormLabel>Valor</AppFormLabel>
        <AppFormInput v-model="localTransaction.amount" type="number" />
      </div>

      <div>
        <AppFormLabel>Descrição</AppFormLabel>
        <AppFormInput v-model="localTransaction.description" />
      </div>
    </div>

    <div class="space-x-4 flex items-center justify-end">
      <button
        class="inline-flex text-gray-700 text-sm"
        @click.stop.prevent="onCancel()"
      >
        Cancelar
      </button>

      <AppButton @click="updateTransaction"> Editar </AppButton>
      <button
        class="inline-flex items-center justify-center border focus:outline-none transition ease-in-out duration-150 text-white bg-red-600 hover:bg-red-800 border-red-600 hover:red-indigo-800 rounded text-sm px-4 py-2"
        @click.stop.prevent="deleteTransaction"
      >
        Excluir
      </button>
    </div>
  </div>
</template>

<script>
import AppButton from "~/components/Ui/AppButton";
import AppFormInput from "~/components/Ui/AppFormInput";
import AppFormLabel from "~/components/Ui/AppFormLabel";
import AppFormSelect from "~/components/Ui/AppFormSelect";
import db from "~/static/db";

export default {
  name: "TransactionEdit",

  components: {
    AppButton,
    AppFormInput,
    AppFormLabel,
    AppFormSelect,
  },

  props: {
    transaction: {
      type: Object,
      default: () => ({}),
    },
  },

  data() {
    return {
      localTransaction: {
        date: this.transaction.date,
        description: this.transaction.description,
        amount: this.transaction.amount,
        categoryId: this.transaction.categoryId,
        categoryName: this.transaction.categoryName,
        id: this.transaction.id,
      },
      categories: db.categories,
    };
  },

  methods: {
    updateTransaction() {
      const data = this.localTransaction;

      this.$emit("update", {
        ...data,
      });
      this.onCancel();
    },

    deleteTransaction() {
      const id = this.transaction.id;

      const transactionIndex = db.transactions.findIndex((t) => t.id === id);

      if (transactionIndex !== -1) {
        db.transactions.splice(transactionIndex, 1);
      }
    },

    onCancel() {
      this.$emit("cancel");
    },
  },
};
</script>
