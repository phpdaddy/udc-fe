<template>
    <div>
        <div v-for="item in allItems">
            {{ item.id +'. ('+item.code +') '+item.fullPath}}
            <v-textarea v-model="item.keywords"
                    @input="changeKeywords"></v-textarea>
        </div>
    </div>
</template>

<script>

    import axios from 'axios';

    export default {
        mounted() {
            axios
                .get('http://localhost:8001/rest/categories')
                .then(response => (this.allItems = response.data))

        },
        methods: {
            changeKeywords() {
                let transformedRequest = this.allItems.map(i => ({id: i.id, keywords: i.keywords}));
                console.log(transformedRequest)
                axios
                    .post('http://localhost:8001/rest/categories', transformedRequest)
                    .then();
            }
        },
        data: () => ({
            allItems: [],
        }),
    }
</script>

<style>
</style>
