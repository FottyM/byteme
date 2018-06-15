<template>
<table>
   <thead>
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
      <tr v-for="(entry,i) in filteredData" :key="i">
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
</template>
<script>
export default {
  name: 'data-table',
  props: {
    data: Array,
    columns: Array,
    filterKey: String
  },
  data () {
    let sortOrders = {}
    this.columns.forEach((key) => {
      sortOrders[key] = 1
    })
    return {
      sortKey: '',
      sortOrders: sortOrders
    }
  },
  computed: {
    filteredData () {
      let sortKey = this.sortKey
      let filterKey = this.filterKey && this.filterKey.toLowerCase()
      let order = this.sortOrders[sortKey] || 1
      let data = this.data
      console.log({filterKey, sortKey})
      if (filterKey) {
        data = data.filter((row) => {
          return Object.keys(row).some((key) => {
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
    }
  }
}
</script>
<style scoped>
table {
  /* border: 1px solid black; */
  /* border-radius: 300px; */
  width: 100%;
}

thead {
  background: teal;
}
thead th {
  padding: 10px;
  color: lavender;
  font-size: 18px;
  opacity: 0.8;
}

tbody td {
  padding: 0 10px;
  background: #f0f0f0;
}

td.thumb {
  width: 5px;
  height: 5px;
  text-align: center;
}

th.active {
  color: #fff;
  opacity: 1;
}

th.active .arrow {
  opacity: 1;
}

.arrow {
  display: inline-block;
  vertical-align: middle;
  width: 0;
  height: 0;
  margin-left: 5px;
  opacity: 0.66;
}

.arrow.asc {
  border-left: 4px solid transparent;
  border-right: 4px solid transparent;
  border-bottom: 4px solid #fff;
}

.arrow.dsc {
  border-left: 4px solid transparent;
  border-right: 4px solid transparent;
  border-top: 4px solid #fff;
}
</style>
