<template lang="">
    <nav aria-label="...">
            <ul class="pagination pagination-sm">
              <li v-for="pageNumber in totalPage" :key="pageNumber">
                  <span class="page-link" style="cursor:pointer;" :class="{'active': pageNumber == page}" @click="ChangePageNumber(pageNumber)">{{ pageNumber }}</span>
              </li>
            </ul>
    </nav>
</template>
<script>
export default {
    props:{
        totalPage:{
            type: Number,
            required: true
        },
        page: {
            type: Number,
            required: true
        },
        ChangePageNumber:{
            type: Function,
            required: true
        }
    }
}
</script>
<style lang="">
    
</style>