<template>
    <div>
        <label v-if="label" :for="id" class="block text-sm font-medium mb-1">{{
            label
        }}</label>
        <input
            :id="id"
            :type="type"
            :value="modeValue"
            :placeholder="placeholder"
            :disabled="disabled"
            :class="[
                'block w-full p-2 border rounded-md focus:outline-none focus:ring-2',
                inputTypeClasses,
            ]"
            @input="handleInput"
        />
        <p v-if="error" class="text-sm text-red-500 mt-1">{{ error }}</p>
    </div>
</template>
<script lang="ts">
import { computed, PropType } from "vue";
import { defineComponent } from "vue";
export default defineComponent({
    name: "ComponentInput",
    props: {
        id: { type: String, required: true },
        type: {
            type: String as PropType<"text" | "password" | "email" | "number">,
            default: "text",
        },
        modelValue: { type: String, default: "" },
        placeholder: { type: String, default: "" },
        label: { type: String, default: "" },
        disabled: { type: Boolean, default: false },
        error: { type: String, default: "" },
    },
    setup(props, { emit }) {
        const inputTypeClasses = computed(() => {
            return props.error
                ? "border-red-500 focus:ring-red-500"
                : "border-metal focus:ring-metal";
        });

        const handleInput = (event: Event) => {
            const target = event.target as HTMLInputElement;

            if (target) {
                emit("updated:modelInput", target.value);
            }
        };

        return { inputTypeClasses, handleInput };
    },
});
</script>
