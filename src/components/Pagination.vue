<template>
      <p class="pagination-container">
          <img src="https://img.icons8.com/fluency-systems-filled/20/000000/double-left.png" @click="changePage(0)"/>
          <img src="https://img.icons8.com/fluency-systems-filled/20/000000/back--v1.png" @click="changePage(-1)"/>
          <span> Page {{ page }} of {{ pages }}</span>
          <img src="https://img.icons8.com/fluency-systems-filled/20/000000/forward--v1.png" @click="changePage(1)"/>
          <img src="https://img.icons8.com/fluency-systems-filled/20/000000/double-right.png" @click="changePage(pages)"/>
      </p>
     <!-- <p>
           <span
                class="showing"
                :class="perPage === amount && 'active'"
                v-for="(amount, index) in perPageOptions"
                :key="index"
                @click="setPerPage(amount)"
            >| {{amount}} | </span>
      </p>
      -->
</template>

<script>
export default {
    props: ['totalRecords', 'perPageOptions' ],

    data () {
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
        setPerPage(amount) { // TO FIX: number of rows in the parent doesn't get updated
            this.perPage = amount
            this.$emit('input', {page: this.page, perPage: amount})
        },
        changePage (val) {
            switch (val) {
                case 0: this.page = 1; break;
                case -1: this.page = this.page > 1 ? this.page - 1 : this.page; break;
                case 1: this.page = this.page < this.pages ? this.page + 1 : this.page; break;
                case this.pages: this.page = this.pages; break;
            }
            this.$emit('update:modelValue', {   page: this.page, perPage: this.perPage })
        }
    }
}
</script>

<style>
.pagination-container {
    margin: 0.5rem;
    font-size: 0.95rem;
    text-align: center;
    width: 100%;
}
</style>