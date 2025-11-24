<script setup>
const props = defineProps({
  onSelectGenerator: {
    type: Function,
    required: true
  },
  selectedItem: {
    type: String,
    default: ''
  }
})

function selectGenerator(generator) {
  props.onSelectGenerator(generator)
}

</script>

<template>
  <nav class="generatorSelector__container">
    <div class="generatorSelector__item" @click="selectGenerator('descriptiveAnimals')"
      :class="{ navBar__isSelected: selectedItem == 'descriptiveAnimals' }">Descriptive animals</div>
    <div class="generatorSelector__item" @click="selectGenerator('stringGenerator')"
      :class="{ navBar__isSelected: selectedItem == 'stringGenerator' }">String generator</div>
  </nav>
</template>

<style lang="scss" scoped>
.generatorSelector__container {
  display: flex;
  gap: 16px;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 100px;

  .generatorSelector__item {
    cursor: pointer;
    text-decoration: none;
    color: black;
    background: linear-gradient(#000000, #000000) left bottom / 0 2px no-repeat;
    transition: background-size 0.3s ease;

    &:hover {
      background-size: 100% 2px;
    }
  }

  .navBar__isSelected {
    font-weight: bold;
    background-size: 100% 2px;
  }
}
</style>
