<template>
    <div>
        <label>Date et heure de début du graph</label>
        <form>
            <input type="text" placeholder="DD/MM/AAAA hh:mm" v-model="timeStart">
            <label>Date et heure de fin du graph</label>
            <input type="text" placeholder="DD/MM/AAAA hh:mm" v-model="timeEnd">
        </form>
        <button type="submit" @click="getData(timeStart, timeEnd)">submit</button>
        <line-chart :data="data" />
    </div>
</template>

<script>
    import axios from 'axios';
    export default {
        name: 'graphicDetail',
        data() {
            return {
                data: [],
                errors: [],

                serverId: 1,
                labelIds: [
                        "2",
                        "5",
                        "10",
                        "14"
                    ],
                    timeStart: "04/01/2018 00:01",
                    timeEnd: "04/01/2018 01:11"

            }
        },

        mounted(){
        },

        methods:{
            getData: function(timeStart, timeEnd) {
                this.timeStart = timeStart;
                this.timeEnd = timeEnd;

                axios.post('http://localhost:8080/data',
                    {
                        serverId : this.serverId,
                        labelIds : this.labelIds,
                        timeStart : this.timeStart,
                        timeEnd : this.timeEnd

                    }).then(res => {
                    this.data = res.data;
                }).catch(e => {
                    this.errors.push(e);
                })
            }



        }
    }


</script>

<style>


</style>