<template>
    <div class="app-info">
        <p class="fs-3 text-uppercase">Barcha kinolar soni: {{ movieCount }}</p>
        <p class="fs-3 text-uppercase">Ko'rilgan kinolar soni: {{ favouriteMovie }}</p>
    </div>
</template>

<script>
    export default{
        props: {
            movieCount: {
                type: Number,
                required: true
            },
            favouriteMovie: {
                type: Number,
                required: true
            }
        }
    }
</script>

<style scoped>
    .app-info{
        padding: 1.5rem;
        border-radius: 4px;
        background-color: #fcfaf5;
        box-shadow: 15px 15px 15px rgba(0, 0, 0, 0.15);
    }
</style>