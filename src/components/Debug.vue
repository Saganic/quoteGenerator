<template>
  <div class="debug">
      <h4>Debug</h4>
      <ul>
        <li v-for="(value, propertyName) in data" :key="propertyName">
          {{ propertyName }}: {{ value }}
        </li>
      </ul>
    </div>
</template>

<script>
export default {
  name: 'Debug',
  props: {
    data: {
      type: Object,
      required: true,
    },
  },
};
</script>

<style scoped>
 .debug{
    position:fixed;
    bottom:0;
    right:0;
    padding:2%;
    background-color:brown;
    color:white;
  }
</style>
