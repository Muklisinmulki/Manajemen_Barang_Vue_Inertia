<template>
  <div class="p-6 max-w-4xl mx-auto">
    <h1 class="text-3xl font-bold mb-6">Manajemen Barang</h1>
    <Link href="posts/create" class="bg-blue-500 text-white px-4 py-2 rounded hover:bg-blue-600">Create new Post</Link>
    <div class="overflow-x-auto mt-6">
      <table class="min-w-full bg-white border border-gray-200 rounded-lg shadow-md">
        <thead class="bg-gray-100">
          <tr>
            <th v-for="header in headers" :key="header" class="py-3 px-6 text-left text-gray-600 font-semibold">
              {{ header }}
            </th>
            <th class="py-3 px-6 text-left text-gray-600 font-semibold">Actions</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="post in posts" :key="post.id" class="border-b border-gray-200">
            <td class="py-4 px-6">{{ post.name }}</td>
            <td class="py-4 px-6">{{ post.description }}</td>
            <td class="py-4 px-6">{{ post.price }}</td>
            <td class="py-4 px-6">{{ post.quantity }}</td>
            <td class="py-4 px-6 flex space-x-2">
              <button @click="deletePost(post.id)" class="bg-red-500 text-white px-3 py-1 rounded hover:bg-red-600">
                Delete
              </button>
              <Link :href="`posts/${post.id}/edit`" class="bg-yellow-500 text-white px-3 py-1 rounded hover:bg-yellow-600">
                Edit
              </Link>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script setup>
import { Link, useForm } from '@inertiajs/vue3';

defineProps({
  posts: {
    type: Array,
    default: () => [],
  },
});

const headers = ['Name', 'Description', 'Price', 'Quantity'];
const form = useForm({});

const deletePost = (id) => {
  form.delete(`posts/${id}`);
};
</script>
