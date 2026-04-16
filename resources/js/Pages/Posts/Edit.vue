<script setup>
import AuthenticatedLayout from "@/Layouts/AuthenticatedLayout.vue";
import { useForm, Link } from "@inertiajs/vue3";

const props = defineProps({
    post: Object,
});

const form = useForm({
    title: props.post.title,
    body: props.post.body,
});

const submit = () => {
    form.put(route("posts.update", props.post.id));
};
</script>

<template>
    <AuthenticatedLayout>
        <template #header>
            <h2 class="text-xl font-semibold leading-tight text-gray-800">
                Edit Post
            </h2>
        </template>
        <div class="mx-auto max-w-7xl py-6 sm:px-6 lg:px-8">
            <div class="mb-6">
                <Link
                    class="px-4 py-2 bg-gray-200 hover:bg-gray-300 text-gray-800 rounded transition"
                    :href="route('posts.index')"
                    >Back</Link
                >
            </div>
            <form
                @submit.prevent="submit"
                class="w-full flex flex-col items-start"
            >
                <input
                    class="w-full mb-4"
                    v-model="form.title"
                    placeholder="Title"
                />
                <div v-if="form.errors.title">{{ form.errors.title }}</div>

                <textarea
                    class="w-full mb-4"
                    v-model="form.body"
                    placeholder="Body"
                ></textarea>
                <div v-if="form.errors.body">{{ form.errors.body }}</div>

                <button
                    type="submit"
                    class="m-1 px-4 py-1 rounded text-sm bg-green-500 text-white transition hover:opacity-80"
                >
                    Update
                </button>
            </form>
        </div>
    </AuthenticatedLayout>
</template>
