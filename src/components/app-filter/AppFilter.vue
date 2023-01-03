<template>
    <div class="btn-group">
        <button :class="[filterName == 'all' ? 'btn-dark' : 'btn-outline-dark']" class="btn" type="button" @click="filterHandler('all')">Barcha kinolar</button>
        <button :class="[filterName == 'favourite' ? 'btn-dark' : 'btn-outline-dark']" class="btn" type="button" @click="filterHandler('favourite')">Mashxur kinolar</button>
        <button :class="[filterName == 'popular' ? 'btn-dark' : 'btn-outline-dark']" class="btn" type="button" @click="filterHandler('popular')">Eng ko'p ko'rilgan kinolar</button>
    </div>
</template>
<script>
export default {
    props: {
        updateFilterHandler: {
            type: Function,
            required: true
        },
        filterName: {
            type: String,
            required: true
        }
    },

    data(){
        return {
            filter: 'all'
        }
    },

    methods: {
        filterHandler(filter){
            this.filter = filter
            this.updateFilterHandler(this.filter)
        }
    },
}
</script>
<style lang="">
    
</style>