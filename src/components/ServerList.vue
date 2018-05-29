<template>
    <div>
        <ul>
            <li v-for="OneServer in ServerList">
                <input type="radio" class="radio-button" v-model="OneServer.id">
                {{OneServer.name}}
            </li>
        </ul>
    </div>
</template>

<script>
    import axios from 'axios';
        export default {
            name: 'serverlist',
        data() {
            return {
                ServerList: [],
            OneServer: {
                id: 0,
                name :''
            }
        }

        },


        mounted(){
            this.getServers();
        },

        methods:{
            getServers: function () {

                axios.get('http://127.0.0.1:8080/server')
                    .then(res =>
                        this.ServerList = res.data,
                    ).catch(e => {
                    this.errors.push(e);
                })

            }
        }
    }


</script>

<style>


</style>