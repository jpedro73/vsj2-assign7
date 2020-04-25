<template>
    <div class="container">
        <app-header></app-header>
        <hr>
        <div class="row">
            <AppServers :serverFromApp="servers"></AppServers>
            <app-server-details></app-server-details>
        </div>
        <hr>
        <app-footer></app-footer>
    </div>
</template>

<script>
    import Header from './components/Shared/Header.vue';
    import Footer from './components/Shared/Footer.vue';
    import Servers from './components/Server/Servers.vue';
    import ServerDetails from './components/Server/ServerDetails.vue';
    import {bus} from './main'

    

    export default {
        data() {
            return {
                servers:[
                {id:1, status: 'normal', cssClass:'', isChanged:false},
                {id:2, status: 'normal', cssClass:'', isChanged:false},
                {id:3, status: 'normal', cssClass:'', isChanged:false},
                {id:4, status: 'normal', cssClass:'', isChanged:false},
                {id:5, status: 'normal', cssClass:'', isChanged:false}
                ]
            }
        },
        methods: {
            
        },

        
        components: {
            appHeader: Header,
            AppServers: Servers,
            'app-server-details': ServerDetails,
            'app-footer': Footer
        },

        created(){
            bus.$on('sendStatusToBus', (value)=>{
                this.servers=value
            })
        },
    }
</script>

<style>

</style>
