<template>
  <div class="app font-monospace">
    <div class="content">
      <AppInfo :movieCount="movies.length" :favouriteMovie="movies.filter(m => m.favourite).length"/>
      <div class="search-panel">
        <SearchPanel  :updateTermHandler="updateTermHandler" />
        <AppFilter :updateFilterHandler="updateFilterHandler" :filterName="filter" />
      </div>
      <movie-list :movies="onFilterHandler(onSearchHandler(movies, term), filter)" 
                  @onLike="onLikeHandler" 
                  @onDelete="onDeleteHandler"
                  @onFavourite="onFavouriteHandler" />
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
  export default{
    components: {
        AppInfo,
        SearchPanel,
        AppFilter,
        MovieList,
        MovieAddForm
    },

    data() {
        return {
            movies: [
                {name: "Ertugrul", favourite:true, like:true, viewers: 856, id: 1},
                {name: "Cho'qintirgan ota", favourite:false, like:false, viewers: 56, id: 2},
                {name: "O'tgan kunlar", favourite:true, like:false, viewers: 956, id: 3},
            ],
            term: '',
            filter: 'all'
        }
    },

    methods: {
      createMovie(item){
        this.movies.push(item)
      },
      onLikeHandler(id){
          const arr = this.movies.map(item => {
            if(item.id == id){
                item.like = ! item.like
            }
            return item
          })
      },
      onDeleteHandler(id){
        this.movies = this.movies.filter(c => c.id !== id)
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
            case 'popular' : return arr.filter(c => c.viewers > 500)
            default : return arr
          }
      },

      updateFilterHandler(filter){
        this.filter = filter
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