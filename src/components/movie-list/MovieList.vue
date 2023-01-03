<template lang="">
    <ul class="movie-list list-group">
        <MovieListItem 
            v-for="movie in movies" 
            v-bind:key="movie.id" 
            :movie="movie" 
            @onLike="this.$emit('onLike', movie.id)"
            @onDelete="this.$emit('onDelete', movie.id)"
            @onFavourite="this.$emit('onFavourite', movie.id)"
            />
    </ul>
</template>
<script>
import MovieListItem from '../movie-list-item/MovieListItem.vue'
export default {
    components: {
        MovieListItem,
    },

    props: {
        movies: {
            type: Array,
            required: true
        }
    }
}
</script>
<style scoped>
    .movie-list{
        margin-top: 2rem;
        margin-bottom: 2rem;
        padding: 1.5rem;
        border-radius: 4px;
        background-color: #fcfaf5;
        box-shadow: 15px 15px 15px rgba(0, 0, 0, 0.15);
    }
</style>