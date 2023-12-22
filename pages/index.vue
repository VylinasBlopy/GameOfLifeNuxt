<template>
    <div class="layout">
        <button
            v-if="isGameRun"
            @click="resetGame"
            class="button reset"
            :class="{'disabled:opacity-50': !isGameRun}"
        >
            Reset
        </button>

        <button
            @click="runGame"
            class="button run"
            :class="{'disabled:opacity-50': isGameRun}"
            :disabled="isGameRun"
        >
            Lancer le jeux !
        </button>

        <div class="checkerboard">
            <template v-for="col in colSize" :key="col">
                <div class="column">
                    <template v-for="row in rowSize" :key="row">
                        <div class="row">
                            <Cell ref="cell" :isGameRun="isGameRun" :col="col" :row="row" />
                        </div>
                    </template>
                </div>
            </template>
        </div>
    </div>
</template>

<script>
import Cell from "../components/Cell.vue";

export default {
    components: { Cell },
    data() {
        return {
            colSize: 10,
            rowSize: 10,
            engine: null,
        }
    },
    computed: {
        isGameRun() {
            return this.engine !== null;
        }
    },
    methods: {
        runGame() {
            this.engine = setInterval(() => {
                this.evolvesState();
            }, 1000);
        },
        resetGame() {
            clearInterval(this.engine);
            this.engine = null;

            this.$refs.cell.forEach(cell => {
                cell.resetPopulation();
            });
        },
        evolvesState() {
            this.$refs.cell.forEach(cell => {
                const { col, row } = cell;

                const neighborsResearched = this.getNeighborsResearched(col, row);

                const countNeighborsPopulate = this.countNeighbors(neighborsResearched);

                // Stop : Go lire le readme
            });
        },
        getNeighborsResearched(col, row) {
            // 1 pour la première col/row because boucle de rendu vue compte à partir de 1 ¯\_(ツ)_/¯
            // considérer que null représente une bordure du plateau
            return {
                topNeighbor: {
                    col,
                    row: (row - 1) > 0 ? row - 1 : null,
                },
                bottomNeighbor: {
                    col,
                    row: (row + 1) < this.rowSize? row + 1 : null,
                },
                leftNeighbor: {
                    col: (col - 1) > 0 ? col - 1 : null,
                    row,
                },
                rightNeighbor: {
                    col: (col + 1) < this.colSize ? col + 1 : null,
                    row
                },
                topLeftNeighbor: {
                    col: (col - 1) > 0 ? col - 1 : null,
                    row: (row - 1) > 0 ? row - 1 : null,
                },
                topRightNeighbor: {
                    col: (col + 1) < this.colSize ? col + 1 : null,
                    row: (row - 1) > 0 ? row - 1 : null,
                },
                bottomLeftNeighbor: {
                    col: (col - 1) > 0 ? col - 1 : null,
                    row: (row + 1) < this.rowSize ? row + 1 : null,

                },
                bottomRightNeighbor: {
                    col: (col + 1) < this.colSize ? col + 1 : null,
                    row: (row + 1) < this.rowSize ? row + 1 : null,
                },
            }
        },
        countNeighborsPopulate(neighborsResearched) {
            let count = 0;

            neighborsResearched.forEach(neighbor => {
                if (neighbor.classList.contains("populate")) {
                    count++;
                }
            });

            return count;
        }
    }
}
</script>

<style lang="scss" scoped>
.layout { // Don't need real clean layout integration for this one page app
    @apply w-screen h-screen bg-slate-600 flex flex-col justify-center items-center;

    .button {
        @apply px-5 py-3 bg-teal-300 rounded-lg shadow-md text-white font-bold;
        @apply hover:bg-teal-500 hover:shadow-xl hover:scale-105;
        @apply ease-in-out duration-200;

        &.run {
            @apply flex justify-center items-center;
        }

        &.reset {
            @apply absolute top-3 right-3;
        }
    }

    .checkerboard {
        @apply flex mt-5 mx-auto text-white overflow-auto max-w-none;

        @layer .column { // Doesn't work with @layer @apply
            @apply first:border-l last:border-r;
        }
    }
}
</style>