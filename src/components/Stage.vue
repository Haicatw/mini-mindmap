<template>
  <v-card id="konva-stage">
    <v-stage ref="stage" :config="configKonva" @wheel="zoomingStage">
      <v-layer>
        <v-circle :config="configCircle"></v-circle>
      </v-layer>
    </v-stage>
  </v-card>
</template>

<script>
export default {
  data: () => ({
    configKonva: { width: 0, height: 0, draggable: true },
    configCircle: {
      x: 100,
      y: 100,
      radius: 70,
      fill: 'red',
      stroke: 'black',
      strokeWidth: 4
    },
    zoomingSensitivity: 1.5
  }),
  computed: {},
  mounted() {
    const selector = '#konva-stage'
    const selectedStage = document.querySelector(selector).parentElement
    this.configKonva.width =
      selectedStage.clientWidth -
      window
        .getComputedStyle(selectedStage, null)
        .getPropertyValue('padding-left')
        .match(/\d+/)[0] -
      window
        .getComputedStyle(selectedStage, null)
        .getPropertyValue('padding-right')
        .match(/\d+/)[0]
    this.configKonva.height =
      selectedStage.clientHeight -
      window
        .getComputedStyle(selectedStage, null)
        .getPropertyValue('padding-top')
        .match(/\d+/)[0] -
      window
        .getComputedStyle(selectedStage, null)
        .getPropertyValue('padding-bottom')
        .match(/\d+/)[0]
  },
  methods: {
    zoomingStage(event) {
      // console.log(event)
      event.evt.preventDefault()
      var oldScale = this.$refs.stage.getNode().scaleX()

      var pointer = this.$refs.stage.getNode().getPointerPosition()

      var mousePointTo = {
        x: (pointer.x - this.$refs.stage.getNode().x()) / oldScale,
        y: (pointer.y - this.$refs.stage.getNode().y()) / oldScale
      }

      var newScale =
        event.evt.deltaY > 0
          ? oldScale * this.zoomingSensitivity
          : oldScale / this.zoomingSensitivity

      this.$refs.stage.getNode().scale({ x: newScale, y: newScale })

      var newPos = {
        x: pointer.x - mousePointTo.x * newScale,
        y: pointer.y - mousePointTo.y * newScale
      }
      this.$refs.stage.getNode().position(newPos)
      this.$refs.stage.getNode().batchDraw()
    }
  }
}
</script>

<style></style>
