<template>
    <tbody class="bg-white divide-y divide-gray-200">
    <!--<tr v-if="hasRecords" v-for="record in records">-->
    <tr v-if="hasRecords" v-for="(record, index) in records" @click="showModalTable(index)">
        <td v-for="(item, key) in record" class="px-6 py-4">
            <div class="text-sm text-gray-900">
                <span :class="headers[key].classes">
                    {{item}}
                </span>
            </div>
        </td>
    </tr>
    <tr v-else>
        <td :colspan="Object.keys(headers).length">
            <div class="rounded-md bg-red-50 p-4">
                <div class="flex">
                    <div class="flex-shrink-0">
                        <!-- Heroicon name: solid/x-circle -->
                        <svg class="h-5 w-5 text-red-400" xmlns="http://www.w3.org/2000/svg"
                             viewBox="0 0 20 20" fill="currentColor" aria-hidden="true">
                            <path fill-rule="evenodd"
                                  d="M10 18a8 8 0 100-16 8 8 0 000 16zM8.707 7.293a1 1 0 00-1.414 1.414L8.586 10l-1.293 1.293a1 1 0 101.414 1.414L10 11.414l1.293 1.293a1 1 0 001.414-1.414L11.414 10l1.293-1.293a1 1 0 00-1.414-1.414L10 8.586 8.707 7.293z"
                                  clip-rule="evenodd"/>
                        </svg>
                    </div>
                    <div class="ml-3">
                        <h3 class="text-sm font-medium text-red-800">
                            Records array can not be null
                        </h3>
                    </div>
                </div>
            </div>
        </td>
    </tr>
    <div v-if="toggleModal && hasRecords" class="fixed z-10 inset-0 overflow-y-auto" aria-labelledby="modal-title"
         role="dialog" aria-modal="true">
        <div class="flex items-end justify-center min-h-screen pt-4 px-4 pb-20 text-center sm:block sm:p-0">
            <!--
              Background overlay, show/hide based on modal state.

              Entering: "ease-out duration-300"
                From: "opacity-0"
                To: "opacity-100"
              Leaving: "ease-in duration-200"
                From: "opacity-100"
                To: "opacity-0"
            -->
            <div class="fixed inset-0 bg-gray-500 bg-opacity-75 transition-opacity" aria-hidden="true"></div>

            <!-- This element is to trick the browser into centering the modal contents. -->
            <span class="hidden sm:inline-block sm:align-middle sm:h-screen" aria-hidden="true">&#8203;</span>

            <!--
              Modal panel, show/hide based on modal state.

              Entering: "ease-out duration-300"
                From: "opacity-0 translate-y-4 sm:translate-y-0 sm:scale-95"
                To: "opacity-100 translate-y-0 sm:scale-100"
              Leaving: "ease-in duration-200"
                From: "opacity-100 translate-y-0 sm:scale-100"
                To: "opacity-0 translate-y-4 sm:translate-y-0 sm:scale-95"
            -->
            <div class="inline-block align-bottom bg-white rounded-lg px-4 pt-5 pb-4 text-left overflow-hidden shadow-xl transform transition-all sm:my-8 sm:align-middle sm:max-w-lg sm:w-full sm:p-6">
                <div class="hidden sm:block absolute top-0 right-0 pt-4 pr-4">
                    <button @click="toggleModal = false" type="button"
                            class="bg-white rounded-md text-gray-400 hover:text-gray-500 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500">
                        <span class="sr-only">Close</span>
                        <!-- Heroicon name: outline/x -->
                        <svg class="h-6 w-6" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24"
                             stroke="currentColor" aria-hidden="true">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                  d="M6 18L18 6M6 6l12 12"/>
                        </svg>
                    </button>
                </div>
                <div class="sm:flex sm:items-start">
                    <div  class="mt-3 text-center sm:mt-0 sm:ml-4 sm:text-left">
                        <div  class="mt-2">
                            <p class="text-sm text-gray-500">
                                {{records_copy[itemModal]}}
                            </p>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
    </tbody>

</template>

<style scoped>
    @tailwind base;
    @tailwind components;
    @tailwind utilities;
</style>

<script>
    export default {
        props: {
            settings: {
                type: Object,
                default: null
            },
            headers: {
                type: Object,
                default: null
            },
            paginate: {
                type: Object,
                default: null
            },
        },
        components: {},
        data() {
            return {
                records: null,
                pageable: null,
                records_copy: null,
                toggleModal: false,
                itemModal: null
            }
        },
        watch: {
            pageable: function () {
                this.$emit('pageable', this.pageable)
            }
        },
        computed: {
            hasRecords() {
                if (this.headers) {
                    this.api().then((records) => {
                            console.log('response --------------------')
                            console.log(records)
                            if (this.settings.pagination) {
                                console.log('pagination --------------------')
                                console.log(records.content)
                                this.records = records.content
                                this.records_copy = JSON.parse(JSON.stringify(records.content))
                                console.log('records copy -----')
                                console.log(this.records_copy)
                                this.keepRecordsToShow()
                                delete records.content
                                this.pageable = records
                                this.pageable.sort = this.paginate.sort
                                this.pageable.direction = this.paginate.direction

                            } else {
                                console.log('not pagination --------------------')
                                console.log(records)
                                this.records = records
                                this.records_copy = JSON.parse(JSON.stringify(records))
                                this.keepRecordsToShow()
                            }

                        }
                    ).catch(
                        //console.error('error fetching data from remote url')
                    )
                    //console.log('ciao')
                    return true
                } else {
                    console.error('Headers & Records array can not be null')
                    return false;
                }

            },
        },
        methods: {
            async api() {
                let url = this.settings.sourceURL
                if (this.settings.search && this.paginate.search !== null) {
                    url += "?search=" + this.paginate.search + "&"
                } else {
                    url += "?"
                }

                url += "direction=" + this.paginate.direction + "&sort=" + this.paginate.sort

                if (this.settings.pagination && this.paginate.current_page !== null) {
                    url += "&page=" + this.paginate.current_page
                }

                url += "&size=" + this.paginate.per_page
                console.log(url)
                //let response = await fetch("http://isin03.dti.supsi.ch:81/template/bff/items?search="+this.paginate.search+"&direction="+this.paginate.direction+"&sort="+this.paginate.sort+"&page="+this.paginate.current_page+"&size="+this.paginate.per_page+"");
                let response = await fetch(url);

                /*(this.paginate.direction) ? "direction="+this.paginate.direction : '' +
                (this.paginate.sort) ? "&sort="+this.paginate.sort : ''  +
                (this.paginate.current_page) ? "&page="+this.paginate.current_page : ''  +
                (this.paginate.per_page) ? "&size="+this.paginate.per_page : '' +"");*/

                return await response.json();

                // fare copia per tabella
                // orginale mostrare modale
            },
            keepRecordsToShow() {
                console.log(this.records)
                this.records.forEach(element => {
                    for (let key in element) {
                        if (!this.headers.hasOwnProperty(key)) {
                            delete element[key]
                            // da tenere --- mostrare in modal alert
                        }
                    }
                })
            },

            isToShow(key) {

                if (this.headers.hasOwnProperty(key)) {
                    return true;
                }
                return false;
            },

            showModalTable(id) {
                console.log('new ID')
                console.log(id)
                this.toggleModal = !this.toggleModal
                this.itemModal = id;
            }
        }
    }
</script>