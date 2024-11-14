<template>
<div>
    <div v-for="(item, index) in localArray" :key="index">
    <input
        :value="item"
        @input="updateValue($event.target.value, index)"
        @focus="setFocusedIndex(index)"
        @blur="removeIfEmpty(index)"
    />
    </div>
    <!-- Додатковий вхід для нових значень -->
    <input
    v-if="localArray[localArray.length - 1] !== ''"
    value=""
    @input="addNewInput($event.target.value)"
    @focus="setFocusedIndex(localArray.length)"
    />
</div>
</template>

<script>
export default {
name: 'XArray',
props: {
    modelValue: {
    type: Array,
    required: true,
    },
},
data() {
    return {
    localArray: [...this.modelValue],
    focusedIndex: null,
    };
},
methods: {
    // Оновлення значення в localArray
    updateValue(value, index) {
    this.localArray[index] = value; // пряме оновлення значення
    },
    addNewInput(value) {
    this.localArray.push(value); // додавання нового елемента
    },
    removeIfEmpty(index) {
    if (this.localArray[index] === '') {
        this.localArray.splice(index, 1); // видалення елемента, якщо він порожній
    }
    },
    setFocusedIndex(index) {
    this.focusedIndex = index; // зберігання індексу фокусу
    },
},
watch: {
    // Синхронізація з modelValue без циклічних оновлень
    modelValue(newVal) {
    if (newVal.length !== this.localArray.length) {
        this.localArray = [...newVal]; // оновлення localArray при зміні modelValue
    }
    },
},
};
</script>
