<template>
    <div class="col-xs-12 col-sm-6">
        <ul class="list-group">
            <div v-for="(item, index) in serverFromApp" :key="index" :class="cssClass">
            <li class="list-group-item">
                Server #{{ serverFromApp[index].id }}, status: {{serverFromApp[index].status}}
            <button @click="updtLow" :name="serverFromApp[index].id">Low</button>
            <button @click="updtNormal" :name="serverFromApp[index].id">Normal</button>
            <button @click="updtCritical" :name="serverFromApp[index].id">Critical</button>
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

            cssClass:''
            
        }
    },
    methods: {
        updtNormal(e){
            this.serverFromApp[e.target.attributes[1].value-1].status='Normal'
        },
        updtCritical(e){
            this.serverFromApp[e.target.attributes[1].value-1].status='Critical'
            e.target.parentElement.classList.add("red")
        },
        updtLow(e){
            this.serverFromApp[e.target.attributes[1].value-1].status='Low'
            

        },

        sendServersToBus(){
            bus.$emit('sendServerToDetails', this.serverFromApp)
            // console.log(this.serverFromApp)
        }
    }
}
</script>

<style scoped>
.red {
    color: red;
}



</style>
