<template>
    <div class="block" @mousedown="startDrag" @mouseup="endDrag">
      {{ name }}
    </div>
  </template>
  
  <script>
  export default {
    name: 'OneBlock',
    props: {
      name: String
    },
    data() {
      return {
        isDragging: false, // Indicates whether the block is being dragged
        position: { x: 0, y: 0 } // Current position of the block
      };
    },
    methods: {
      startDrag(event) {
        this.isDragging = true;
        // Record the initial mouse position
        this.startMousePosition = { x: event.clientX, y: event.clientY };
      },
      endDrag() {
        this.isDragging = false;
      }
    }
  }
  </script>
  
  <style scoped>
  .block {
    /* Define styles for the block */
    width: 100px;
    height: 50px;
    background-color: #f0f0f0;
    border: 1px solid #ddd;
    cursor: move;
    position: absolute;
  }
  </style>
  