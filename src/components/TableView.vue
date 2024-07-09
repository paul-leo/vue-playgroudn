<template>
    <div>
        <!-- 使用 Suspense 组件来懒加载 LagRadar -->
        <div id="lagWrap"></div>
        <CountDown :count="count" @change="handleCountChange" />
        <Table :list="list"></Table>
    </div>
</template>

<script lang="ts">
import { defineComponent, ref, onMounted, onUnmounted } from 'vue';
import CountDown from './Timer.vue'; // 确保路径正确
import Table from './Table.vue'; // 确保路径正确
import LagRadar from '@gaearon/lag-radar'; // 确保路径正确
// 假设我们有一个类似的 Vue 组件 `vue-lag-radar`
// const LagRadar = defineAsyncComponent(() => import('vue-lag-radar'));

export default defineComponent({
    name: 'TableView',
    components: {
        CountDown,
        Table,
    },
    setup() {
        const count = ref(0);
        const nodes = 1000;
        const list = ref<number[]>(
            Array.from({ length: nodes }, () => Math.floor(Math.random() * 100))
        );

        const handleCountChange = (newCount: number) => {
            count.value = newCount;
        };
        let lagRadar: any;
        onMounted(() => {
            const lagWrap = document.getElementById('lagWrap');
            lagRadar = LagRadar({
                frames: 50, // number of frames to draw, more = worse performance
                speed: 0.0017, // how fast the sweep moves (rads per ms)
                size: 300, // outer frame px
                inset: 3, // circle inset px
                parent: lagWrap, // DOM node to attach to
            });
        });
        onUnmounted(() => {
            lagRadar();
        });
        return {
            count,
            list,
            handleCountChange,
        };
    },
});
</script>

<style scoped>
/* 在这里添加样式 */
#lagWrap{
  width: 300px;
  height: 320px;
}
</style>
