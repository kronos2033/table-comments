<template>
  <section class="table-section">
    <table class="table">
      <thead>
        <tr class="table__row">
          <th class="table__header">
            <span>ID</span>
            <button
              class="btn"
              @click="reverseTableData"
            >
              {{ isSorted? '&#x2193;' : '&#8593;' }}
            </button>
          </th>
          <th class="table__header">
            Name
          </th>
          <th class="table__header">
            Email
          </th>
        </tr>
      </thead>
      <tbody class="table__body">
        <tr
          v-for="comment in comments"
          :key="comment.id"
          class="table__row"
          @click="$router.push(`/${comment.id}`)"
        >
          <td class="table__data">
            {{ comment.id }}
          </td>
          <td class="table__data">
            {{ comment.name }}
          </td>
          <td class="table__data">
            {{ comment.email }}
          </td>
        </tr>
      </tbody>
    </table>
  </section>
</template>

<script>
export default {
  props: {
    comments: {
      type: Array,
      default: null
    }
  },
  data () {
    return {
      isSorted: false
    }
  },
  methods: {
    reverseTableData () {
      this.isSorted = !this.isSorted
      this.$props.comments.reverse()
    }
  }
}
</script>

<style>
.table {
  min-width: 30rem;
  border-collapse: collapse;
  border: 3px solid #44475C;
}

.table .table__header {
  text-transform: uppercase;
  text-align: center;
  background: #44475C;
  color: #FFF;
  padding: 8px;
  min-width: 20px;
}

.table .table__data {
  text-align: left;
  padding: 8px;
  border-right: 2px solid #7D82A8;
}

.table .table__data:last-child {
  border-right: none;
}
.table .table__body .table__row:hover {
  cursor: pointer;
  color: #7D82A8;
}
.table .table__body .table__row:nth-child(even) td {
  background: #D4D8F9;
}

.table .table__body .table__row:nth-child(odd) td {
  background: #FFF;
}
</style>
