<template>
  <div class="app font-monospace">
    <div class="content">
      <AppInfo />
      <div class="search-panel">
        <SearchPanel />
        <AppFilter />
      </div>
      <movie-list />
      <movie-add-form />
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