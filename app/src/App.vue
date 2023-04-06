<template>
  <div class="app-container">
    <TheCanvas ref="canvasRef" />
    <div class="block-types-container">
      <BlockType
        v-for="(blockType, index) in blockTypes"
        :key="index"
        :name="blockType.name"
      />
    </div>
  </div>
</template>

<script>
import TheCanvas from './components/TheCanvas.vue';
import BlockType from './components/BlockType.vue';

export default {
  components: {
    TheCanvas,
    BlockType
  },
  data() {
    return {
      blockTypes: [
        { name: 'openAi' },
        { name: 'customCode' }
      ]
    };
  }
}
</script>

<style scoped>
.app-container {
  display: flex;
}

.block-types-container {
  /* Define styles for the block types container */
  padding: 10px;
  margin-left: 20px;
  border: 1px solid #ddd;
  width: 150px;
}

</style>
