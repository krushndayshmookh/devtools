<template>
  <div class="gradients container mx-auto p-4">
    <div class="flex" :style="`height: ${availableHeight}px`">
      <div class="w-1/4 h-full overflow-scroll scrollbar-hidden p-4">
        <div class="grid grid-cols-3 gap-4">
          <div
            v-for="gradient in gradients"
            :key="gradient.id"
            class="card h-24 shadow-md hover:shadow-xl hover:scale-105 hover:rounded-md cursor-pointer transition-all duration-100"
            :style="getGradientStyle(gradient, 'to bottom right')"
            @click="previewState.gradient = gradient"
          ></div>
        </div>
      </div>
      <div class="w-3/4 h-full p-4">
        <div
          class="w-full h-full rounded-lg transition-all duration-200"
          :style="gradientStyle"
        >
          <!-- direction selection dropdown -->
          <div class="">
            <div class="dropdown dropdown-start">
              <div tabindex="0" class="m-2 btn">
                <img
                  :src="
                    directionOptions.find(
                      option => option.value == previewState.direction
                    ).icon
                  "
                  class="w-4 h-auto"
                />
                {{ previewState.direction }}
              </div>
              <ul
                tabindex="0"
                class="p-2 shadow menu dropdown-content bg-base-100 rounded-box w-52"
              >
                <li class="menu-title">
                  <span>Direction</span>
                </li>
                <li>
                  <a
                    class="cursor-pointer"
                    v-for="option in directionOptions"
                    :key="option.value"
                    @click="previewState.direction = option.value"
                  >
                    <img :src="option.icon" class="w-4 h-auto" />
                    {{ option.label }}
                  </a>
                </li>
              </ul>
            </div>

            <!-- gradient code snippet -->

            <div class="dropdown dropdown-start">
              <div tabindex="0" class="m-2 btn">
                <img
                  src="https://img.icons8.com/material-outlined/24/000000/code.png"
                  class="w-4 h-auto"
                />
                CSS
              </div>
              <ul
                tabindex="0"
                class="p-2 shadow menu dropdown-content bg-base-100 rounded-box w-128"
              >
                <li class="menu-title">
                  <span>Code Snippet</span>
                </li>
                <li>
                  <a class="cursor-pointer" @click="copyToClipboard">
                    <pre class="text-sm">{{ codeSnippet }}</pre>
                  </a>
                </li>
              </ul>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, reactive, computed } from 'vue'

import ArrowDL from '@/assets/icons/arrow-down-left.svg'
import ArrowDR from '@/assets/icons/arrow-down-right.svg'
import ArrowUL from '@/assets/icons/arrow-up-left.svg'
import ArrowUR from '@/assets/icons/arrow-up-right.svg'
import ArrowL from '@/assets/icons/arrow-left.svg'
import ArrowR from '@/assets/icons/arrow-right.svg'
import ArrowU from '@/assets/icons/arrow-up.svg'
import ArrowD from '@/assets/icons/arrow-down.svg'
import RotateR from '@/assets/icons/rotate-right.svg'

const availableHeight = computed(() => window.innerHeight - 68 - 16 - 16) // SCREEN - HEADER - PADDING_TOP - PADDING_BOTTOM;\

const previewState = reactive({
  gradient: {
    id: 1,
    name: 'Blue',
    colors: ['#4e54c8', '#8f94fb']
  },
  direction: 'to bottom right'
})

const gradientStyle = computed(() => {
  return {
    backgroundImage:
      previewState.direction == 'radial'
        ? `radial-gradient(${previewState.gradient.colors[0]}, ${previewState.gradient.colors[1]})`
        : `linear-gradient(${previewState.direction}, ${previewState.gradient.colors[0]}, ${previewState.gradient.colors[1]})`
  }
})

const codeSnippet = computed(() => {
  return `.my-gradient {
  background-image: ${gradientStyle.value.backgroundImage};
  background-color: ${previewState.gradient.colors[0]};
}`
})

const copyToClipboard = () => {
  const el = document.createElement('textarea')
  el.value = codeSnippet.value
  document.body.appendChild(el)
  el.select()
  document.execCommand('copy')
  document.body.removeChild(el)
}

const getGradientStyle = (gradient: any, direction: string) => {
  return {
    backgroundImage: `linear-gradient(${direction}, ${gradient.colors[0]}, ${gradient.colors[1]})`
  }
}

