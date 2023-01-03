<template>
    <div class="btn-group">
        <button 
            v-for="btn in filterButtons" :key="btn.name"
            class="btn" :class="[filterName == btn.name ? 'btn-dark' : 'btn-outline-dark']"
            @click="filterHandler(btn.name)"
            >
            {{ btn.title }}
        </button>
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
            filterButtons: [
                {title: 'Barcha kinolar', name: 'all'},
                {title: 'Mashxur kinolar', name: 'favourite'},
                {title: "Eng ko'p ko'rilgan kinolar", name: 'popular'},
            ],
            filter: 'all',
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