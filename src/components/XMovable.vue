<template>
  <div>
    <div v-for="item in valueCopy"
         :key="item.key || item.value"
         draggable="true"
         style="width: min-content;"
         @dragstart="handleDragStart(item)"
         @dragover="handleDragOver(item, $event)">
      <slot :item="item"></slot>
    </div>
  </div>
</template>

<script>
  export default {
    name: "XMovable",
    props: {
      value: Array
    },
    data() {
      return {
        curItem: null,
        curIndex: null,
        valueCopy: []
      };
    },
    watch: {
      'value': {
        immediate: true,
        handler(val) {
          this.valueCopy = val;
          this.$emit('input', val);
        }
      }
    },
    methods: {
      handleDragStart(item) {
        this.curItem = item;
        this.curIndex = this.value.indexOf(item);
      },
      handleDragOver(item, event) {
        event.preventDefault();
        let { value, curIndex } = this;
        let index = this.value.indexOf(item);

        if (index < this.curIndex) {
          this.valueCopy = [...value.slice(0, index), this.curItem, ...value.slice(index, curIndex), ...value.slice(curIndex + 1, value.length)];
          console.log('1', this.value);
        } else if (index > this.curIndex) {
          this.valueCopy = [...value.slice(0, curIndex), ...value.slice(curIndex + 1, index + 1), this.curItem, ...value.slice(index + 1, value.length)];
          console.log('2', this.value);
        }
      }
    }
  }
</script>

<style scoped>

</style>
