<template>
    <div>
      <input type="text" v-model="searchQuery" placeholder="Tìm kiếm" />
      <button @click="search"> <i class="fa-solid fa-magnifying-glass"></i></button>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        searchQuery: "",
      };
    },
    methods: {
      search() {
        this.$emit("search", this.searchQuery);
      },
    },
  };
  </script>
  <style scoped>
  input[type="text"] {
    padding: 5px;
    border: 1px solid gray;
  }
  
  button {
    background-color: blue;
    color: white;
    padding: 5px 10px;
    border: none;
    cursor: pointer;
  }
  
  button:hover {
    background-color: darkblue;
  }
  </style>
  