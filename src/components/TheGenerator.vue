<script setup>
import { onMounted, ref } from 'vue'
import { getDescriptiveAnimal, getRandomString } from './helpers/generators'
import GeneratorSelector from './GeneratorSelector.vue'

const generatorMap = {
  descriptiveAnimals: getDescriptiveAnimal,
  stringGenerator: getRandomString
}

const randomizedStrings = ref("")
const activeGenerator = ref('descriptiveAnimals')
const separator = ref(' ')

onMounted(() => generateString())

function generateString() {
  randomizedStrings.value = generatorMap[activeGenerator.value]()
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
        <div class="theGenerator__string" v-for="(string, index) in randomizedStrings" :key="index">
          <transition mode="out-in">
            <p :key="string">{{ string.join(separator) }}</p>
          </transition>
        </div>
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

      display: flex;
      flex-direction: column;
      align-items: end;

      text-align: right;
      font-size: 1.1rem;

      .theGenerator__string p{
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

.v-enter-active {
  animation: flash-background 1s;
}

.v-enter-to {
  animation: flash-background 1s;
}

@keyframes flash-background {
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
</style>
