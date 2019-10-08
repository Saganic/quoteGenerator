<template>
  <div class="quote">
    <div class="section-header">
      <h1>Create new quote request</h1>
    </div>
    <section>
      <div class="col">
        <label>Job Number</label>
        <input type="text" v-model="quote.jobNumber" placeholder="Number" required/>
      </div>
      <div class="col">
        <label>Due Date</label>
        <input type="date" v-model="quote.dueDate" placeholder="Select date" required/>
      </div>
    </section>

    <!--Materials Section-->
    <Materials
      :items="quote.items"
      v-on:toggleSearchModal="materialSearchModalShow = !materialSearchModalShow"
    />

    <!--Material Search Modal-->
    <MaterialsSearchModal
      :availableItems="availableItems"
      v-show="materialSearchModalShow"
      v-on:toggleSearchModal="materialSearchModalShow = !materialSearchModalShow"
      v-on:addItemToQuote="addItemToQuote"
    />


    <!--Debug Window-->
    <Debug :data="quote" v-show="debug"/>
  </div>
</template>

<script>

import Debug from './Debug.vue';
import Materials from './Materials.vue';
import MaterialsSearchModal from './MaterialSearchModal.vue';
import availableItems from '../../data/output';

export default {
  name: 'Quote',
  components: {
    Debug,
    Materials,
    MaterialsSearchModal,
  },
  data() {
    return {
      debug: false,
      materialSearchModalShow: false,
      // availableItems: [
      //   {
      //     code: 0,
      //     name: 'My Item',
      //     price: 3.00,
      //   },
      //   {
      //     code: 1,
      //     name: 'My other item',
      //     price: 4.50,
      //   },
      //   {
      //     code: 2,
      //     name: 'My third item',
      //     price: 9.95,
      //   },
      // ],
      availableItems,
      quote: {
        jobNumber: null,
        dueDate: '',
        items: [],
      },
    };
  },
  methods: {
    addItemToQuote(item) {
      if (this.quote.items.some(itemInQuote => itemInQuote.code === item.code)) {
        /* vendors contains the element we're looking for */
        this.quote.items.map((itemInQuote) => {
          if (itemInQuote.code === item.code) {
            // eslint-disable-next-line no-param-reassign
            itemInQuote.quantity += 1;
          }
          return itemInQuote;
        });
      } else {
        this.quote.items.push({
          code: item.code,
          name: item.name,
          quantity: 1,
          price: item.price,
        });
      }
    },
  },
};
</script>
