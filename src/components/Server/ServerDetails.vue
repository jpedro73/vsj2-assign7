<template>
    <div class="col-xs-12 col-sm-6">
        <div v-html="content"></div>

        <ul>
            <li v-for="(item, index) in servers" :key="index">Server ID: {{item.id}} , Status: {{item.status}}</li>
        </ul>
    </div>

</template>

<script>
import {bus} from '../../main'
export default {
   data() {
       return {
           servers:[],
           content:'<p>Server Details are currently not updated</p>'
       }
   },

   created() {
       bus.$on('sendServerToDetails', (value)=>{
           this.servers=this.servers.concat(value)
           this.content='<h3>Servers Updated</h3>'
       })
   }
}
</script>

<style>

</style>
