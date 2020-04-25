<template>
    <div class="col-xs-12 col-sm-6">
        <ul class="list-group">
            <div v-for="(item, index) in serverFromApp" :key="index">
            <li class="list-group-item"><span :class="item.cssClass">Server #{{ item.id }}, status: {{item.status}}</span>
                
            <button @click="updtLow" :name="item.id">Low</button>
            <button @click="updtCritical" :name="item.id">Critical</button>
            </li>

            </div>
        </ul>
        <button @click="sendServersToBus">Send to Details</button>
    </div>
</template>

<script>
import {bus} from '../../main'
export default {
    props:{
        serverFromApp: {
            type: Array
        }
    },

    data(){
        return {

            updatedResult:[],
            isUpdated:false
            
        }
    },
    methods: {
        updtCritical(e){
            this.serverFromApp[e.target.attributes[1].value-1].status='Critical'
            this.serverFromApp[e.target.attributes[1].value-1].cssClass='red'
            this.serverFromApp[e.target.attributes[1].value-1].isChanged='true'
            this.isUpdated=true
        },

        updtLow(e){
            this.serverFromApp[e.target.attributes[1].value-1].status='Low'
            this.serverFromApp[e.target.attributes[1].value-1].cssClass='blue'
            this.serverFromApp[e.target.attributes[1].value-1].isChanged='true'
            this.isUpdated=true
        },

        sendServersToBus(){
            this.updatedResult=this.serverFromApp.filter((item) => item.isChanged)
            bus.$emit('sendServerToDetails', this.updatedResult)
        }
    },

    
}
</script>

<style scoped>
.red {
    color: red;
}
.blue {
    color: blue;
}



</style>
