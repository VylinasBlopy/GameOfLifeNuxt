<template>
    <div ref="item" class="item" @click="togglePopulate">
        Col : {{ col }}<br />
        Row : {{ row }}
    </div>
</template>

<script>
export default {
    name: "Cell",
    props: {
        col: Number,
        row: Number,
        isGameRun: Boolean,
    },
    methods: {
        resetPopulation() {
            this.$refs.item.classList.remove("populate");
        },
        togglePopulate() {
            if (this.isGameRun) return;

            this.$refs.item.classList.toggle("populate");
        }
    }
}
</script>

<style scoped lang="scss">
.item {
    @apply border p-4 bg-teal-300 select-none;
    @apply hover:bg-teal-500;
    @apply ease-in-out duration-200;

    &.populate {
        @apply bg-teal-700;
        @apply hover:bg-teal-900;
    }
}
</style>