<script setup>
import { useForm, Link } from "@inertiajs/vue3";

const form = useForm({
    title: "",
    body: "",
});

const submit = () => {
    form.post("/posts");
};
</script>

<template>
    <div class="p-6">
        <h1>Create Post</h1>

        <form @submit.prevent="submit">
            <div>
                <input v-model="form.title" placeholder="Title" />
                <div v-if="form.errors.title">{{ form.errors.title }}</div>
            </div>

            <div>
                <textarea v-model="form.body" placeholder="Body"></textarea>
                <div v-if="form.errors.body">{{ form.errors.body }}</div>
            </div>

            <button type="submit">Save</button>
        </form>

        <Link href="/posts">Back</Link>
    </div>
</template>
