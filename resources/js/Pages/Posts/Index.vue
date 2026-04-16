<script setup>
import { router } from "@inertiajs/vue3";
import AuthenticatedLayout from "@/Layouts/AuthenticatedLayout.vue";
import ActionButton from "@/Components/ActionButton.vue";

defineProps({
    posts: Array,
});

const destroy = (post) => {
    if (confirm(`Delete post?`)) {
        router.delete(`/posts/${post.id}`);
    }
};
</script>

<template>
    <AuthenticatedLayout>
        <template #header>
            <h2 class="text-xl font-semibold leading-tight text-gray-800">
                Posts
            </h2>
        </template>
        <div class="py-6">
            <div class="mx-auto max-w-7xl sm:px-6 lg:px-8">
                <ActionButton
                    label="Create Post"
                    :can="true"
                    variant="blue"
                    :onClick="() => router.visit(route('posts.create'))"
                    blockedMessage="You cannot create this post"
                />
                <div
                    class="overflow-hidden my-6 bg-white shadow-sm sm:rounded-lg"
                >
                    <div
                        v-for="post in posts"
                        :key="post.id"
                        class="p-3 mt-3 border-b"
                    >
                        <h2 class="font-bold">Title: {{ post.title }}</h2>
                        <p class="bg-gray-100">{{ post.body }}</p>
                        <small class="italic"
                            >by {{ post.user.name }} posted at
                            {{
                                new Date(post.created_at).toLocaleDateString(
                                    "pl-PL",
                                )
                            }}</small
                        >

                        <div class="mt-2">
                            <ActionButton
                                label="Edit"
                                :can="post.can.update"
                                variant="green"
                                :onClick="
                                    () => router.visit(`/posts/${post.id}/edit`)
                                "
                                blockedMessage="You cannot edit this post"
                            />

                            <ActionButton
                                label="Delete"
                                :can="post.can.delete"
                                variant="red"
                                :onClick="() => destroy(post)"
                                blockedMessage="You cannot delete this post"
                            />
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </AuthenticatedLayout>
</template>
