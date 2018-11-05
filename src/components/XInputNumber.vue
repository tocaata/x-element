<template>
  <div class="columns is-centered">
    <div class="field has-addons" data-container>
      <div class="control">
        <a class="button" @click="minus" :disabled="disabled">
          -
        </a>
      </div>
      <div class="control">
        <input class="input"
               type="text"
               :value="inputValue"
               @change="change"
               :disabled="disabled"
               :name="name"
        />
      </div>
      <div class="control">
        <a class="button" @click="plus" :disabled="disabled">
          +
        </a>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'XInputNumber',
    data() {
      return {
        inputValue: this.value || 0,
        stepValue: this.step || 1
      };
    },
    props: {
      'placeholder': String,
      'value': Number,
      'step': Number,
      'min': Number,
      'max': Number,
      'disabled': Boolean,
      'name': String
    },
    mounted(){
    },

    methods: {
      plus() {
        if (this.disabled) {
          return ;
        }
        if ((this.max !== null && this.max !== undefined) && (this.inputValue + this.stepValue) <= this.max || !this.max === undefined) {
          this.inputValue += this.stepValue;
          this.$emit('input', this.inputValue);
        }
      },
      minus() {
        if (this.disabled) {
          return ;
        }
        if ((this.min !== null && this.min !== undefined) && (this.inputValue - this.stepValue) >= this.min || this.min === undefined) {
          this.inputValue -= this.stepValue;
          this.$emit('input', this.inputValue);
        }
      },
      change(event) {
        this.inputValue = Number.parseFloat(event.target.value);
        this.$emit('input', this.inputValue);
      }
    }
  }
</script>

<style scoped>
  div[data-container] {
    width: 10rem;
  }
</style>
