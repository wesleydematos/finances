<template>
  <div>
    <div class="flex items-center justify-between">
      <h1 class="font-bold text-2xl">Categorias</h1>
    </div>

    <div class="mt-6">
      <div>
        <div class="flex items-center space-x-3">
          <div>
            <AppFormInput v-model="name" @keyup.enter="addCategory" />
          </div>

          <AppButton @click="addCategory"> Adicionar </AppButton>
        </div>
      </div>

      <table class="mt-4 min-w-full divide-y divide-gray-200 shadow">
        <thead class="bg-gray-50">
          <tr>
            <th
              scope="col"
              class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider"
            >
              Categoria
            </th>
            <th scope="col" class="relative px-6 py-3">
              <span class="sr-only">Edit</span>
            </th>
          </tr>
        </thead>
        <tbody class="bg-white divide-y divide-gray-200">
          <tr
            v-for="category in categories"
            :key="category.id"
            class="bg-white"
          >
            <td
              class="px-6 py-4 whitespace-nowrap text-sm font-medium text-gray-900"
            >
              <div v-if="category.is_updating" class="w-72">
                <AppFormInput
                  v-model="category.name"
                  @keyup.enter="updateCategory(category)"
                />
              </div>

              <template v-else>
                {{ category.name }}
              </template>
            </td>

            <td
              v-if="category.id > 1"
              class="px-6 py-4 whitespace-nowrap text-right text-sm font-medium space-x-4"
            >
              <button
                class="text-indigo-600 hover:text-indigo-900"
                @click.stop.prevent="updateCategory(category)"
              >
                Edit
              </button>

              <button
                class="text-red-600 hover:text-red-900"
                @click.stop.prevent="deleteCategory(category.id)"
              >
                Excluir
              </button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
import AppButton from "~/components/Ui/AppButton";
import AppFormInput from "~/components/Ui/AppFormInput";
import AppFormLabel from "~/components/Ui/AppFormLabel";
import db from "~/static/db";

export default {
  name: "categoriesPage",

  components: {
    AppButton,
    AppFormInput,
    AppFormLabel,
  },

  data() {
    return {
      name: "",
      categories: db.categories,
    };
  },

  head() {
    return {
      title: "Categories",
      meta: [
        {
          hid: "description",
          name: "description",
          content:
            "Crie, edite e exclua categorias que serão utilizadas para organizar as suas finanças.",
        },
      ],
    };
  },

  methods: {
    deleteCategory(id) {
      const categoryIndex = this.categories.findIndex(
        (category) => category.id === id
      );

      if (categoryIndex !== -1) {
        this.categories.splice(categoryIndex, 1);
      }
    },

    updateCategory(category) {
      if (category.is_updating) {
        category.is_updating = false;
      } else {
        category.is_updating = true;
      }
    },

    addCategory() {
      if (!this.name) {
        return;
      }

      const id = db.categories.length + 1;

      const newCategory = {
        id: id,
        name: this.name,
        is_updating: false,
      };

      db.categories.push(newCategory);
      this.name = "";
    },
  },
};
</script>
