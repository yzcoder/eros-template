<template>
  <wxc-cell :has-top-border="hasTopBorder"
            v-on:wxcCellDivClick="wxcCellDivClick">
    <text :style="{color:color}"
          class="title-text"
          slot="title">{{title}}</text>
    <image :src="checkIcon"
           slot="value"
           class="checkbox"></image>
  </wxc-cell>
</template>

<style scoped>
  .checkbox {
    width: 48px;
    height: 48px;
  }
  .title-text{
    font-size: 30px;
  }
</style>

<script>
  import WxcCell from '../wxc-cell';
  import { CHECKED, UNCHECKED, CHECKED_DISABLED, UNCHECKED_DISABLED } from './icon.base64.js'
  export default {
    components: { WxcCell },
    props: {
      hasTopBorder: {
        type: Boolean,
        default: false
      },
      title: {
        type: String,
        require: true
      },
      value: {
        type: [String, Number, Object],
        require: true
      },
      disabled: {
        type: Boolean,
        default: false
      },
      checked: {
        type: Boolean,
        default: false
      }
    },
    data: () => ({
      icon: [CHECKED, UNCHECKED, CHECKED_DISABLED, UNCHECKED_DISABLED],
      color: '#3D3D3D',
      innerChecked: false
    }),
    computed: {
      checkIcon () {
        const { icon, disabled, innerChecked } = this;
        if (disabled) {
          return icon[innerChecked ? 2 : 3];
        } else {
          return icon[innerChecked ? 0 : 1];
        }
      }
    },
    created () {
      const { checked, disabled } = this;
      this.innerChecked = checked;
      this.color = checked && !disabled ? '#EE9900' : '#3D3D3D';
    },
    methods: {
      wxcCellDivClick () {
        const { disabled, innerChecked, value } = this;
        if (!disabled) {
          this.innerChecked = !innerChecked;
          this.color = (this.innerChecked ? '#EE9900' : '#3D3D3D');
          this.$emit('wxcCheckBoxItemChecked', { value, checked: this.innerChecked })
        }
      }
    }
  }
</script>
