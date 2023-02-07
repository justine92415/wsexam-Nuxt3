<template lang="">
    <input
        v-if="type === 'text'"
        type="text"
        :id="id"
        v-model="modelValue"
        @change="updateModelValue"
        :placeholder="placeholder"
    />

    <input
        v-if="type === 'radio'"
        type="radio"
        :id="id"
        v-model="modelValue"
        :value="radioValue"
        :name="group"
        @change="updateModelValue"
    />

    <select
        v-if="type === 'select'"
        v-model="modelValue"
        @change="updateModelValue"
    >
        <option v-for="opt in optionArr" :key="opt" :value="opt">
            {{ opt }}
        </option>
    </select>
</template>
<script>
export default {
    props: {
        id: String,
        type: String,
        value: String,
        group: String,
        radioValue: String,
        optionArr: Array,
        placeholder: String,
    },
    emits: ['update'],
    data() {
        return {
            modelValue: this.value,
        };
    },

    methods: {
        updateModelValue() {
            this.$emit('update', this.modelValue);
        },
    },
};
</script>
