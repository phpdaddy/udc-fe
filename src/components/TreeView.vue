<template>
    <v-treeview
            :active="active"
            active-class="active"
            activatable
            :open="open"
            :items="items"
            open-on-click></v-treeview>
</template>

<script>

    import axios from 'axios';

    export default {
        mounted() {
            let transform = (list) => {
                return list.map(i => {
                    i.name = i.code + '. ' + (i.name ? i.name : '');
                    i.children = transform(i.children);
                    return i
                });
            };
            axios
                .get('http://localhost:8001/rest/category/all')
                .then(response => (this.allItems = transform(response.data)))

        },
        computed: {
            open() {
                let transform = (list, ids) => {
                    return list.forEach(i => {
                        ids.push(i.id);
                        transform(i.children, ids);
                    });
                };
                let ids = [];
                transform(this.items, ids);
                return ids;
            },
            items() {
                let filterData = (array, id) => array.filter(
                    function iter(i) {
                        var temp;

                        if (!id) {
                            return true;
                        }
                        if (i.id === (id)) {
                            return true;
                        }
                        if (!Array.isArray(i.children)) {
                            return false;
                        }
                        temp = i.children.filter(iter);
                        if (temp.length) {
                            i.children = temp;
                            return true;
                        }
                    });
                let arr = JSON.parse(JSON.stringify(this.allItems));
                return filterData(arr, this.search)
            },
            active() {
                return this.search ? [this.search] : [];
            }
        },
        methods: {
            changeKeywords(keywords) {
                if (keywords && keywords.trim()) {
                    axios
                        .get('http://localhost:8001/rest/search/keywords/' + keywords)
                        .then(response => (this.search = response.data.id))
                } else {
                    this.search = null
                }
            },
            changeAnnotation(annotation) {
                if (annotation && annotation.trim()) {
                    axios
                        .get('http://localhost:8001/rest/search/annotation/' + annotation)
                        .then(response => (this.search = response.data.id))
                } else {
                    this.search = null
                }
            }
        },
        data: () => ({
            search: null,
            allItems: [],
            activeTab: null,
        }),
    }
</script>

<style>
    .v-treeview-node__content {
        width: 100%;
    }

    .v-treeview-node__label {
        width: 100%;
    }

    .v-treeview-node__root {
        height: auto;
        padding-top: 5px;
        padding-bottom: 5px;

    }

    .active {
        background-color: rgba(198, 196, 228, 0.78);
    }
</style>
