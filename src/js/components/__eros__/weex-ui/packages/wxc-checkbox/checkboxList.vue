<!-- CopyRight (C) 2017-2022 Alibaba Group Holding Limited. -->
<template>
  <div>
    <wxc-checkbox v-for="(item,i) in list"
                  v-bind="item"
                  v-on:wxcCheckBoxItemChecked="wxcCheckBoxItemChecked"
                  :key="i"></wxc-checkbox>
  </div>
</template>

<style scoped>

</style>

<script>
  import WxcCheckbox from './index.vue';
  export default {
    components: { WxcCheckbox },
    props: {
      list: {
        type: Array,
        default: () => ([])
      }
    },
    data: () => ({
      checkedList: []
    }),
    created () {
      const { list } = this;
      if (list && list.length > 0) {
        list.forEach((item, i) => {
          item.checked && this.checkedList.push(item.value);
        });
      }
    },
    methods: {
      wxcCheckBoxItemChecked (e) {
        if (e.checked) {
          this.checkedList.push(e.value);
        } else {
          var index = this.checkedList.indexOf(e.value);
          this.checkedList.splice(index, 1);
        }
        this.$emit('wxcCheckBoxListChecked', { checkedList: this.checkedList })
      }
    }
  }
</script>
