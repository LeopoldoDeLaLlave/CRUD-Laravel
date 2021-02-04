<template>
    <div class="card card-default">
        <div class="card-heading">¿Qúe quieres anotar?</div>
        <div class="card-body">
            <form action="" @submit.prevent="newNote()">
                <div class="form-group">
                    <label for="note">Nota:</label>
                    <input type="text" class="form-control" name="note" v-model="description">
                </div>
                <button type="submit" class="btn btn-primary">
                    Subir nota
                </button>
            </form>
        </div>
    </div>
</template>

<script>
    export default {

        data() {
            return{
                description:""
            }
        },
        methods:{
            newNote(){

                const params ={
                    description: this.description 
                }

                axios.post('/notes', params).then((response)=>console.log(response));

                let note = {
                    id: 2,
                    description: this.description,
                    create_at: '03/02/2021'
                }
                this.$emit('new', note);
                this.description=""
            }
        }
    }
</script>