<template>
  <div class="modal" @click.self="toggleSearchModal">
    <div class="modal-inner">
      <div class="section-header">
        <h2>Search Materials</h2>
      </div>
      <section>
        <input
          type="search"
          v-model="searchQuery"
          placeholder="Search materials"
          class="search-box"
        />
      </section>
      <br/>
      <section>
        <table class="col" v-if="availableItems">
          <tr>
            <th v-for="(value, propertyName) in filteredItems[0]" :key="propertyName">
              {{propertyName}}
            </th>
          </tr>
          <tr v-for="(item, index) in filteredItems" :key="index">
            <th v-for="(value, propertyName) in item" :key="propertyName + item">
              {{propertyName === 'price' ? returnAsCurrency(value) : value}}
            </th>
            <th>
              <button @click="addToQuote(item)">Add to quote</button>
            </th>
          </tr>
        </table>
      </section>
    </div>
  </div>
</template>

<script>
export default {
  name: 'MaterialSearchModal',
  props: {
    availableItems: {
      type: Array,
    },
  },
  computed: {
    filteredItems() {
      return this.availableItems.filter((item) => {
        if (item.name.toLowerCase().includes(this.searchQuery.toLowerCase())) {
          return item;
        }
        if (item.code === parseInt(this.searchQuery, 0)) {
          return item;
        }
        return undefined;
      });
    },
  },
  data() {
    return {
      searchQuery: '',
    };
  },
  methods: {
    toggleSearchModal() {
      this.$emit('toggleSearchModal');
    },
    returnAsCurrency(val) {
      return val.toFixed(2);
    },
    addToQuote(item) {
      this.$emit('addItemToQuote', item);
    },
  },
};
</script>
