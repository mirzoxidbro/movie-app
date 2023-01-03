<template lang="">
    <div class="movie-add-form">
        <h3>Yangi kino qo'shish</h3>
        <form class="add-form d-flex" @submit.prevent>
            <input v-model="name"  type="text" class="form-control new-movie-label" placeholder="Qanday kino?">
            <input v-model="viewers"  type="number" class="form-control new-movie-label" placeholder="Qancha ko'rilgan?">
            <button class="btn btn-outline-dark" type="submit" @click="addMovie()">Qo'shish</button>
        </form>
    </div>
</template>
<script>
export default {
    data(){
        return {
            name: '',
            viewers: ''
        }
    },

    methods: {
        addMovie(){
            if(!this.name || !this.viewers) return
            const newMovie = {
                id: Date.now(),
                name: this.name,
                viewers: this.viewers,
                favourite: false,
                like: false
            }
            
            this.$emit('createMovie', newMovie);
            this.name = '',
            this.viewers = ''
        },
        

    }

}
</script>
<style>
    .movie-add-form{
        margin-top: 2rem;
        margin-bottom: 2rem;
        padding: 1.5rem;
        border-radius: 4px;
        background-color: #fcfaf5;
        box-shadow: 15px 15px 15px rgba(0, 0, 0, 0.15);
    }
</style>