<template>
  <div class="app font-monospace">
    <div class="content">
      <AppInfo :movieCount="movies.length" :favouriteMovie="movies.filter(m => m.favourite).length"/>
      <div class="search-panel">
        <SearchPanel  :updateTermHandler="updateTermHandler" />
        <AppFilter :updateFilterHandler="updateFilterHandler" :filterName="filter" />
      </div>
      <Box v-if="!movies.length && !isLoading">
         <div class="text-center fs-3 text-danger">Kinolar yo'q</div> 
      </Box>
      <Loader v-else-if="isLoading" class="d-flex justify-content-center"></Loader>
        <movie-list v-else
                   :movies="onFilterHandler(onSearchHandler(movies, term), filter)" 
                    @onLike="onLikeHandler" 
                    @onDelete="onDeleteHandler"
                    @onFavourite="onFavouriteHandler" />
                    
        <Box>
          <nav aria-label="...">
            <ul class="pagination pagination-sm">
              <li v-for="pageNumber in totalPage" :key="pageNumber" @click="ChangePageNumber(pageNumber)">
                  <span class="page-link" style="cursor:pointer;" :class="{'active': pageNumber == page}" >{{ pageNumber }}</span>
              </li>
            </ul>
          </nav>
        </Box>
                    
      <movie-add-form @createMovie="createMovie"/>
    </div>
  </div>
</template>

<script>
import AppFilter from '../app-filter/AppFilter.vue'
import AppInfo from '../app-info/AppInfo.vue'
import MovieAddForm from '../movie-add-form/MovieAddForm.vue'
import MovieList from '../movie-list/MovieList.vue'
import SearchPanel from '../search-panel/SearchPanel.vue'
import axios from 'axios'
import PrimaryButton from '../../ui-components/PrimaryButton.vue'
import  Box  from '../../ui-components/Box.vue'
import  Loader  from '../../ui-components/Loader.vue'


  export default{
    components: {
        AppInfo,
        SearchPanel,
        AppFilter,
        MovieList,
        MovieAddForm,
        PrimaryButton,
        Box,
        Loader
    },

    data() {
        return {
            movies: [],
            term: '',
            filter: 'all',
            isLoading: false,
            limit: 10,
            page:1,
            totalPage: 0
        }
    },

    methods: {
      async createMovie(item){
        // this.movies.push(item)
        const response = await axios.post('https://jsonplaceholder.typicode.com/posts', item)
        console.log(response);
      },
      onLikeHandler(id){
          const arr = this.movies.map(item => {
            if(item.id == id){
                item.like = ! item.like
            }
            return item
          })
      },
      async onDeleteHandler(id){
        this.movies = this.movies.filter(c => c.id !== id)
        const response = await axios.delete(`https://jsonplaceholder.typicode.com/posts/${id}`)
        console.log(response)
      },
      onFavouriteHandler(id){
        const arr = this.movies.map(item => {
          if(item.id == id){
            item.favourite = ! item.favourite
          }
        })
        return item;      
      },
      onSearchHandler(arr, term){
        if(term.length == 0){
          return arr;
        }

        return arr.filter(c => c.name.toLowerCase().indexOf(term) > -1)
      },
      
      updateTermHandler(term){
        this.term = term
      },

      onFilterHandler(arr, filter){
        switch(filter){
            case 'favourite' : return arr.filter(c => c.like);
            case 'popular' : return arr.filter(c => c.viewers > 50)
            default : return arr
          }
      },

      updateFilterHandler(filter){
        this.filter = filter
      },

      ChangePageNumber(page){
        this.page = page
      },

      async fetchMovie(){
        try {
          this.isLoading = true
            const response = await axios.get('https://jsonplaceholder.typicode.com/posts', {
              params: {
                _limit: this.limit,
                _page: this.page
              }
            })
            const newArr = response.data.map(item => ({
              id: item.id,
              name: item.title,
              favourite: false,
              like: false,
              viewers: item.id * 10
  
            }))
            this.movies = newArr
            this.isLoading = false
            this.totalPage = Math.ceil(response.headers['x-total-count'] / this.limit) 
        } catch (error) {
          alert(error.message)
        } 
        finally {
          this.isLoading = false
        }
      },

    },
    mounted() {
          this.fetchMovie();
        },

    watch: {
      page(){
        this.fetchMovie()
      }
    }
  }
</script>

<style>
    .app{
      height: 100vh;
      color: 000;
    }

    .content{
      width: 1000px;
      min-height: 700px;
      background-color: #fff;
      margin: 0 auto;
      padding: 5rem 0;
    }
    
    .search-panel{
      margin-top: 2rem;
      padding: 1.5rem;
      background-color: #fcfaf5;
      border-radius: 4px;
      box-shadow: 15px 15px 15px rgba(0, 0, 0, 0.15);
    }
</style>