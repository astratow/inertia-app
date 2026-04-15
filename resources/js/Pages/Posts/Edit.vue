<script setup>
import { useForm, Link } from "@inertiajs/vue3";

const props = defineProps({
    post: Object,
});

const form = useForm({
    title: props.post.title,
    body: props.post.body,
});

const submit = () => {
    form.put(`/posts/${props.post.id}`);
};
</script>

<template>
    <div class="p-6">
        <h1>Edit Post</h1>

        <form @submit.prevent="submit">
            <input v-model="form.title" />
            <div v-if="form.errors.title">{{ form.errors.title }}</div>

            <textarea v-model="form.body"></textarea>
            <div v-if="form.errors.body">{{ form.errors.body }}</div>

            <button type="submit">Update</button>
        </form>

        <Link href="/posts">Back</Link>
    </div>
</template>
