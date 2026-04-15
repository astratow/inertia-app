<script setup>
defineProps({ post: Object });
</script>

<template>
    <div class="p-6">
        <h1>{{ post.title }}</h1>
        <p>{{ post.body }}</p>

        <small>By {{ post.user.name }}</small>
    </div>
</template>
