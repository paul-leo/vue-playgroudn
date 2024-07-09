<template>
  <table>
    <Row v-for="item in list" :key="item" :random="item" />
  </table>
</template>

<script lang="ts">
import { defineComponent, PropType } from 'vue';
import Row from './Row.vue'; // 确保路径正确

export default defineComponent({
  name: 'Table',
  components: {
    Row,
  },
  props: {
    list: {
      type: Array as PropType<number[]>,
      required: true,
    },
  },
  mounted() {
    console.log('Table render');
  }
});
</script>

<style scoped>
/* 可以在这里引入 index.css 或者直接写样式 */
table,
tr,
td {
    text-align: center;
}
table {
  margin: 0 auto;
}

</style>
