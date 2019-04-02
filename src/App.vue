<template>
    <v-app>
        <v-toolbar app>
            <v-toolbar-title class="headline text-uppercase">
                <span class="font-weight-light">UDC</span>
            </v-toolbar-title>
            <v-spacer></v-spacer>

        </v-toolbar>

        <v-content>
            <MainView/>
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
        data() {
            return {
                //
            }
        }
    }
</script>
