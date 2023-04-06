<template>
    <div class="block-type" draggable="true" @dragstart="onDragStart">
      {{ name }}
    </div>
  </template>
  
  <script>
  export default {
    name: 'BlockType',
    props: {
      name: String
    },
    methods: {
      onDragStart(event) {
        // Set the drag data to the block name
        event.dataTransfer.setData('text/plain', this.name);
      }
    }
  }
  </script>
  
  <style scoped>
  .block-type {
    /* Define styles for the block type */
    padding: 10px;
    margin: 5px;
    background-color: #f0f0f0;
    border: 1px solid #ddd;
    cursor: move;
  }
  </style>
  