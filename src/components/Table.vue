<template>
    <div v-bind="init" class="bg-white overflow-hidden shadow rounded-lg divide-y divide-gray-200">
        <div class="flex flex-col">
            <div class="-my-2 overflow-x-auto sm:-mx-6 lg:-mx-8">
                <div class="py-2 align-middle inline-block min-w-full sm:px-6 lg:px-8">
                    <div class="shadow overflow-hidden border-b border-gray-200 sm:rounded-lg">
                        <table-toolbar :settings="settings" :paginate="paginate" v-on:newSearch="updateSearch" v-on:newPerPage="updatePerPage"
                                       v-on:search="updateSearch"/>
                        <table class="min-w-full divide-y divide-gray-200">
                            <table-header :headers="headers" :paginate="paginate"  v-on:newDirection="updateDirection" v-on:newSort="updateSort"/>
                            <table-body-local v-if="settings.source === 'local'" :records="records" :headers="headers"
                                              :settings="settings" :paginate="paginate" @pageable="updatePaginate"/>
                            <table-body-api v-else-if="settings.source === 'api'" :headers="headers"
                                            :settings="settings" :paginate="paginate" @pageable="updatePaginate"/>
                        </table>
                        <table-pagination v-if="pagination" :paginate="paginate" v-on:newCurrentPage="updatePage"/>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<style scoped>
    @tailwind base;
    @tailwind components;
    @tailwind utilities;
</style>

<script>
    import TableHeader from './TableHeader.vue'
    import TableBodyLocal from './TableBodyLocal.vue'
    import TableBodyApi from './TableBodyApi.vue'
    import TablePagination from './TablePagination.vue'
    import TableToolbar from './TableToolbar.vue'

    export default {
        props: {
            /*source: {
                type: String,
                default: 'local'
            },
            sourceURL: {
                type: String,
                default: null
            },
            per_page: {
                type: Number,
                default: 10
            },
            pagination: {
                type: Boolean,
                default: false
            },
            search: {
                type: Boolean,
                default: false
            },*/
            settings: {
                type: Object,
                default: null
            },
            headers: {
                type: Object,
                default: null
            },
            records: {
                type: Object,
                default: null
            },
            /*currentSort: {
                type: String,
                default: null
            },
            currentSortDir: {
                type: String,
                default: null
            }*/
        },

        components: {
            TableHeader,
            TableBodyLocal,
            TableBodyApi,
            TablePagination,
            TableToolbar
        },
        data() {
            return {
                paginate: {
                    /*total_records: this.records.length,
                    numberOfPages: Math.ceil(this.records.length / this.per_page),*/
                    per_page: this.settings.per_page,
                    current_page: 0,
                    /*last_page: 1,
                    from: 1,
                    to: 10,*/
                    direction: null,
                    sort: null,
                    search:null,
                },
                source: this.settings.source,
                sourceURL: this.settings.sourceURL,
                per_page: this.settings.per_page,
                pagination: this.settings.pagination,
                search: this.settings.search,
            }
        },
        computed: {
            init() {
                if (this.headers && this.paginate.sort === null && this.paginate.direction === null) {
                    for (let key in this.headers) {
                        if (this.headers[key].sort) {
                            this.paginate.sort = key
                            this.paginate.direction = 'asc'

                            /*const ordered = Object.keys(this.records).sort().reduce(
                                (obj, key) => {
                                    obj[key] = this.records[key];
                                    return obj;
                                },
                            );
                            console.log(ordered)*/

                        }
                    }
                }
            },

        },
        methods: {
            updatePaginate: function (pageable) {

                this.paginate.total_records = pageable.totalElements;
                this.paginate.numberOfPages = pageable.totalPages;
                this.paginate.per_page = pageable.pageable.pageSize;
                this.paginate.current_page = pageable.pageable.pageNumber;
                this.paginate.last_page = pageable.last;
                this.paginate.first_page = pageable.first;
                this.paginate.from = pageable.pageable.offset;
                this.paginate.to = pageable.pageable.offset + pageable.pageable.pageSize;
                this.paginate.direction = pageable.direction;
                this.paginate.sort = pageable.sort;

            },
            updatePage: function (newCurrentPage) {
                this.paginate.current_page = newCurrentPage
            },
            updateDirection: function (newDirection) {
                console.log('new direction')
                console.log(newDirection)
                this.paginate.direction = newDirection
                this.paginate.current_page = 0
            },
            updateSort: function (newSort) {
                console.log('new sort')
                console.log(newSort)
                this.paginate.sort = newSort
                this.paginate.current_page = 0
            },
            updatePerPage: function (newPerPage) {
                this.paginate.per_page = newPerPage
                this.paginate.current_page = 0
            },
            updateSearch: function (searchText) {

                console.log(searchText)
                //this.paginate.current_page = 1
                this.paginate.search = searchText
                this.paginate.current_page = 0
            }
        }
    }

    // This starter template is using Vue 3 experimental <script setup> SFCs
    // Check out https://github.com/vuejs/rfcs/blob/script-setup-2/active-rfcs/0000-script-setup.md
</script>