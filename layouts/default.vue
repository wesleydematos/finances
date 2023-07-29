<template>
  <div>
    <header class="bg-gray-800">
      <nav>
        <div class="max-w-7xl mx-auto px-2 sm:px-6 lg:px-8">
          <div class="relative flex items-center justify-between h-16">
            <div class="flex-1 flex items-center items-stretch justify-start">
              <div class="flex-shrink-0 flex items-center">
                <img
                  class="block h-8 w-auto"
                  src="https://tailwindui.com/img/logos/workflow-mark-indigo-500.svg"
                  alt="Workflow"
                />
              </div>

              <div class="hidden sm:block sm:ml-6">
                <div class="flex space-x-4">
                  <NuxtLink
                    to="/"
                    :class="{
                      'bg-gray-900 text-white px-3 py-2 rounded-md text-sm font-medium':
                        $route.name === 'index',
                      'text-gray-300 hover:bg-gray-700 hover:text-white px-3 py-2 rounded-md text-sm font-medium':
                        $route.name !== 'index',
                    }"
                    >Início</NuxtLink
                  >
                  <NuxtLink
                    to="/categories"
                    :class="{
                      'bg-gray-900 text-white px-3 py-2 rounded-md text-sm font-medium':
                        $route.name === 'categories',
                      'text-gray-300 hover:bg-gray-700 hover:text-white px-3 py-2 rounded-md text-sm font-medium':
                        $route.name !== 'categories',
                    }"
                    >Categorias</NuxtLink
                  >
                </div>
              </div>
            </div>
          </div>
        </div>
      </nav>
    </header>

    <div class="max-w-7xl mx-auto p-4">
      <div class="mt-4">
        <Nuxt />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "",

  data() {
    return {};
  },

  methods: {},
};
</script>
