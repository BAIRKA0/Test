<template>
    <section :class="['w-full', containerClass]">
        <section :class="['w-full relative', sectionClass]">
            <input @input="onInput" v-model="value" :type="props.type"
                :class="['peer w-full h-full pt-4 pb-2 bg-white outline outline-0 focus:outline-0 disabled:border-0 border-2 focus:border-2 text-sm px-3 py-2.5 rounded-[7px] border-gray-900 placeholder-shown:border-0 placeholder-shown:bg-gray-200 focus:bg-white', inputClass]"
                placeholder=" " />
            <label v-if="placeholder"
                :class="['flex w-full h-full select-none pointer-events-none absolute left-0 !overflow-visible truncate leading-tight peer-focus:leading-tight peer-disabled:text-transparent transition-all top-1.5 peer-placeholder-shown:text-sm text-[11px] peer-focus:text-[11px] before:block before:w-2.5 before:h-1.5 before:mt-[6.5px] before:mr-1 before:pointer-events-none before:transition-all after:content[\' \'] after:block after:flex-grow after:w-2.5 after:h-1.5 after:mt-[6.5px] after:pointer-events-none after:transition-all peer-placeholder-shown:leading-[2.25] text-gray-500', labelClass]">
                {{ placeholder }}
            </label>
            <button @click="clearInput" type="button"
                :class="['absolute right-2 top-1/2 transform -translate-y-1/2 peer-placeholder-shown:invisible', buttonClass]">
                <img src="./icons/close.svg" alt="Очистить" class="w-5 h-5"/>
            </button>
        </section>
        <span v-if="error" :class="['text-sm text-rose-600', errorClass]">{{ error }}</span>
    </section>
</template>

<script setup>
import { ref, defineProps, defineEmits, watch } from 'vue';

const props = defineProps({
    modelValue: String,
    label: String,
    id: String,
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

const value = ref(props.modelValue)

const emit = defineEmits(['update:modelValue']);

const onInput = (event) => {
    console.log(event.target.value)
    emit('update:modelValue', event.target.value);
};

const clearInput = () => {
    value.value = '';
    emit('update:modelValue', '');
};

watch(() => props.modelValue, (newValue) => {
    console.log(newValue)
    emit('update:modelValue', newValue);
});
</script>