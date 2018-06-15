<template>
  <div class="container">
    <h1 class="title">Albums table</h1>
    <div class="search-form">
      <form>
        <label for="search-term">
          Looking for...
          <input type="text" v-model="searchTearm" placeholder="Search by..." id='search-term"'>
        </label>
        <label for="check">
          Albums...
          <select v-model="albumTitleOnly">
            <option value="all">All</option>
            <option value="albums">Albums</option>
          </select>
        </label>
    </form>
    </div>
    <div class="data-table">
      <data-table
     :data="combinedData"
     :columns="columns"
     :filterKey="searchTearm"
     :customFilterKey="albumTitleOnly"
    />
    </div>
  </div>
</template>

<script>
import Table from '@/components/DataTable'
export default {
  name: 'home',
  components: {DataTable: Table},
  data () {
    return {
      searchTearm: '',
      albumTitleOnly: 'all',
      columns: ['albumId', 'albumTitle', 'photoTitle', 'photoThumbnail'],
      combinedData: []
    }
  },
  mounted () {
    this.fetchData()
  },
  methods: {
    fetchData (items) {
      const photos = fetch('https://jsonplaceholder.typicode.com/photos').then(res => res.json())
      const albums = fetch('https://jsonplaceholder.typicode.com/albums').then(res => res.json())
      Promise.all([albums, photos]).then(values => {
        const [albums, photos] = values
        this.combinedData = albums.map((album, i) => ({
          albumId: album.id,
          albumTitle: album.title,
          photoTitle: photos[i].title,
          photoThumbnail: photos[i].thumbnailUrl
        }))
      }).catch(console.log)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.container {
  margin-left: 7%;
  margin-right: 7%;
}

.search-form form {
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
}

form input + select {
  margin: 10px auto;
}

.search-form,
.data-table {
  width: 100%;
  padding-top: 10px;
  padding-bottom: 15px;
}

.searc-form > *,
.data-table > * {
  margin: auto 15px;
}
.title {
  text-align: center;
}
input[type='text'],
select {
  /* width: 100%; */
  border-radius: 5px;
  padding: 3px;
}
</style>
