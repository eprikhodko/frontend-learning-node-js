<template>
  <header>
    <div>
      <nav class="flex gap-4">
        <ul class="flex gap-4 pb-4 hover:[&>*]:text-gray-500">
          <li>
            <RouterLink to="/">Shop</RouterLink>
          </li>
          <li>
            <RouterLink to="/admin/add-product">Add product</RouterLink>
          </li>
        </ul>
      </nav>
    </div>
  </header>

  <RouterView />
</template>

<script setup lang="ts">
import { RouterLink, RouterView } from "vue-router";
</script>

<style>
body {
  padding: 32px;
}
</style>
