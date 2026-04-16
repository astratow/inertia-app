<script setup>
import { useForm, Link } from "@inertiajs/vue3";
import AuthenticatedLayout from "@/Layouts/AuthenticatedLayout.vue";

const form = useForm({
    title: "",
    body: "",
});

const submit = () => {
    form.post(route("posts.store"));
};
</script>

<template>
    <AuthenticatedLayout>
        <template #header>
            <h2 class="text-xl font-semibold leading-tight text-gray-800">
                Create Post
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
            <form @submit.prevent="submit">
                <div>
                    <input
                        class="w-full mb-4"
                        v-model="form.title"
                        placeholder="Title"
                    />
                    <div v-if="form.errors.title">{{ form.errors.title }}</div>
                </div>

                <div>
                    <textarea
                        class="w-full mb-4"
                        v-model="form.body"
                        placeholder="Body"
                    ></textarea>
                    <div v-if="form.errors.body">{{ form.errors.body }}</div>
                </div>

                <button
                    class="px-4 py-2 bg-blue-600 text-white rounded hover:bg-blue-700 transition"
                    type="submit"
                >
                    Save
                </button>
            </form>
        </div>
    </AuthenticatedLayout>
</template>
