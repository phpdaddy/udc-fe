<template>
    <v-container>
        <v-layout
                wrap>

            <v-flex xs12>
                <v-tabs-items v-model="activeTab">
                    <v-tab-item>
                        <v-flex xs12>
                            <v-textarea
                                    v-model="keywords"
                                    @input="changeKeywords"
                            ></v-textarea>
                            <TreeView
                                    ref="treeView1"
                            ></TreeView>
                        </v-flex>

                    </v-tab-item>

                    <v-tab-item>
                        <v-flex xs12>
                            <v-textarea
                                    v-model="annotation"
                                    @input="changeAnnotation"
                            ></v-textarea>
                            <TreeView
                                    ref="treeView2"
                            ></TreeView>
                        </v-flex>

                    </v-tab-item>

                    <v-tab-item>
                        <v-flex xs12>
                            <AdminView></AdminView>
                        </v-flex>
                    </v-tab-item>
                </v-tabs-items>

            </v-flex>
        </v-layout>
    </v-container>
</template>

<script>

    import TreeView from "./TreeView";
    import AdminView from "./AdminView";

    export default {
        data: () => ({
            keywords: null,
            annotation: null,
        }),
        computed: {
            showTreeView() {
                return this.activeTab === 0 || this.activeTab === 1;
            }
        },
        methods: {
            changeKeywords() {
                this.$refs.treeView1.changeKeywords(this.keywords)
            },
            changeAnnotation() {
                this.$refs.treeView2.changeAnnotation(this.annotation)
            }
        },
        components: {TreeView, AdminView},
        props: {
            activeTab: null,
        }
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
