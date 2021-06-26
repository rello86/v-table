<template>

    <thead class="bg-gray-50">
    <tr>
        <th v-for="(header, name, index) in headers" scope="col"
            class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider" :key="index">
            <div class="flex">
                <div v-if="header.sort" v-on:click="$emit('newSort', name)" class="text-gray-900">
                    {{header.name}}
                </div>
                <div v-else class="text-gray-400">
                    {{header.name}}
                </div>

                <div v-show="header.sort && name === paginate.sort" class="ml-3">
                    <div v-show="paginate.direction === desc" v-on:click="$emit('newDirection', toggleDirection(paginate.direction))">
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-3 w-3" viewBox="0 0 20 20"
                             fill="currentColor">
                            <path fill-rule="evenodd"
                                  d="M14.707 12.293a1 1 0 010 1.414l-4 4a1 1 0 01-1.414 0l-4-4a1 1 0 111.414-1.414L9 14.586V3a1 1 0 012 0v11.586l2.293-2.293a1 1 0 011.414 0z"
                                  clip-rule="evenodd"/>
                        </svg>
                    </div>
                    <div v-show="paginate.direction === asc" v-on:click="$emit('newDirection', toggleDirection(paginate.direction))">
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-3 w-3" viewBox="0 0 20 20"
                             fill="currentColor">
                            <path fill-rule="evenodd"
                                  d="M5.293 7.707a1 1 0 010-1.414l4-4a1 1 0 011.414 0l4 4a1 1 0 01-1.414 1.414L11 5.414V17a1 1 0 11-2 0V5.414L6.707 7.707a1 1 0 01-1.414 0z"
                                  clip-rule="evenodd"/>
                        </svg>
                    </div>
                </div>
            </div>
        </th>
    </tr>
    </thead>
</template>

<style scoped>
    @tailwind base;
    @tailwind components;
    @tailwind utilities;
</style>

<script>

    export default {
        props: {
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
                asc: 'asc',
                desc: 'desc',
                /*direction: this.paginate.direction,
                sort: this.paginate.sort*/
            }
        },
        watch: {

        },
        computed: {},
        methods: {
            toggleDirection(direction) {
                console.log('sort -------------------------')
                console.log(this.paginate.direction)
                console.log('direction -------------------------')
                console.log(direction)
                if(direction === 'asc'){
                    console.log('new direction -------------------------> desc')
                    return 'desc'
                } else {
                    console.log('new direction -------------------------> asc')
                    return 'asc'
                }
            }
        },

    }

    // This starter template is using Vue 3 experimental <script setup> SFCs
    // Check out https://github.com/vuejs/rfcs/blob/script-setup-2/active-rfcs/0000-script-setup.md
</script>