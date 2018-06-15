<template>
<div class="form-container" @scroll="handleScroll">
  <table class="table">
    <thead class="table-header">
      <tr>
        <th v-for="(key,i) in columns" :key='i'
          @click="sortBy(key)"
          :class="{ active: sortKey === key }">
          {{ key | capitalize }}
          <template v-if="key !== 'photoThumbnail'">
            <span class="arrow" :class="sortOrders[key] > 0 ? 'asc' : 'dsc'">
          </span>
          </template>
        </th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(entry,i) in filteredData" :key="i" :ref="`td${(i+1)}`">
        <td v-for="(key,j) in columns" :key="j">
          <template v-if="key !== 'photoThumbnail'">
            {{entry[key]}}
          </template>
          <template v-else>
            <img :src="entry[key]" alt="aligator" class="thumb">
          </template>
        </td>
      </tr>
    </tbody>
  </table>
</div>
</template>
<script>
export default {
  name: 'data-table',
  props: {
    data: {
      type: Array,
      required: true
    },
    columns: {
      type: Array,
      required: true
    },
    filterKey: {
      type: String,
      required: true
    },
    customFilterKey: {
      type: String,
      required: true
    }
  },
  data () {
    let sortOrders = {}
    this.columns.forEach((key) => {
      sortOrders[key] = 1
    })
    return {
      sortKey: '',
      sortOrders: sortOrders,
      twentyFith: 0
    }
  },
  mounted () {
    const ref25 = this.$refs['td25']
    this.twentyFith = ref25[0].offsetTop
  },
  computed: {
    filteredData () {
      const sortKey = this.sortKey
      const filterKey = this.filterKey && this.filterKey.toLowerCase()
      const customFilterKey = this.customFilterKey && this.customFilterKey.toLowerCase()
      const order = this.sortOrders[sortKey] || 1
      let data = this.data
      if (filterKey) {
        data = data.filter((row) => {
          return Object.keys(row).some((key) => {
            if (key === 'photoThumbnail' || key === 'albumId') return
            if (key !== 'albumTitle' && customFilterKey !== 'all') return
            return String(row[key]).toLowerCase().indexOf(filterKey) > -1
          })
        })
      }
      if (sortKey) {
        data = data.slice().sort((a, b) => {
          a = a[sortKey]
          b = b[sortKey]
          return (a === b ? 0 : a > b ? 1 : -1) * order
        })
      }
      return data
    }
  },
  filters: {
    capitalize: (str) => {
      return (str.charAt(0).toUpperCase() + str.slice(1))
        .split(/(?=[A-Z])/).join(' ')
    }
  },
  methods: {
    sortBy (key) {
      if (key === 'photoThumbnail') return
      this.sortKey = key
      this.sortOrders[key] = this.sortOrders[key] * -1
    },
    handleScroll (e) {
      const table = document.querySelector('.table')
      const tableHeader = document.querySelector('.table-header')
      // console.log({table, tableHeader})
      // console.log(window.pageYOffset)
    }
  }
}
</script>
<style scoped lang='scss'>
//colors
$teal: teal;
$color_blue_chalk_approx: lavender;
$color_gallery_approx: #f0f0f0;
$white: #fff;

table {
  width: 100%;
  overflow: scroll;
}
thead {
  background: $teal;
  th {
    padding: 10px;
    color: $color_blue_chalk_approx;
    font-size: 18px;
    opacity: 0.8;
  }
}
.arrow {
  display: inline-block;
  vertical-align: middle;
  width: 0;
  height: 0;
  margin-left: 5px;
  opacity: 0.66;
  &.asc {
    border-left: 4px solid transparent;
    border-right: 4px solid transparent;
    border-bottom: 4px solid $white;
  }
  &.dsc {
    border-left: 4px solid transparent;
    border-right: 4px solid transparent;
    border-top: 4px solid $white;
  }
}
tbody td {
  padding: 0 10px;
  background: $color_gallery_approx;
}
td.thumb {
  width: 5px;
  height: 5px;
  text-align: center;
}
th.active {
  color: $white;
  opacity: 1;
  .arrow {
    opacity: 1;
  }
}
.form-container {
  height: 3997px;
  overflow: auto;
}
</style>
