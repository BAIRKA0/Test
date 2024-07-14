<template>
    <section class="w-full h-full">
        <button @click="toggleList" type="button" :class="{'bg-white border-2 border-gray-900': selectedValue||isListVisible, 'bg-gray-200': !selectedValue}" class="peer input flex w-full h-12 rounded-lg outline-none relative">
            <label :class="{'top-1': selectedValue, 'top-3': !selectedValue}"
                class="absolute left-2 text-gray-500 text-sm transition-all">{{ label }}</label>
            <label v-if="selectedValue" class="absolute left-2 text-black top-4">{{ selectedValue }}</label>
            <img src="./icons/arrow.svg" :class="{'rotate-180': isListVisible}"
                class="absolute right-2 top-1/2 transform -translate-y-1/2 w-5 h-5"/>
        </button>
        <section v-if="isListVisible" class="mt-4 mb-2">
            <ul class="flex flex-wrap gap-2 text-sm">
                <li v-for="(value, index) in values" :key="index" class="">
                    <input :id="`value${index}`" type="radio" class="hidden w-full h-full" :value="value" v-model="selectedValue">
                    <label :for="`value${index}`" :class="{'bg-blue-300': selectedValue!=value, 'bg-blue-500': selectedValue==value}" class="cursor-pointer w-full h-full text-center p-2 rounded">{{ value }}</label>
                </li>
            </ul>
        </section>
        <span v-if="error" class="text-sm text-rose-600">{{ error }}</span>
    </section>
</template>

<script setup>
import { ref, defineProps, watch } from 'vue';

const props = defineProps({
    modelValue: String,
    label: String,
    id: String,
    values: {
        type: Array,
        default: () => ["1 значение", "2 значение", "3 значение", "4 значение"]
    },
    type: {
        type: String,
        default: 'text'
    },
    placeholder: {
        placeholder: String,
        default: 'Заполните поле'
    },
    error: String,
    inputClass: {
        type: String,
        default: ''
    },
    labelClass: {
        type: String,
        default: ''
    },
    buttonClass: {
        type: String,
        default: ''
    },
    errorClass: {
        type: String,
        default: ''
    },
    containerClass: {
        type: String,
        default: ''
    },
    sectionClass: {
        type: String,
        default: ''
    }
});

const emit = defineEmits(['update:modelValue']);

const isListVisible = ref(false);
const selectedValue = ref(props.modelValue);

const toggleList = () => {
    isListVisible.value = !isListVisible.value;
};

watch(() => props.modelValue, (newValue) => {
    selectedValue.value = newValue;
});

watch(selectedValue, (newValue) => {
    if (newValue !== props.modelValue) {
        emit('update:modelValue', newValue);
    }
});
</script>