const directionOptions = [
  {
    label: 'To Right',
    value: 'to right',
    icon: ArrowR
  },
  {
    label: 'To Left',
    value: 'to left',
    icon: ArrowL
  },
  {
    label: 'To Top',
    value: 'to top',
    icon: ArrowU
  },
  {
    label: 'To Bottom',
    value: 'to bottom',
    icon: ArrowD
  },
  {
    label: 'To Top Right',
    value: 'to top right',
    icon: ArrowUR
  },
  {
    label: 'To Top Left',
    value: 'to top left',
    icon: ArrowUL
  },
  {
    label: 'To Bottom Right',
    value: 'to bottom right',
    icon: ArrowDR
  },
  {
    label: 'To Bottom Left',
    value: 'to bottom left',
    icon: ArrowDL
  },
  {
    label: 'Radial',
    value: 'radial',
    icon: RotateR
  }
]

const gradients = [
  {
    id: 1,
    name: 'Blue',
    colors: ['#4e54c8', '#8f94fb']
  },
  {
    id: 2,
    name: 'Green',
    colors: ['#56ab2f', '#a8e063']
  },
  {
    id: 3,
    name: 'Orange',
    colors: ['#f2994a', '#f2c94c']
  },
  {
    id: 4,
    name: 'Purple',
    colors: ['#614385', '#516395']
  },
  {
    id: 5,
    name: 'Red',
    colors: ['#f85032', '#e73827']
  },
  {
    id: 6,
    name: 'Yellow',
    colors: ['#f6d365', '#fda085']
  },
  {
    id: 7,
    name: 'Light Blue',
    colors: ['#a1c4fd', '#c2e9fb']
  },
  {
    id: 8,
    name: 'Light Green',
    colors: ['#6dd5ed', '#2193b0']
  },
  {
    id: 9,
    name: 'Light Orange',
    colors: ['#ff9a9e', '#fad0c4']
  },
  {
    id: 10,
    name: 'Light Purple',
    colors: ['#cc2b5e', '#753a88']
  },
  {
    id: 11,
    name: 'Light Red',
    colors: ['#ff5f6d', '#ffc371']
  },
  {
    id: 12,
    name: 'Light Yellow',
    colors: ['#ffefba', '#ffffff']
  },
  {
    id: 13,
    name: 'Dark Blue',
    colors: ['#2c3e50', '#3498db']
  },
  {
    id: 14,
    name: 'Dark Green',
    colors: ['#0f0c29', '#302b63']
  },
  {
    id: 15,
    name: 'Dark Orange',
    colors: ['#f857a6', '#ff5858']
  },
  {
    id: 16,
    name: 'Dark Purple',
    colors: ['#141e30', '#243b55']
  },
  {
    id: 17,
    name: 'Dark Red',
    colors: ['#20002c', '#cbb4d4']
  },
  {
    id: 18,
    name: 'Dark Yellow',
    colors: ['#000000', '#e74c3c']
  },
  {
    id: 19,
    name: 'Facebook Messenger',
    colors: ['#00c6ff', '#0072ff']
  },
  {
    id: 20,
    name: 'Green Beach',
    colors: ['#02aab0', '#00cdac']
  },
  {
    id: 21,
    name: 'Intuitive Purple',
    colors: ['#DA22FF', '#9733EE']
  },
  {
    id: 22,
    name: 'Emerald Water',
    colors: ['#348F50', '#56B4D3']
  },
  {
    id: 23,
    name: 'Lemon Twist',
    colors: ['#3CA55C', '#B5AC49']
  },
  {
    id: 24,
    name: 'Monte Carlo',
    colors: ['#CC95C0', '#DBD4B4', '#7AA1D2']
  },
  {
    id: 25,
    name: 'Horizon',
    colors: ['#003973', '#E5E5BE']
  },
  {
    id: 26,
    name: 'Rose Water',
    colors: ['#E55D87', '#5FC3E4']
  },
  {
    id: 27,
    name: 'Frozen',
    colors: ['#403B4A', '#E7E9BB']
  },
  {
    id: 28,
    name: 'Mango Pulp',
    colors: ['#F09819', '#EDDE5D']
  },
  {
    id: 29,
    name: 'Bloody Mary',
    colors: ['#FF512F', '#DD2476']
  },
  {
    id: 30,
    name: 'Aubergine',
    colors: ['#AA076B', '#61045F']
  },
  {
    id: 31,
    name: 'Aqua Marine',
    colors: ['#1A2980', '#26D0CE']
  },
  {
    id: 32,
    name: 'Sunrise',
    colors: ['#FF512F', '#F09819']
  },
  {
    id: 33,
    name: 'Purple Paradise',
    colors: ['#1D2B64', '#F8CDDA']
  }
]
</script>
