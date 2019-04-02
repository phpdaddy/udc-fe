<template>
    <div>
        <div v-for="item in allItems" :class="noChildren(item)">
            <strong>{{ item.id +'. ('+item.code +') '+item.name}}</strong>
            <br/><strong style="font-style: italic">Full path:</strong> {{item.fullPath}}
            <br/><strong style="font-style: italic">Parent:</strong> {{ item.parentId || 'N/A'}}
            <br/><strong style="font-style: italic">
            {{ (item.children && item.children.length>0 ? ('Subtopics: ' + item.children) : 'No children')}}</strong>
            <ChipTagsInputText v-model="item.keywords"
                               label="Keywords"
                               @input="changeKeywords"></ChipTagsInputText>
        </div>
    </div>
</template>

<script>

    import axios from 'axios';
    import ChipTagsInputText from "./ChipTagsInputText";

    export default {
        mounted() {
            axios
                .get('http://localhost:8001/rest/categories')
                .then(response => (this.allItems = response.data.map(i => ({
                        ...i,
                        keywords: i.keywords && i.keywords.split(',')
                    })
                )))

        },
        methods: {
            noChildren(item) {
                return item.children && item.children.length > 0 ? '' : 'noChildren';
            },
            changeKeywords() {
                let transformedRequest = this.allItems.map(i => ({
                    id: i.id,
                    keywords: i.keywords && i.keywords.join(',')
                }));

                axios
                    .post('http://localhost:8001/rest/categories', transformedRequest)
                    .then();
            }
        },
        data: () => ({
            allItems: [],
        }),
        components: {
            ChipTagsInputText
        }
    }
</script>

<style>
    .noChildren {
        background-color: aliceblue;
    }
</style>
