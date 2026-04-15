<script setup>
import { Link, router } from "@inertiajs/vue3";

defineProps({
    posts: Array,
});

const destroy = (id) => {
    if (confirm("Are you sure?")) {
        router.delete(`/posts/${id}`);
    }
};
</script>

<template>
    <div class="p-6">
        <h1 class="text-2xl mb-4">Posts</h1>

        <Link href="/posts/create" class="text-blue-500"> Create Post </Link>

        <div v-for="post in posts" :key="post.id" class="border p-3 mt-3">
            <h2 class="font-bold">{{ post.title }}</h2>
            <p>{{ post.body }}</p>
            <small>by {{ post.user.name }}</small>

            <div class="mt-2">
                <Link
                    :href="`/posts/${post.id}/edit`"
                    class="mr-2 text-green-600"
                >
                    Edit
                </Link>

                <button
                    @click="router.delete(`/posts/${post.id}`)"
                    class="text-red-600"
                >
                    Delete
                </button>
            </div>
        </div>
    </div>
</template>
