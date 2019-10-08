<template>
<div class="materials">
    <div class="section-header">
      <h1>Materials</h1>
      <button @click="toggleSearchModal">Add Materials</button>
    </div>
    <section>
      <table class="col" v-if="items.length > 0">
        <thead>
          <tr>
            <th v-for="(value, propertyName) in items[0]" :key="propertyName">
              {{propertyName}}
            </th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(item, index) in items" :key="index">
            <th v-for="(value, propertyName) in item" :key="propertyName + item">
              {{propertyName === 'price' ? returnAsCurrency(value) : value}}
            </th>
          </tr>
        </tbody>
      </table>
      <p v-else>You haven't added any materials yet</p>
    </section>
    <div v-if="items" class="total-container">
      <p>{{`Total: £${total}`}}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Materials',
  props: {
    items: {
      type: Array,
    },
  },
  computed: {
    total() {
      function quoteTotal(thisTotal, item) {
        return (thisTotal + (item.price.toFixed(2) * item.quantity));
      }
      const total = this.items.reduce(quoteTotal, 0).toFixed(2);
      return total;
    },
  },
  methods: {
    returnAsCurrency(val) {
      return val.toFixed(2);
    },
    toggleSearchModal() {
      this.$emit('toggleSearchModal');
    },
  },
};
</script>
