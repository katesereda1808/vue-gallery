<!-- eslint-disable vue/multi-word-component-names -->
<template>
    <ul class="pagination">
        <li class="pagination-item">
            <button class="pagination-btn" type="button" @click="onClickPage(1)" :disabled="isInFirstPage" :class="{ active: isPageActive(1) }">
                1
            </button>
        </li>
        <li>
            ...
        </li>
        <li v-for="page in pages" class="pagination-item" :key="page.name">
            <button class="pagination-btn" type="button" @click="onClickPage(page.name)" 
                :class="{ active: isPageActive(page.name) }">
                {{ page.name }}
            </button>
        </li>
        <li>
            ...
        </li>
        <li class="pagination-item">
            <button class="pagination-btn" type="button" @click="onClickPage(totalPages)" :disabled="isInLastPage" :class="{ active: isPageActive(totalPages) }">
                {{ totalPages }}
            </button>
        </li>
    </ul>
</template>
  
<script>
export default {
    props: {
        maxVisibleButtons: {
            type: Number,
            required: false,
            default: 3
        },
        totalPages: {
            type: Number,
            required: true
        },
        perPage: {
            type: Number,
            required: true
        },
        currentPage: {
            type: Number,
            required: true
        }
    },
    computed: {
        isInFirstPage() {
            return this.currentPage === 1;
        },
        isInLastPage() {
            return this.currentPage === this.totalPages;
        },
        startPage() {
            if (this.currentPage === 1) {
                return 1;
            }
            if (this.currentPage === this.totalPages) {
                return this.totalPages - this.maxVisibleButtons;
            }
            return this.currentPage - 1;
        },

        pages() {
            const range = [];
            for (
                let i = this.startPage;
                i <= Math.min(this.startPage + this.maxVisibleButtons - 1, this.totalPages);
                i++
            ) {
                range.push({
                    name: i,
                    isDisabled: i === this.currentPage
                });
            }
            return range;
        },
    },

    methods: {
        onClickFirstPage() {
            this.$emit('pagechanged', 1);
        },
        
        onClickPage(page) {
            this.$emit('pagechanged', page);
        },

        isPageActive(page) {
            return this.currentPage === page;
        }
    }
}
</script>
  
<style>
.pagination {
    height: 60px;
    position: sticky;
    bottom: 0;
    display: flex;
    justify-content: center;
    align-items: center;
    list-style-type: none;
    color: #ffffff;
    background-color: rgba(0, 0, 0, 0.9);
}
.pagination-item {
    display: inline-block;
}
.pagination-item .pagination-btn {
    color: #ffffff;
    font-size: 14px;
    font-weight: 400;
    background-color: transparent;
}
.active.pagination-btn{
    font-size: 18px;
    font-weight: 700;
    color: #ffffff;
}

</style>