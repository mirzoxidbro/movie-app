<template lang="">
    <input  
        type="text" 
        class="form-control search-input" 
        placeholder="Kinolarni qidirish"
        @input="changeTermHandler"
        :value="term"
        />
</template>
<script>
export default {
    props: {
        updateTermHandler: {
            type: Function,
            required: true
        }
    },

    data(){
        return{
            term: ''
        }
    },

    methods: {
        changeTermHandler(e){
            this.term = e.target.value
            this.updateTermHandler(this.term)
        }
    }

}
</script>
<style scoped>
    .search-input{
        margin-top: 2rem;
        margin-bottom: 2rem;
        padding: 1.5rem;
        border-radius: 4px;
        background-color: #fcfaf5;
        box-shadow: 15px 15px 15px rgba(0, 0, 0, 0.15);
    }
</style>