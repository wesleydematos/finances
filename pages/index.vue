<template>
  <div>
    <div class="flex items-center justify-between">
      <h1 class="font-bold text-2xl">Transações</h1>

      <AppButton @click="isAdding = !isAdding"> Nova transação </AppButton>
    </div>

    <TransactionAdd
      v-if="isAdding"
      @after-add="afterAdd"
      @cancel="isAdding = false"
    />

    <div class="mt-5 border border-grey-600" />

    <div class="mt-4">
      <div class="space-y-8">
        <div v-for="(transaction, index) in transactions" :key="index">
          <div class="mb-1">
            <div class="font-bold text-sm">
              {{ formatDate(transaction.date) }}
            </div>
          </div>

          <div class="space-y-3">
            <Transaction
              :key="transaction.id"
              :transaction="transaction"
              @update="onUpdate"
            />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import TransactionAdd from "~/components/Transactions/TransactionAdd";
import Transaction from "~/components/Transactions/Transaction";
import AppButton from "~/components/Ui/AppButton";
import TransactionFilter from "~/components/Transactions/TransactionFilter";
import db from "~/static/db";

export default {
  name: "IndexPage",

  components: {
    TransactionAdd,
    Transaction,
    AppButton,
    TransactionFilter,
  },

  data() {
    return {
      isAdding: false,
      transactions: db.transactions,
      categories: db.categories,
    };
  },

  methods: {
    formatDate(date) {
      return this.$dayjs(date).format("DD/MM/YYYY");
    },

    afterAdd(transaction) {
      this.transactions.push(transaction);
    },

    onUpdate(transaction) {
      const index = this.transactions.findIndex((t) => t.id === transaction.id);
      this.transactions.splice(index, 1, {
        ...transaction,
      });
    },
  },
};
</script>
