<template>
<div>
      <p class="pagination-container">
          <img src="https://img.icons8.com/fluency-systems-filled/20/000000/double-left.png" @click="changePage(0)"/>
          <img src="https://img.icons8.com/fluency-systems-filled/20/000000/back--v1.png" @click="changePage(-1)"/>
          <span> Page {{ page }} of {{ pages }}</span>
          <img src="https://img.icons8.com/fluency-systems-filled/20/000000/forward--v1.png" @click="changePage(1)"/>
          <img src="https://img.icons8.com/fluency-systems-filled/20/000000/double-right.png" @click="changePage(pages)"/>
      </p>
      <p>
           <span
                class="showing"
                v-for="(amount, index) in perPageOptions"
                :key="index"
                @click="setPerPage(amount)"
            >| {{amount}} | </span>
      </p>
</div>
</template>

<script>
import { ref, computed } from "vue";
export default {
    props: {
        totalRecords: Number,
        perPageOptions: Array
    },

    setup(props, { emit }) {
        const page = ref(1)
        const perPage = ref(props.perPageOptions[0])
        const records = ref(props.totalRecords)

        const pages = computed(() => {
            if (records.value % perPage.value > 0) {
                return Math.floor(records.value / perPage.value) + 1
            } else {
                return records.value / perPage.value
            }
        })

        function setPerPage(amount) {
            perPage.value = amount
            emit('update:modelValue', { page: page.value, perPage: amount })
        }

        function changePage(val) {
            switch (val) {
                case 0: page.value = 1; break;
                case -1: page.value = page.value > 1 ? page.value - 1 : page.value; break;
                case 1: page.value = page.value < pages.value ? page.value + 1 : page.value; break;
                case pages.value: page.value = pages.value; break;
            }
            emit('update:modelValue', { page: page.value, perPage: perPage.value })
        }

        return {
            page,
            pages,
            setPerPage,
            changePage
        }
    },
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