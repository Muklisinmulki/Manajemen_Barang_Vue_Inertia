<template>
  <div class="p-6 max-w-lg mx-auto bg-white rounded-lg shadow-md">
    <h1 class="text-2xl font-bold mb-6">{{ isUpdating ? 'Update Produk' : 'Tambah Produk' }}</h1>
    <form @submit.prevent="submit" class="space-y-4">
      <div>
        <label for="name" class="block text-sm font-medium text-gray-700">Nama Produk</label>
        <input
          type="text"
          id="name"
          v-model="form.name"
          class="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-blue-500 focus:border-blue-500 sm:text-sm"
        />
      </div>

      <div>
        <label for="description" class="block text-sm font-medium text-gray-700">Deskripsi</label>
        <input
          type="text"
          id="description"
          v-model="form.description"
          class="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-blue-500 focus:border-blue-500 sm:text-sm"
        />
      </div>

      <div>
        <label for="price" class="block text-sm font-medium text-gray-700">Harga</label>
        <input
          type="text"
          id="price"
          v-model="form.price"
          class="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-blue-500 focus:border-blue-500 sm:text-sm"
        />
      </div>

      <div>
        <label for="quantity" class="block text-sm font-medium text-gray-700">Jumlah</label>
        <input
          type="text"
          id="quantity"
          v-model="form.quantity"
          class="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-blue-500 focus:border-blue-500 sm:text-sm"
        />
      </div>

      <button
        type="submit"
        class="w-full bg-blue-500 text-white px-4 py-2 rounded-md shadow-sm hover:bg-blue-600 focus:outline-none focus:ring-2 focus:ring-blue-500 focus:ring-offset-2"
      >
        {{ isUpdating ? 'Update' : 'Submit' }}
      </button>
    </form>
  </div>
</template>

<script setup>
import { onMounted } from 'vue';
import { useForm } from '@inertiajs/vue3';

const props = defineProps({
  post: {
    type: Object,
    default: null,
  },
  isUpdating: {
    type: Boolean,
    default: false,
  },
});

const form = useForm({
  name: '',
  description: '',
  price: '',
  quantity: '',
});

const submit = () => (props.isUpdating ? updatePost() : addPost());
const addPost = () => form.post('/posts');
const updatePost = () => form.put(`/posts/${props.post.id}`);

onMounted(() => {
  if (props.post) {
    form.name = props.post.name;
    form.description = props.post.description;
    form.price = props.post.price;
    form.quantity = props.post.quantity;
  }
});
</script>
