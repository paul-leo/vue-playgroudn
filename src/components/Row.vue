<template>
  <tr>
    <td class="text-center">{{ random }}</td>
    <td
      v-for="i in 100"
      :key="i"
      style="visibility: hidden; display: none;"
      class="hidden"
    >
      {{ i - 1 }}
    </td>
  </tr>
</template>

<script lang="ts">
import { defineComponent, PropType } from 'vue';

export default defineComponent({
  name: 'Row',
  props: {
    random: {
      type: Number as PropType<number>,
      required: true,
    },
  },
});
</script>

<style scoped>
.hidden {
  visibility: hidden;
  display: none;
}
</style>
