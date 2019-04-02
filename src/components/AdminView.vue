<template>
    <div>
        <div v-for="item in allItems" :class="noChildren(item)">
            {{ item.id +'. ('+item.code +') '+item.fullPath}}
            {{item.children}}
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
            noChildren(item) {
                return item.children && item.children.length > 0 ? '' : 'noChildren';
            },
            changeKeywords() {
                let transformedRequest = this.allItems.map(i => ({id: i.id, keywords: i.keywords}));

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
    .noChildren {
        background-color: aliceblue;
    }
</style>
