<template>
    <div class="col-xs-12 col-sm-6">
        <div v-html="content"></div>

        <ul>
            <li v-for="(item, index) in servers" :key="index" v-show="ulClasse">Server ID: {{item.id}} , Status: {{item.status}}</li>
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
           content:'<p>Server Details are currently not updated</p>',
           ulClasse: true
       }
   },

   created() {
       bus.$on('sendServerToDetails', (value)=>{
           this.servers=[]
           this.servers=this.servers.concat(value)
           this.content='<h3>Servers Updated</h3>'
           this.ulClasse ? this.ulClasse : !this.ulClasse
       })
   },
   methods: {
       resetStatus(){
           
            this.content='<p>Server Details are currently not updated</p>'
            // this.ulClasse? !this.ulClasse : this.ulClasse
            bus.$emit('sendStatusToBus', [
                {id:1, status: 'normal', cssClass:'', isChanged:false},
                {id:2, status: 'normal', cssClass:'', isChanged:false},
                {id:3, status: 'normal', cssClass:'', isChanged:false},
                {id:4, status: 'normal', cssClass:'', isChanged:false},
                {id:5, status: 'normal', cssClass:'', isChanged:false}
                ])
       }
   }
}
</script>

<style>

</style>
