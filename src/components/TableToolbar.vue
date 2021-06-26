<template>
    <header class="bg-white lg:static lg:overflow-y-visible">
        <div class="max-w-7xl mx-auto px-4 sm:px-6">
            <div class="relative flex justify-between xl:grid xl:grid-cols-12 lg:gap-8">
                <div v-if="settings.search" class="min-w-0 flex-1 md:px-8 lg:px-0 xl:col-span-7">
                    <div class="flex items-center px-6 py-4 md:max-w-3xl md:mx-auto lg:max-w-none lg:mx-0 xl:px-0">
                        <div class="w-full">
                            <label for="search" class="sr-only">Search</label>
                            <div class="relative">
                                <div class="pointer-events-none absolute inset-y-0 left-0 pl-3 flex items-center">
                                    <!-- Heroicon name: solid/search -->
                                    <svg class="h-5 w-5 text-gray-400" xmlns="http://www.w3.org/2000/svg"
                                         viewBox="0 0 20 20" fill="currentColor" aria-hidden="true">
                                        <path fill-rule="evenodd"
                                              d="M8 4a4 4 0 100 8 4 4 0 000-8zM2 8a6 6 0 1110.89 3.476l4.817 4.817a1 1 0 01-1.414 1.414l-4.816-4.816A6 6 0 012 8z"
                                              clip-rule="evenodd"/>
                                    </svg>
                                </div>
                                <input id="search" name="search"
                                       class="block w-full bg-white border border-gray-300 rounded-md py-2 pl-10 pr-3 text-sm placeholder-gray-500 focus:outline-none focus:text-gray-900 focus:placeholder-gray-400 focus:ring-1 focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm"
                                       placeholder="Search" type="search" v-model="searchText"
                                       @change="$emit('newSearch', searchText)">
                            </div>
                        </div>
                    </div>
                </div>
                <div v-if="settings.search" class="col-span-2">
                    <div class="flex items-center px-6 py-4 md:max-w-3xl md:mx-auto lg:max-w-none lg:mx-0 xl:px-0">
                        <button v-on:click="$emit('newSearch', searchText)"
                                class="inline-flex items-center px-4 py-2 border border-transparent text-sm font-medium rounded-md shadow-sm text-white bg-indigo-600 hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500">
                            Search
                        </button>
                    </div>
                </div>
                <div v-if="settings.pagination" class="hidden lg:flex lg:items-center lg:justify-end xl:col-span-2">
                    <div class="relative inline-block text-left">
                        <div>
                            <button type="button" @click="showPerPageOptions = !showPerPageOptions"
                                    class="inline-flex justify-center w-full rounded-md border border-gray-300 shadow-sm px-4 py-2 bg-white text-sm font-medium text-gray-700 hover:bg-gray-50 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-offset-gray-100 focus:ring-indigo-500"
                                    id="options-menu" aria-expanded="true" aria-haspopup="true">
                                {{paginate.per_page}}
                                <!-- Heroicon name: solid/chevron-down -->
                                <svg class="-mr-1 ml-2 h-5 w-5" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20"
                                     fill="currentColor" aria-hidden="true">
                                    <path fill-rule="evenodd"
                                          d="M5.293 7.293a1 1 0 011.414 0L10 10.586l3.293-3.293a1 1 0 111.414 1.414l-4 4a1 1 0 01-1.414 0l-4-4a1 1 0 010-1.414z"
                                          clip-rule="evenodd"/>
                                </svg>
                            </button>
                        </div>
                        <transition
                                enter-active-class="transition ease-out duration-200"
                                enter-class="transform opacity-0 scale-95"
                                enter-to-class="transform opacity-100 scale-100"
                                leave-active-class="transition ease-in duration-75"
                                leave-class="transform opacity-100 scale-100"
                                leave-to-class="transform opacity-0 scale-95">
                            <div v-show="showPerPageOptions"
                                 class="origin-top-right absolute right-0 mt-2 w-36 rounded-md shadow-lg bg-white ring-1 ring-black ring-opacity-5 focus:outline-none"
                                 role="menu" aria-orientation="vertical" aria-labelledby="options-menu">
                                <div class="py-1" role="none">
                                    <button href="#" v-show="paginate.per_page !== 5"
                                            v-on:click="$emit('newPerPage', 5)"
                                            class="w-full block px-4 py-2 text-sm text-gray-700 hover:bg-gray-100 hover:text-gray-900"
                                            role="menuitem">5
                                    </button>
                                    <button href="#" v-show="paginate.per_page !== 10"
                                            v-on:click="$emit('newPerPage', 10)"
                                            class="w-full block px-4 py-2 text-sm text-gray-700 hover:bg-gray-100 hover:text-gray-900"
                                            role="menuitem">10
                                    </button>
                                    <button href="#" v-show="paginate.per_page !== 15"
                                            v-on:click="$emit('newPerPage', 15)"
                                            class="w-full block px-4 py-2 text-sm text-gray-700 hover:bg-gray-100 hover:text-gray-900"
                                            role="menuitem">15
                                    </button>
                                </div>
                            </div>
                        </transition>
                    </div>
                </div>
            </div>
        </div>
    </header>
</template>

<style scoped>
    @tailwind base;
    @tailwind components;
    @tailwind utilities;
</style>

<script>
    export default {
        props: {
            paginate: {
                type: Object,
                default: null
            },
            settings: {
                type: Object,
                default: null
            },
        },
        data() {
            return {
                showPerPageOptions: false,
                searchText: null
            }
        },
        methods: {
            /*realTimeSearchText: throttle(function (newSearch) {
                // the plan is to replace this with an API call
                this.searchText = newSearch;
            }, 0)*/
        },
        components: {}
        ,
        computed: {}
        ,
        watch: {}
    }

</script>