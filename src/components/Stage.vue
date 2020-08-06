<template>
  <v-card id="konva-stage">
    <v-stage :config="configKonva"> </v-stage>
  </v-card>
</template>

<script>
export default {
  data: () => ({
    configKonva: { width: 0, height: 0 }
  }),
  computed: {},
  mounted() {
    const selector = '#konva-stage'
    const selectedStage = document.querySelector(selector).parentElement
    this.configKonva.width = selectedStage.clientWidth
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
  }
}
</script>

<style></style>
