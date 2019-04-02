<template>
    <v-container>
        <v-layout
                wrap>

            <v-flex xs12>
                <v-tabs
                        v-model="activeTab"
                        color="cyan"
                        dark
                        slider-color="yellow">
                    <v-tab ripple>
                        Keywords
                    </v-tab>
                    <v-tab ripple>
                        Annotation
                    </v-tab>
                    <v-tab ripple>
                        Admin
                    </v-tab>
                    <v-tab-item>
                        <v-flex xs12>
                            <v-textarea
                                    v-model="keywords"
                                    @input="changeKeywords"
                            ></v-textarea>
                        </v-flex>

                    </v-tab-item>

                    <v-tab-item>
                        <v-flex xs12>
                            <v-textarea
                                    v-model="annotation"
                                    @input="changeAnnotation"
                            ></v-textarea>
                        </v-flex>

                    </v-tab-item>
                    <v-tab-item>
                        <AdminView></AdminView>
                    </v-tab-item>
                </v-tabs>

                <TreeView
                        v-if="showTreeView"
                        ref="treeView"
                ></TreeView>
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
            activeTab: null,
        }),
        computed: {
            showTreeView() {
                return this.activeTab === 0 || this.activeTab === 1;
            }
        },
        methods: {
            changeKeywords() {
                this.$refs.treeView.changeKeywords(this.keywords)
            },
            changeAnnotation() {
                this.$refs.treeView.changeAnnotation(this.annotation)
            }
        },
        components: {TreeView, AdminView}
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
