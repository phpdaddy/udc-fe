<template>
    <v-app>
        <v-toolbar app>
            <v-toolbar-title class="headline text-uppercase">
                <span class="font-weight-light">UDC</span>
            </v-toolbar-title>
            <v-spacer></v-spacer>


            <v-tabs
                    centered
                    color="transparent"
                    v-model="activeTab">
                <v-tab ripple>
                    Keywords
                </v-tab>
                <v-tab ripple>
                    Annotation
                </v-tab>
                <v-tab ripple>
                    Admin
                </v-tab>
            </v-tabs>
        </v-toolbar>
        <v-content>
            <MainView :activeTab="activeTab"/>
        </v-content>
    </v-app>
</template>

<script>
    import MainView from './components/MainView'

    export default {
        name: 'App',
        components: {
            MainView,
        },
        data: () => ({
            activeTab: null,
        })
    }
</script>

<style scoped>

    .v-toolbar .v-tabs {
        width: auto;
    }

    .logo {
        height: 90%;
        margin-left: 10px;
    }
</style>
