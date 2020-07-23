<template>
  <mindmap
    :nodes="nodes"
    :connections="connections"
    :editable="true"
  />
</template>

<script>
  export default {
    name: 'MindMap',
    props: ['nodes', 'connections', 'editable']
  }
</script>