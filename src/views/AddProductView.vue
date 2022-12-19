<template>
  <div>
    <main>
      <form class="flex gap-4">
        <input
          v-model="title"
          type="text"
          name="title"
          class="rounded-md border border-solid border-gray-300 p-2 text-gray-700"
        />

        <button
          type="button"
          @click="addProduct"
          class="bg-gray-300 px-8 rounded-md hover:bg-gray-400 font-bold text-1 text-letters-primary transition duration-[150ms]"
        >
          Add
        </button>
      </form>
    </main>
  </div>
</template>

<script setup lang="ts">
import { ref } from "vue";

const title = ref("");

const addProductToServer = async () => {
  // console.log({ title: title.value });
  try {
    const response = await fetch("http://localhost:3333/admin/add-product", {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      body: JSON.stringify({ title: title.value }),
    });
    console.log(response);
  } catch (error) {
    console.error(error);
  }
};

const addProduct = () => {
  const isOnlySpaces = (str: string) => {
    return /^\s*$/.test(str);
  };
  const isStringContainOnlySpaces = isOnlySpaces(title.value);
  if (isStringContainOnlySpaces) {
    title.value = "";
  }
  if (title.value !== "" && !isStringContainOnlySpaces) {
    addProductToServer();

    title.value = "";
  }
};
</script>
