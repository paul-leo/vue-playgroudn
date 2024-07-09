<template>
    <div class="timer-wrap">{{ count }}</div>
</template>

<script lang="ts">
import { defineComponent, ref, onMounted, onBeforeUnmount, watch } from 'vue';

export default defineComponent({
    name: 'CountDown',
    props: {
        count: {
            type: Number,
            required: true,
        },
        onChange: {
            type: Function as unknown as () => (count: number) => void,
            required: true,
        },
    },
    setup(props) {
        const count = ref<string>('');

        const updateCount = () => {
            const now = new Date().getTime();
            const formatter = new Intl.DateTimeFormat('zh-CN', {
                year: 'numeric',
                month: '2-digit',
                day: '2-digit',
                hour: '2-digit',
                minute: '2-digit',
                second: '2-digit',
                hour12: false,
            });
            const formattedTime = formatter.format(now);
            count.value = formattedTime;
            props.onChange(now);
        };

        let timer: number;

        onMounted(() => {
            timer = window.setInterval(updateCount, 1000);
        });

        onBeforeUnmount(() => {
            clearInterval(timer);
        });

        watch(
            () => props.count,
            () => {
                updateCount();
            }
        );

        return {
            count,
        };
    },
});
</script>

<style scoped>
.timer-wrap {
  font-size: 40px;
  text-align: center;
  padding: 10px;
}
</style>
