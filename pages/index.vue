<template>
  <div class="index-page">
    <CommentsTable :comments="comments" />
    <div class="btns">
      <button
        v-if="pageNumber>1"
        class="btn btn_go_prev"
        @click="goPageWithNumber(pageNumber - 1)"
      >
        &lt;
      </button>
      <button
        v-for="(one,idx) in pageBtnValues"
        :key="idx"
        class="btn"
        :class="{'btn_type_active': one === pageNumber}"
        @click="goPageWithNumber(one)"
      >
        {{ one }}
      </button>
      <button
        v-if="pageNumber < maxPageCount / limit"
        class="btn btn_go_next"
        @click="goPageWithNumber(pageNumber + 1)"
      >
        &gt;
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'PageIndex',
  async asyncData () {
    const apiData = await fetch('https://jsonplaceholder.typicode.com/comments').then(res => res.json())
    const maxPageCount = apiData[apiData.length - 1].id
    const comments = apiData.slice(0, 10)
    return { comments, maxPageCount }
  },
  data () {
    return {
      pageNumber: 1,
      maxPageCount: null,
      comments: [],
      limit: 10,
      BASE_URL: 'https://jsonplaceholder.typicode.com/comments?_limit=10&_page=',
      pageBtnValues: []
    }
  },
  methods: {
    async fetchNewPage () {
      this.comments = await fetch(`${this.BASE_URL}${this.pageNumber}`)
        .then(res => res.json())
    },
    goPageWithNumber (pageNumber) {
      this.pageNumber = pageNumber
      this.calculateBtnValues()
      this.fetchNewPage()
    },
    calculateBtnValues () {
      const btnsCount = 3
      this.pageBtnValues = []
      if (this.pageNumber > this.maxPageCount / this.limit - btnsCount) {
        this.pageBtnValues.push(this.maxPageCount / this.limit - 2, this.maxPageCount / this.limit - 1, this.maxPageCount / this.limit)
      } else {
        this.pageBtnValues.push(this.pageNumber, this.pageNumber + 1, this.pageNumber + 2, this.maxPageCount / this.limit)
      }
    }
  }
}
</script>

<style>
.index-page {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 90vh;
}
.btns {
  display: flex;
  margin: 20px auto 0;
  border-radius: 20px;
}
.btn{
  padding: 10px;
  border: none;
  color: #FFF;
  background: #44475C;
  transition: .2s ease-in-out;
  min-width: 35px;
}
.btn_type_active {
  background: #D4D8F9;
  color: #000;
}
.btn:hover{
  opacity: 0.8;
}

</style>
