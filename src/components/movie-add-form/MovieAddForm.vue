<template lang="">
    <div class="movie-add-form">
        <h3>Yangi kino qo'shish</h3>
        <form class="add-form d-flex">
            <input type="text" class="form-control new-movie-label" placeholder="Qanday kino?">
            <input type="text" class="form-control new-movie-label" placeholder="Qancha ko'rilgan?">
            <button class="btn btn-outline-dark" type="submit">Qo'shish</button>
        </form>
    </div>
</template>
<script>
export default {
    
}
</script>
<style scoped>
    .movie-add-form{
        margin-top: 2rem;
        margin-bottom: 2rem;
        padding: 1.5rem;
        border-radius: 4px;
        background-color: #fcfaf5;
        box-shadow: 15px 15px 15px rgba(0, 0, 0, 0.15);
    }
</style>