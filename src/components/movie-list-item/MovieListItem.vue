<template>

    <li 
        class="list-group-item d-flex justify-content-between favourite"
        :class="[{like: movie.like}, {favourite: movie.favourite}]"
        >

        <span @click="onLike()" class="list-group-item-label" >{{ movie.name }}</span>
        <input type="number" class="list-group-item-input" :value="movie.viewers" >

        <div>
            <button @click="onFavourite()" type="button" class="btn-cookie btn-sm"><i class="fas fa-cookie"></i></button>
            <button @click="onDelete()" type="button" class="btn-trash btn-sm"><i class="fas fa-trash"></i></button>
            <i class="fas fa-heart"></i>
        </div>
    </li>
</template>
<script>
export default {
    props: {
        movie: {
            type: Object,
            required: true
        }
    },
    methods: {
        onLike(){
            this.$emit('onLike', this.movie.id)
        },
        onDelete(){
            this.$emit('onDelete', this.movie.id)
        },
        onFavourite(){
            this.$emit('onFavourite', this.movie.id)
        }
    }
}
</script>
<style scoped>
    .list-group-item{
        padding: 15px 20px;
        border-bottom: 1px solid #3d5a80;
    }

    .list-group-item:last-child{
        border-bottom: 0;
    }
    .list-group-item span{
        line-height: 35px;
        font-size: 20px;
        text-align: center;
        cursor: pointer;
    }

    .list-group-item input{
        line-height: 35px;
        font-size: 20px;
        text-align: center;
        border: 0;
        outline: none;
    }

    .list-group-item button{
        width: 35px;
        height: 35px;
        margin: 3px;
        font-size: 17px;
        border: none;
        cursor: pointer;
    }

    .list-group-item .fa-heart{
        width: 35px;
        height: 35px;
        text-align: center;
        line-height: 35px;
        font-size: 16px;
        color: #bb0312;
        transition: 0.3s all;
        transform: translateX(30px);
        opacity: 0;
    }

    .list-group-item.like .fa-heart{
        transform: translateX(0);
        opacity: 1;
    }

    .list-group-item .btn-cookie{
        color: #e09f3e;
    }

    .list-group-item .btn-trash{
        color: #e5383b;
    }

    .list-group-item.favourite .list-group-item-label
    .list-group-item.favourite .list-group-item-label{
        color: #e09f3e;
    }
</style>