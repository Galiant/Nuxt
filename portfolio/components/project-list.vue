<template>
  <p class="mb-10">Take at look at my Github projects</p>

  <section v-if="pending">Loading....</section>
  <section v-if="error">Something went wrong. Please try again!</section>
  <section v-else>
    <ul class="grid grid-cols-1 gap-4">
      <li
        v-for="repository in repos"
        :key="repository.id"
        class="border border-gray-200 rounded-sm p-4 hover:bg-gray-100 font-mono">
        <a :href="repository.html_url" target="_blank">
          <div class="flex items-center justify-between text-sm">
            <div class="font-semibold">{{ repository.name }}</div>
          </div>
          <p class="text-sm">{{ repository.description }}</p>
        </a>
      </li>
    </ul>
  </section>
</template>

<script setup>
const { error, pending, data } = await useFetch(
  'https://api.github.com/users/galiant/repos'
);

const repos = computed(() => data.value.filter((repo) => repo.description));
</script>
