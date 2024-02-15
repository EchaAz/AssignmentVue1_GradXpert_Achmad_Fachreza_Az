<template>
    <div>
      <h2>Item List</h2>
      <ul>
        <li v-for="(item, index) in items" :key="index">{{ item }}</li>
      </ul>
      <input type="text" v-model="newItem">
      <button @click="addItem">Add Item</button>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        items: ['Item 1', 'Item 2', 'Item 3'],
        newItem: ''
      };
    },
    methods: {
      addItem() {
        if (this.newItem.trim() !== '') {
          this.items.push(this.newItem);
          this.newItem = '';
        }
      }
    }
  };
  </script>
  