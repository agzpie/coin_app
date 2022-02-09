<template>
  <section>
      <p class="pagination-container">
          <img src="https://img.icons8.com/fluency-systems-filled/24/000000/double-left.png" @click="changePage(0)"/>
          <img src="https://img.icons8.com/fluency-systems-filled/24/000000/back--v1.png" @click="changePage(-1)"/>
          <span> Page {{ page }} of {{ pages }}</span>
          <img src="https://img.icons8.com/fluency-systems-filled/24/000000/forward--v1.png" @click="changePage(1)"/>
          <img src="https://img.icons8.com/fluency-systems-filled/24/000000/double-right.png" @click="changePage(pages)"/>
      </p>
  </section>
</template>

<script>
export default {
    props: ['totalRecords', 'perPageOptions'],

    data: function () {
        return {
            page: 1,
            perPage: this.perPageOptions[0]
        }
    },
    computed: {
        pages () {
            const remainder = this.totalRecords % this.perPage
            if (remainder > 0) {
                return Math.floor(this.totalRecords / this.perPage) + 1
            } else {
                return this.totalRecords / this.perPage
            }
        }
    },
    methods: {
        changePage (val) {
            switch (val) {
                case 0: this.page = 1; break;
                case -1: this.page = this.page > 1 ? this.page - 1 : this.page; break;
                case 1: this.page = this.page < this.pages ? this.page + 1 : this.page; break;
                case this.pages: this.page = this.pages; break;
            }

            this.$emit('input', { page: this.page })
        }
    }
}
</script>

<style>

</style>