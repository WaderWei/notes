<template>
    <div id="app">
        <!-- <h1>count: {{count}}</h1>
        <div>
            <button @click="countIncrease">点我</button>
        </div>-->
        <router-view></router-view>
    </div>
</template>

<script>
export default {
    name: "app",
    components: {},
    computed: {
        count() {
            return this.$store.state.count;
        }
    },
    methods: {
        countIncrease() {
            this.$store.commit("countIncrease", 100);
        }
    }
};
</script>

<style>
#app {
    font-family: "Avenir", Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
}
</style>
