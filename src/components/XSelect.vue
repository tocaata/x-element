<template>
  <div class="dropdown" :class="{ 'is-active': active, 'multiple-select': multiple }">
    <div class="dropdown-trigger">
      <p class="control has-icons-right" ref="control">
        <input ref="input" class="input"
               type="text"
               :value="innerValue"
               :placeholder="placeholder"
               @click.stop="handleInputClick"
               readonly
        />
        <span class="icon is-small is-right" @click.stop="handleDelete">
          <i v-if="icon === 'down'" class="fas fa-angle-down"></i>
          <i v-else class="fas fa-times-circle" data-icon></i>
        </span>
      </p>
    </div>
    <div class="dropdown-menu" role="menu">
      <div class="dropdown-content">
        <slot></slot>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'XSelect',
    props: {
      value: [String, Number, Array],
      clearable: Boolean,
      placeholder: String,
      multiple: Boolean
    },
    data() {
      return {
        innerValue: this.value,
        active: false,
        icon: 'down'
      };
    },
    mounted() {
      this.$on('click', (value) => this.handleOptionClick(value));
      if (this.clearable) {
        this.$refs.control.addEventListener('mouseover', (e) => { this.innerValue && (this.icon = 'delete'); });
        this.$refs.control.addEventListener('mouseout', (e) => { this.icon = 'down'; });
      }
      document.addEventListener('click', () => { this.active = false; });
    },
    methods: {
      handleInputClick(event) {
        this.active = !this.active;
      },
      handleDelete(e) {
        if (this.icon === 'delete') {
          this.innerValue = null;
          this.active = false;
        }
      },
      handleOptionClick(value) {
        if (this.multiple) {
          this.innerValue =  this.innerValue || [];
          if (this.innerValue.includes(value)) {
            const index = this.innerValue.indexOf(value);
            this.innerValue.splice(index, 1);
          } else {
            this.innerValue.push(value);
          }
          this.$emit('input', this.innerValue);
        } else {
          this.active = !this.active;
          this.innerValue = value;
          this.$emit('input', this.innerValue);
        }
      }
    }
  }
</script>

<style scoped>
  span.icon {
  }

  input.input {
    z-index: 1;
    width: 12rem;
    cursor: pointer;
    transition: all .3s;
    padding: 0 15px;
  }
</style>
