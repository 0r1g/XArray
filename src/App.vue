<template>
  <div>
    <XArray v-model="myArray" />
  </div>
</template>

<script>
import XArray from './components/XArray.vue';

export default {
  components: {
    XArray,
  },
  data() {
    return {
      myArray: ['one', 'two'],
    };
  },
};
</script>
