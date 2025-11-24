<script setup>
import { onMounted, ref } from 'vue'
import { getDescriptiveAnimal, getRandomString } from './helpers/generators'
import GeneratorSelector from './GeneratorSelector.vue'

const generatorMap = {
  descriptiveAnimals: getDescriptiveAnimal,
  stringGenerator: getRandomString
}

const randomizedString = ref("")
const activeGenerator = ref('descriptiveAnimals')
const separator = ref(' ')

onMounted(() => generateString())

function generateString() {
  randomizedString.value = generatorMap[activeGenerator.value]().join(separator.value)
}

function changeGenerator(generator) {
  if (generator != activeGenerator.value) {
    activeGenerator.value = generator
    generateString()
  }
}
</script>

<template>
  <div class="theGenerator__container">
    <div class="theGenerator__options">
      <div class="theGenerator__generatorSelector">
        <generator-selector :on-select-generator="changeGenerator" :selected-item="activeGenerator" />
      </div>
    </div>
    <div class="theGenerator__input">
      <div class="theGenerator__leftColumn">
        <Transition mode="out-in">
          <span class="theGenerator__string" :key="randomizedString">
            {{ randomizedString }}
          </span>
        </Transition>
      </div>
      <div class="theGenerator__rightColumn">
        <button @click="generateString">Randomize</button>
      </div>
    </div>
  </div>
</template>

<style scoped lang="scss">
.theGenerator__container {
  width: 100%;

  .theGenerator__input {
    display: flex;
    gap: 20px;
    align-items: center;

    .theGenerator__leftColumn {
      flex: 1;
      text-align: right;

      font-size: 1.1rem;

      .theGenerator__string {
        padding: 8px;
      }
    }

    .theGenerator__rightColumn {
      flex: 1;
      text-align: left;

      button {
        padding: 8px;
        border-radius: 25px;
        background-color: rgb(168, 206, 255);
        border: solid 1px hsl(214, 100%, 60%);
        transition: background-color 0.3s;

        &:hover {
          cursor: pointer;
          background-color: hsl(214, 100%, 60%);
        }
      }
    }
  }
}

.v-enter-active{
  animation: bounce-in 1s ;
}

.v-enter-to{
  animation: bounce-in 1s ;
}

@keyframes bounce-in {
  0% {
    background-color: none;
  }
  50% {
    background-color: hsl(214, 100%, 90%);
  }
  100% {
    background-color: none;
  }
}

@media only screen and (min-width: 768px) {}
</style>
