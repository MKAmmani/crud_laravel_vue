<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import { Head, Link, useForm } from '@inertiajs/vue3';

const props = defineProps({
    posts: Array
})
const form = useForm();

function deleteItem(id){
    if(confirm("Are you sure you want to delete this?")){
        form.delete(route('posts.destroy', id)),{
            preserveScroll: true
        }
    }
}
</script>

<template>
    <Head title="POSTS" />

    <AuthenticatedLayout>
        <template #header>
            <h2
                class="text-xl font-semibold leading-tight text-gray-800"
            >
                POSTS
            </h2>
        </template>

        <div class="py-12">
            <div class="mx-auto max-w-7xl sm:px-6 lg:px-8">
                <Link href="/posts/create" class="px-4 py-2 bg-slate">Create Post</Link>
                <div
                    class="overflow-hidden bg-white shadow-sm sm:rounded-lg"
                >
                    
                    <div class="p-2 text-gray-900">
                        SHOWING POSTS
                        <table>
                            <thead>
                                <tr>
                                    <th class="px-4 py-2">ID</th>
                                    <th class="px-4 py-2">Title</th>
                                    <th class="px-4 py-2">Content</th>
                                    <th class="px-4 py-2">Actions</th>
                                    <!--<th class="px-4 py-2">Author</th>
                                    <th class="px-4 py-2">Created At</th>-->
                                </tr>
                            </thead>
                            <tbody>
                                <tr v-for="post in posts" :key="post.id">
                                    <td class="border px-4 py-2">{{ post.id }}</td>
                                    <td class="border px-4 py-2">{{ post.title }}</td>
                                    <td class="border px-4 py-2">{{ post.body }}</td>
                                    <td class="border px-4 py-2">
                                        <Link :href="`/posts/${post.id}/edit`" class="mx-4 hover:underline bg-green-400">Edit</Link>
                                        <button @click="deleteItem(post.id)" class="mx-2 hover:underline bg-red-400">Delete</button>
                                    </td>
                                    <!--<td class="border px-4 py-2">{{ post.author.name }}</td>
                                    <td class="border px-4 py-2">{{ post.created_at }}</td>-->
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
        </div>
    </AuthenticatedLayout>
</template>
