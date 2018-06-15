<template>
  <div class="container">
    <div class="searc-form">
      <form>
      <input type="text" v-model="searchTearm" placeholder="Search by...">
    </form>
    </div>
    <div class="data-table">
      <data-table
     :data="combinedData"
     :columns="columns"
     :filterKey="searchTearm"
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
      columns: ['albumId', 'albumTitle', 'photoTitle', 'photoThumbnail'],
      combinedData: []
    }
  },
  async mounted () {
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
.searc-form,
.data-table {
  width: 100%;
  padding-top: 10px;
  padding-bottom: 15px;
}
.searc-form > *,
.data-table > * {
  margin: auto 15px;
}
input[type='text'] {
  /* width: 100%; */
  border-radius: 5px;
  padding: 3px;
  height: 30px;
  font-size: 20px;
}
</style>
