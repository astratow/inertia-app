<script setup>
import { ref } from "vue";

const props = defineProps({
    label: String,
    can: {
        type: Boolean,
        default: true,
    },
    variant: {
        type: String,
        default: "gray", // gray | green | red | blue
    },
    onClick: Function,
    blockedMessage: {
        type: String,
        default: "You are not allowed to do this action",
    },
});

const showError = ref(false);
const errorMessage = ref("");

const handleClick = () => {
    if (!props.can) {
        errorMessage.value = props.blockedMessage;
        showError.value = true;
        return;
    }

    props.onClick?.();
};
</script>

<template>
    <button
        @click="handleClick"
        :class="[
            'm-1 px-4 py-1 rounded text-sm transition hover:opacity-80',
            !can && 'cursor-not-allowed opacity-50',
            variant === 'green' && 'bg-green-500 text-white',
            variant === 'red' && 'bg-red-500 text-white',
            variant === 'blue' && 'bg-blue-500 text-white',
            variant === 'gray' && 'bg-gray-500 text-white',
        ]"
    >
        {{ label }}
    </button>

    <!-- popup -->
    <div
        v-if="showError"
        class="fixed inset-0 bg-black/50 flex items-center justify-center"
    >
        <div class="bg-white p-4 rounded shadow max-w-sm text-center">
            <p class="mb-3">{{ errorMessage }}</p>
            <button
                class="px-3 py-1 bg-gray-800 text-white rounded"
                @click="showError = false"
            >
                OK
            </button>
        </div>
    </div>
</template>
