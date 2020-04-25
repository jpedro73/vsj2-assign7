<template>
    <div class="col-xs-12 col-sm-6">
        <div v-html="content"></div>

        <ul>
            <li v-for="(item, index) in servers" :key="index">Server ID: {{item.id}} , Status: {{item.status}}</li>
        </ul>

        <hr>
        <button @click="resetStatus">Reset to Normal</button>
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
           this.servers=[]
           this.servers=this.servers.concat(value)
           this.content='<h3>Servers Updated</h3>'
       })
   },
   methods: {
       resetStatus(){
           this.servers=[
                {id:1, status: 'normal'},
                {id:2, status: 'normal'},
                {id:3, status: 'normal'},
                {id:4, status: 'normal'},
                {id:5, status: 'normal'}
                ]
            bus.$emit('sendStatusToBus', this.servers)
       }
   },
}
</script>

<style>

</style>
