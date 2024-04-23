<template>
  <h2>CSS3 Perspective Playground</h2>
  <main>
    <section class="settings">
      <div class="settings-container">
        <label>color</label>
        <input v-model="color" type="color" value="#8d81f3"/>

        <label>border radius: {{ borderRadius }}px; </label>
        <input v-model="borderRadius" type="range" min="0" max="100"/>

        <label>rotateX: {{ rotateX }}deg; </label>
        <input v-model="rotateX" type="range" min="-180" max="180"/>

        <label>rotateY: {{ rotateY }}deg; </label>
        <input v-model="rotateY" type="range" min="-180" max="180"/>

        <label>rotateZ: {{ rotateZ }}deg; </label>
        <input v-model="rotateZ" type="range" min="-180" max="180"/>

        <button @click.prevent="reset" type="button">Reset</button>
        <button @click.prevent="copy" type="button">Copy</button>
      </div>
    </section>
    <section class="output">
      <div class="box-container" :style="test">
        <div class="box" :style="box"></div>
      </div>
    </section>
  </main>
  <css-doodle>
    :doodle {
    @grid: 1x3 / 100vmax;
    position: absolute;
    top: 0; left: 0;
    z-index: 0;
    }

    @size: 100% 150%;
    position: absolute;

    background: @m(100, (
    linear-gradient(transparent, @p(
    #FFFDE1@repeat(2, @p([0-9a-f])),
    #FB3569@repeat(2, @p([0-9a-f]))
    ))
    @r(0%, 100%) @r(0%, 100%) /
    @r(1px) @r(23vmin)
    no-repeat
    ));

    will-change: transform;
    animation: f 50s linear calc(-50s / @size() * @i()) infinite;
    @keyframes f {
    from { transform: translateY(-100%) }
    to { transform: translateY(100%) }
    }
  </css-doodle>
</template>
<script>
import '@/assets/css-doodle.js'

export default {
  data: () => ({
    color: '#8d81f3',
    borderRadius: 0,
    rotateX: 0,
    rotateY: 0,
    rotateZ: 0,
  }),
  computed: {
    box() {
      return {
        transform: `
          rotateX(${this.rotateX}deg)
          rotateY(${this.rotateY}deg)
          rotateZ(${this.rotateZ}deg)
        `,
        'background-color': `
          ${this.color}
        `,
        'border-radius': `
          ${this.borderRadius}px
        `
      }
    }
  },
  methods: {
    reset() {
      this.color = '#8d81f3';
      this.borderRadius = 0;
      this.rotateX = 0;
      this.rotateY = 0;
      this.rotateZ = 0;
    },
    async copy() {
      let text = `transform: rotateX(${this.rotateX}deg) rotateY(${this.rotateY}deg) rotateZ(${this.rotateZ}deg);\n`
      text += `background-color: ${this.color};\n`
      text += `border-radius: ${this.borderRadius};\n`
      await navigator.clipboard.writeText(text)
      alert('style Copied to clipboard')
    }
  }
}
</script>
<style lang="scss">
@import "src/assets/main.css";
</style>
