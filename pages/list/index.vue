<template lang="">
    <MyHeader></MyHeader>
    <div class="container">
        <div class="row">
            <div class="col-12" v-for="todo in source">
                <h1>Name：{{ todo.name }}</h1>
                <h2>City：{{ todo.city }}</h2>
            </div>
        </div>
    </div>
</template>
<script>
import axios from 'axios';

export default {
    data() {
        return {
            source: [],
        };
    },

    computed: {
        isLoading() {
            return this.source.length;
        },
    },

    created() {
        axios
            .get('https://mocki.io/v1/d4867d8b-b5d5-4a48-a4ab-79131b5809b8')
            .then((res) => (this.source = res.data));
    },
};
</script>
<style lang=""></style>
