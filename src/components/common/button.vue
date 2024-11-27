<template>
    <button
        :class="[
            'inline-flex items-center justify-center px-4 py-2 border rounded-md font-medium focus:outline-none transition',
            buttonTypeClasses,
        ]"
        :disabled="disabled"
        @click="handleClick"
    >
        <slot>{{ label }}</slot>
    </button>
</template>

<script lang="ts">
import { computed, defineComponent, PropType } from "vue";

export default defineComponent({
    name: "ComponentButton",
    props: {
        label: { type: String, default: "" },
        type: {
            type: String as PropType<"primary" | "secondary" | "danger">,
            default: "primary",
        },
        disabled: {
            type: Boolean,
            default: false,
        },
    },
    emits: ["click"],
    methods: {
        handleClick(event: MouseEvent) {
            if (!this.disabled) {
                this.$emit("click", event);
            }
        },
    },
    setup(props) {
        const buttonTypeClasses = computed(() => {
            switch (props.type) {
                case "primary":
                    return "bg-#00ffff text-#fff border-#00ffff hover:bg-#00faaa";
                case "secondary":
                    return "bg-gray-500 text-white border-gray-500 hover:bg-gray-600";
                case "danger":
                    return "bg-red-500 text-white border-red-500 hover:bg-red-600";
                default:
                    return "";
            }
        });
        return { buttonTypeClasses };
    },
});
</script>
