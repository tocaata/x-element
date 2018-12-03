<template>
  <td>
    <slot :prop="prop"></slot>
  </td>
</template>

<script>
  export default {
    name: "XTableColumn",
    props: ['prop', 'label']
  }
</script>

<style scoped>

</style>
