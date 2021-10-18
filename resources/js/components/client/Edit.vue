<template>
    <div class="row">
        <div class="col-8">
            <div class="card">
                <div class="card-header">
                    <h4>Update client</h4>
                </div>
                <div class="card-body">
                    <form @submit.prevent="update">
                        <div class="row">
                            <div class="col-12 mb-2">
                                <div class="form-group">
                                    <label>Nom</label>
                                    <input type="text" class="form-control" v-model="client.name">
                                </div>
                            </div>
                            <div class="col-12 mb-2">
                                <div class="form-group">
                                    <label>Téléphone</label>
                                    <input type="text" class="form-control" v-model="client.phone">
                                </div>
                            </div>
                              <div class="col-12 mb-2">
                                <div class="form-group">
                                    <label>Email</label>
                                    <input type="text" class="form-control" v-model="client.email">
                                </div>
                            </div>
                              <div class="col-12 mb-2">
                                <div class="form-group">
                                    <label>Adresse</label>
                                    <input type="text" class="form-control" v-model="client.address">
                                </div>
                            </div>
                              <div class="col-12 mb-2">
                                <div class="form-group">
                                    <label>Date de naissance</label>
                                    <input type="date" class="form-control" v-model="client.birthday">
                                </div>
                            </div>
                            <div class="col-12">
                                <button type="submit" class="btn btn-primary">Modifier</button>
                            </div>
                        </div>                        
                    </form>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name:"update-client",
    data(){
        return {
            client:{
                name:"",
                phone:"",
                email:"",
                address:"",
                birthday:"",
                _method:"patch"
            }
        }
    },
    mounted(){
        this.showClient()
    },
    methods:{
        async showClient(){
            await this.axios.get(`/api/client/${this.$route.params.id}`).then(response=>{
                const { name, phone, email, address, birthday } = response.data
                this.client.name = name
                this.client.phone = phone
                this.client.email = email
                this.client.address = address
                this.client.birthday = birthday
            }).catch(error=>{
                console.log(error)
            })
        },
        async update(){
            await this.axios.post(`/api/client/${this.$route.params.id}`,this.client).then(response=>{
                this.$router.push({name:"<ClientList>"})
            }).catch(error=>{
                console.log(error)
            })
        }
    }
}
</script>