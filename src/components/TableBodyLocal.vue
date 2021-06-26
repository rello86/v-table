<template>
    <tbody v-if="hasRecords" class="bg-white divide-y divide-gray-200">
    <tr v-show="index >= pageable.offset && index <= (pageable.offset + pageable.pageable.pageSize -1)" v-for="(record, index) in records">
        <td v-for="(item, key) in record" class="px-6 py-4">
            <div class="text-sm text-gray-900">
                <span :class="headers[key].classes">{{item}}</span>
            </div>
        </td>
    </tr>

    <!--<tbody v-else class="bg-white divide-y divide-gray-200">
    <tr>
        <td :colspan="Object.keys(headers).length">
            <div class="rounded-md bg-red-50 p-4">
                <div class="flex">
                    <div class="flex-shrink-0">
                        &lt;!&ndash; Heroicon name: solid/x-circle &ndash;&gt;
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
    </tr>-->
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
            records: {
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
                pageable: null
            }
        },
        computed: {
            hasRecords() {
                if (this.records && this.headers) {
                    this.keepRecordsToShow()
                    this.pageable = {
                        totalElements: this.records.length,
                        totalPages: Math.ceil(this.records.length / this.paginate.per_page),
                        pageable: {
                            pageSize: this.paginate.per_page,
                            pageNumber: this.paginate.current_page,
                        },
                        last: false,
                        first: true,
                        offset: 0,
                    }
                    return true;
                } else {
                    console.error('Headers & Records array can not be null')
                    return false;
                }
            },
        },
        methods: {
            keepRecordsToShow() {
                this.records.forEach(element => {
                    for (let key in element) {
                        if (!this.headers.hasOwnProperty(key)) {
                            delete element[key]
                        }
                    }
                })
            }
        },
        watch: {
            pageable: function () {
                this.$emit('pageable', this.pageable)
            }
        },
    }
</script>