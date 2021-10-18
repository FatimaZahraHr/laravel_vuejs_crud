<template>
    <div class="row">
        <div class="col-12 mb-2 text-end">
            <router-link :to='{name:"clientAdd"}' class="btn btn-primary">Ajouter</router-link>
        </div>
        <div class="col-12">
            <div class="card">
                <div class="card-header">
                    <h4>Client</h4>
                </div>
                <div class="card-body">
                    <div class="table-responsive">
                        <table class="table table-bordered">
                            <thead>
                                <tr>
                                    <th>ID</th>
                                    <th>Nom</th>
                                    <th>Téléphone</th>
                                    <th>Email</th>
                                    <th>Adresse</th>
                                    <th>Date de naissance</th>
                                    <th>Actions</th>
                                </tr>
                            </thead>
                            <tbody v-if="clients.length > 0">
                                <tr v-for="(client,key) in clients" :key="key">
                                    <td>{{ client.id }}</td>
                                    <td>{{ client.name }}</td>
                                    <td>{{ client.phone }}</td>
                                    <td>{{ client.email }}</td>
                                    <td>{{ client.address }}</td>
                                    <td>{{ client.birthday }}</td>
                                    <td>
                                        <router-link :to='{name:"clientEdit",params:{id:client.id}}' class="btn btn-success">Editer</router-link>
                                        <button type="button" @click="deleteClient(client.id)" class="btn btn-danger">Supprimer</button>
                                    </td>
                                </tr>
                            </tbody>
                            <tbody v-else>
                                <tr>
                                    <td colspan="4" align="center">Aucun client trouvé.</td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name:"clients",
    data(){
        return {
            clients:[]
        }
    },
    mounted(){
        this.getClients()
    },
    methods:{
        async getClients(){
            await this.axios.get('/api/client').then(response=>{
                this.clients = response.data
            }).catch(error=>{
                console.log(error)
                this.clients = []
            })
        },
        deleteClient(id){
            if(confirm("Vous êtes sûre vous voulez supprimer ce client ?")){
                this.axios.delete(`/api/client/${id}`).then(response=>{
                    this.getClients()
                }).catch(error=>{
                    console.log(error)
                })
            }
        }
    }
}
</script>