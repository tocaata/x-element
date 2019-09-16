<template>
  <div class="container">
    <div v-for="(item, index) in valueCopy"
         :key="item.key || item.value"
         class="drag-item"
         draggable="true"
         :style="{ width: 'min-content', backgroundColor: item === pickItem ? '#c8ebfb' : '#fff' }"
         @dragstart="handleDragStart(item)"
         @dragenter="handleDragEnter($event, item, index)"
         @dragover="$event.preventDefault()"
         @dragend="handleDragEnd"
         @drop="handleDrop(item)">
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
        pickItem: null,
        pickIndex: null,
        valueCopy: this.value
      };
    },
    watch: {
      value(newValue) {
        // console.log(newValue);
        this.valueCopy = newValue;
      }
    },
    methods: {
      handleDragStart(item) {
        this.pickItem = item;
        this.pickIndex = this.value.indexOf(item);
      },
      handleDragEnter(event, item, putIndex) {
        event.preventDefault();

        // if (item === this.pickItem) return;
        let { value, pickIndex } = this;
        // let putIndex = value.indexOf(item);
        // console.log(value[putIndex].value);

        if (putIndex < this.pickIndex) {
          this.valueCopy = [...value.slice(0, putIndex), this.pickItem, ...value.slice(putIndex, pickIndex), ...value.slice(pickIndex + 1, value.length)];
          // console.log('1', this.value);
        } else if (putIndex > this.pickIndex) {
          this.valueCopy = [...value.slice(0, pickIndex), ...value.slice(pickIndex + 1, putIndex + 1), this.pickItem, ...value.slice(putIndex + 1, value.length)];
          // console.log('2', this.value);
        } else {
          this.valueCopy = this.value;
        }
      },
      handleDrop(curItem) {
        this.pickItem = null;
        this.pickIndex = null;
        this.$emit('input', this.valueCopy);
      },
      handleDragEnd() {
        this.pickItem = null;
        this.pickIndex = null;
      }
    }
  }
</script>

<style scoped>
  .container {
    margin: auto;
    width: min-content;
    cursor: move;
  }

  .drag-item {
    margin: 2px 0;
  }
</style>
