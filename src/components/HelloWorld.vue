<template>
  <div>
    <h1>#金曜GUI</h1>
    <h2>SVG FilterEffectsを学ぶ</h2>

    <div class="control">
      <label>
        seed
        <input v-model="seed" type="range" min="0" max="100" step="1" />
        {{ seed }}
      </label>
      <label>
        freq
        <input v-model="freq" type="range" min="0.001" max="0.2" step="any" />
        {{ freq }}
      </label>
      <label>
        octaves
        <input v-model="octaves" type="range" min="0" max="5" step="1" />
        {{ octaves }}
      </label>
      <label>
        scale
        <input v-model="scale" type="range" min="1" max="100" step="any" />
        {{ scale }}
      </label>
      <label>
        useDisplacement
        <input v-model="useDisplacement" type="checkbox" />
        {{ useDisplacement }}
      </label>
    </div>

    <h3>filtered</h3>
    <svg ref="svgRef" width="400" viewBox="0 0 400 400">
      <filter id="filter1">
        <feTurbulence
          type="turbulence"
          :baseFrequency="freq"
          :numOctaves="octaves"
          result="turbulence"
          :seed="seed"
        />
        <feDisplacementMap
          v-if="useDisplacement"
          in2="turbulence"
          in="SourceGraphic"
          :scale="scale"
          xChannelSelector="R"
          yChannelSelector="G"
        />
      </filter>
      <image
        href="@/assets/cat.jpg"
        filter="url(#filter1)"
        height="400"
        width="400"
      />
    </svg>

    <h3>original</h3>
    <img src="@/assets/cat.jpg" alt="" />
  </div>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  data() {
    return {
      seed: 0,
      freq: 0.05,
      octaves: 2,
      scale: 50,
      useDisplacement: true,
    }
  },
})
</script>

<style scoped lang="scss">
.control {
  display: flex;
  flex-direction: column;
  > * {
    display: flex;
    flex-direction: column;
  }
}
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
