<template>
  <div class="container" id="playground">
    <div class="row justify-content-center no-gutters">
      <div class="col-md-9">
        <div class="row no-gutters">
          <Canvas ref="canvas"/>
        </div>
      </div>
      <!-- <div class="col-md-3 bordered">
        <div class="row no-gutters">
          <Tool
            v-for="(tool, id) of tools"
            @select-tool="currentTool = $event"
            :key="id"
            :name="tool.name"
            :imageUrl="tool.imageUrl"
          />
        </div>
      </div>-->
    </div>
    {{currentTool}}
  </div>
</template>

<script>
import Canvas from './playground/Canvas'
import Tool from './playground/Tool'
import bresenham from '../algorithms/bresenham'
import Circle from '../algorithms/circle'
import Ellipse from '../algorithms/ellipse'
import bezier from '../algorithms/bezier'
import MemoryBuffer from '../algorithms/memory-buffer'
import FloodFill from '../algorithms/floodfill'

export default {
  name: 'Playground',
  components: {
    Canvas,
    Tool
  },
  data: () => ({
    tools: [
      {
        name: 'Line',
        imageUrl: 'http://lorempixel.com/output/nightlife-q-c-200-200-5.jpg',
        algorithmFileUrl: ''
      },
      {
        name: 'Circle',
        imageUrl: 'http://lorempixel.com/output/nightlife-q-c-200-200-5.jpg',
        algorithmFileUrl: ''
      },
      {
        name: 'Line',
        imageUrl: 'http://lorempixel.com/output/nightlife-q-c-200-200-5.jpg',
        algorithmFileUrl: ''
      },
      {
        name: 'Circle',
        imageUrl: 'http://lorempixel.com/output/nightlife-q-c-200-200-5.jpg',
        algorithmFileUrl: ''
      }
    ],
    currentTool: ''
  }),

  methods: {
    setCurrentTool(toolName) {
      this.currentTool = toolName
    }
  },

  mounted() {
    const { canvas } = this.$refs

    const buffer = new MemoryBuffer(canvas.size)

    const ellipse = new Ellipse(buffer, '#0066ff')
    ellipse.draw([25, 35], 15, 8)
    canvas.readMemoryBuffer(buffer)

    const circle = new Circle(buffer, '#800000')
    circle.draw([7, 21], 5)
    canvas.readMemoryBuffer(buffer)

    const flood = new FloodFill(buffer, '#cd4001')
    flood.fill([25, 35])
    canvas.readMemoryBuffer(buffer)

    // flood.setBuffer(ellipseBuffer)
    // flood.fill([25, 35])
    // canvas.readMemoryBuffer(ellipseBuffer, '#ff66ff')

    // const bezierBuffer = bezier(canvas.size, [[40, 22], [29, 21], [40, 36]])
    // canvas.readMemoryBuffer(bezierBuffer, '#ffff00')

    // //Não reutilizar buffers - use bufCopy e copie as formas p/ um
    // //buffer container
    // const lineBuffer1 = bresenham(canvas.size, [45, 45], [16, 15])
    // canvas.readMemoryBuffer(lineBuffer1, '#006600')

    // const lineBuffer2 = bresenham(canvas.size, [41, 22], [41, 46])
    // canvas.readMemoryBuffer(lineBuffer2, '#0000ff')

    // const lineBuffer3 = bresenham(canvas.size, [15, 21], [41, 26])
    // canvas.readMemoryBuffer(lineBuffer3, '#00eedd')

    // const buffers = [lineBuffer1, lineBuffer2, lineBuffer3]
    // const buf = new MemoryBuffer(canvas.size)

    // buffers.forEach(b => buf.bufCopy(b))

    // flood.setBuffer(buf)
    // console.log(JSON.stringify(buf.grid))
    // flood.fill([37, 28])
    // canvas.readMemoryBuffer(buf, '#e4c002')
  }
}
</script>

<style scoped>
.bordered {
  border: 2px solid red;
}
</style>
