<template>
  <div
    class="canvas"
    @mousemove="moveBlock"
    @dragover.prevent
    @drop="onDrop"
  >
    <OneBlock
      v-for="(block, index) in blocks"
      :key="index"
      :name="block.name"
      :position="block.position"
    />
  </div>
</template>

<script>
import OneBlock from './OneBlock.vue';

export default {
  name: 'TheCanvas',
  components: {
    OneBlock
  },
  data() {
    return {
      blocks: [], // Array to hold the blocks on the canvas
      currentBlock: null, // Reference to the block being dragged
      startMousePosition: { x: 0, y: 0 } // Initial mouse position for dragging
    };
  },
  methods: {
    moveBlock(event) {
      // Update the position of the currently dragged block
      if (this.currentBlock && this.currentBlock.isDragging) {
        const deltaX = event.clientX - this.startMousePosition.x;
        const deltaY = event.clientY - this.startMousePosition.y;
        this.currentBlock.position.x += deltaX;
        this.currentBlock.position.y += deltaY;
        this.startMousePosition = { x: event.clientX, y: event.clientY };
      }
    },
    isColliding(blockA, blockB) {
      const blockWidth = 100;
      const blockHeight = 50;
      return (
        blockA.position.x < blockB.position.x + blockWidth &&
        blockA.position.x + blockWidth > blockB.position.x &&
        blockA.position.y < blockB.position.y + blockHeight &&
        blockA.position.y + blockHeight > blockB.position.y
      );
    },
    onDrop(event) {
      // Get the block name from the drag data
      const blockName = event.dataTransfer.getData('text/plain');
      // Calculate the position of the new block based on the drop coordinates
      const position = { x: event.clientX, y: event.clientY };
      // Define the new block
      const newBlock = { name: blockName, position, isDragging: false };

      // Check if the new block is colliding with any existing blocks
      for (const existingBlock of this.blocks) {
        if (this.isColliding(newBlock, existingBlock)) {
          // Adjust the position of the new block to avoid collision
          // For example, place the new block below the existing block
          newBlock.position.y = existingBlock.position.y + 60;
          break;
        }
      }

      // Add the new block to the canvas
      this.blocks.push(newBlock);
    }
  }
}
</script>

<style scoped>
.canvas {
  /* Define styles for the canvas */
  width: 100%;
  height: 600px;
  border: 1px solid #ddd;
  position: relative;
}
</style>
