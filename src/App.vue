<template>
    <div v-for="example in examples" class="relative min-h-screen flex flex-col">
        <!-- 3 column wrapper -->
        <div class="flex-grow w-full max-w-full mx-auto xl:px-8 lg:flex">
            <!-- Left sidebar & main wrapper -->
            <div class="flex-1 min-w-0 bg-white xl:flex">
                <div class="border-b border-gray-200 xl:border-b-0 xl:flex-shrink-0 xl:w-64 xl:border-r xl:border-gray-200 bg-white">
                    <div class="h-full pl-4 pr-6 py-6 sm:pl-6 lg:pl-8 xl:pl-0">
                        <!-- Start left column area -->
                        <div class="h-full relative" style="min-height: 12rem;">
                            <div class="absolute inset-0 border-2 border-gray-200 border-dashed rounded-lg">
                                <h2 class="text-2xl font-bold leading-7 text-gray-900 sm:text-3xl sm:truncate">
                                    <img alt="Vue logo" class="w-10 h-10" src="./assets/logo.png"/>
                                    {{example.title}}
                                </h2>
                            </div>
                        </div>
                        <!-- End left column area -->
                    </div>
                </div>

                <div class="bg-white lg:min-w-0 lg:flex-1">
                    <div class="h-full py-6 px-4 sm:px-6 lg:px-8">
                        <!-- Start main area-->
                        <div class="relative h-full" style="min-height: 76rem;">
                            <div class="absolute inset-0 border-2 border-gray-200 border-dashed rounded-lg">
                                <Table :headers="example.headers" :records="example.records" :settings="example.settings"/>
                            </div>
                        </div>
                        <!-- End main area -->
                    </div>
                </div>
            </div>

            <div class="bg-gray-50 pr-4 sm:pr-6 lg:pr-8 lg:flex-shrink-0 lg:border-l lg:border-gray-200">
                <div class="h-full pl-6 py-6 lg:w-80">
                    <!-- Start right column area -->
                    <div class="h-full relative" style="min-height: 16rem;">
                        <div class="absolute inset-0 border-2 border-gray-200 border-dashed rounded-lg p-2">
                            <h2 class="text-2xl font-bold leading-7 text-gray-900 sm:text-3xl sm:truncate">Settings</h2>
                            <pre><code class="block whitespace-pre overflow-x-scroll">
                                {{example.settings}}
                            </code></pre>
                            <h2 class="text-2xl font-bold leading-7 text-gray-900 sm:text-3xl sm:truncate">Headers</h2>
                            <pre><code class="block whitespace-pre overflow-x-scroll">
                                {{example.headers}}
                            </code></pre>
                        </div>
                    </div>
                    <!-- End right column area -->
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
    import Table from './components/Table.vue'

    export default {
        props: [],
        components: {
            Table
        },
        data() {
            return {
                examples: {
                    simpleApi: {
                        title: 'Simple Api',
                        settings: {
                            source: 'api',
                            sourceURL: 'http://isin03.dti.supsi.ch:81/template/bff/items',
                            per_page: 5,
                            pagination: false,
                            search: false,
                        },
                        headers: {
                            // To avoid potential bugs keep the order as the records array
                            'title': {
                                'name': "Titolo",
                                'sort': true,
                                'classes': ''
                            },
                            'description': {
                                'name': "Descrizione",
                                'sort': true,
                                'classes': ''
                            },
                            'status': {
                                'name': "Stato",
                                'sort': false,
                                'classes': 'inline-flex items-center px-3 py-0.5 rounded-full text-sm font-medium bg-gray-100 text-gray-800'
                            },
                        },
                        records: {

                        }
                    },
                    paginationApi: {
                        title: 'Pagination Api',
                        settings: {
                            source: 'api',
                            sourceURL: 'http://isin03.dti.supsi.ch:81/template/bff/items',
                            per_page: 10,
                            pagination: true,
                            search: false,
                        },
                        headers: {
                            // To avoid potential bugs keep the order as the records array
                            'title': {
                                'name': "Titolo",
                                'sort': true,
                                'classes': ''
                            },
                            'description': {
                                'name': "Descrizione",
                                'sort': false,
                                'classes': ''
                            },
                            'status': {
                                'name': "Stato",
                                'sort': false,
                                'classes': 'inline-flex items-center px-3 py-0.5 rounded-full text-sm font-medium bg-gray-100 text-gray-800'
                            },
                        },
                        records: {

                        }
                    },
                    searchApi: {
                        title: 'Search Api',
                        settings: {
                            source: 'api',
                            sourceURL: 'http://isin03.dti.supsi.ch:81/template/bff/items',
                            per_page: 5,
                            pagination: false,
                            search: true,
                        },
                        headers: {
                            // To avoid potential bugs keep the order as the records array
                            'title': {
                                'name': "Titolo",
                                'sort': false,
                                'classes': ''
                            },
                            'description': {
                                'name': "Descrizione",
                                'sort': false,
                                'classes': ''
                            },
                            'status': {
                                'name': "Stato",
                                'sort': false,
                                'classes': 'inline-flex items-center px-3 py-0.5 rounded-full text-sm font-medium bg-gray-100 text-gray-800'
                            },
                        },
                        records: {

                        }
                    },
                    fullApi: {
                        title: 'Full Api',
                        settings: {
                            source: 'api',
                            sourceURL: 'http://isin03.dti.supsi.ch:81/template/bff/items',
                            per_page: 5,
                            pagination: true,
                            search: true,
                        },
                        headers: {
                            // To avoid potential bugs keep the order as the records array
                            'title': {
                                'name': "Titolo",
                                'sort': true,
                                'classes': ''
                            },
                            'description': {
                                'name': "Descrizione",
                                'sort': true,
                                'classes': ''
                            },
                            'status': {
                                'name': "Stato",
                                'sort': true,
                                'classes': 'inline-flex items-center px-3 py-0.5 rounded-full text-sm font-medium bg-gray-100 text-gray-800'
                            },
                        },
                        records: {

                        }
                    },
                    simpleLocal: {
                        title: 'Simple Local',
                        settings: {
                            source: 'local',
                            sourceURL: null,
                            per_page: 10,
                            pagination: true,
                            search: false,
                        },
                        headers: {
                            // To avoid potential bugs keep the order as the records array
                            'title': {
                                'name': "Titolo",
                                'sort': true,
                                'classes': ''
                            },
                            'description': {
                                'name': "Descrizione",
                                'sort': false,
                                'classes': ''
                            },
                            'category': {
                                'name': "Categoria",
                                'sort': false,
                                'classes': ''
                            },
                            'author': {
                                'name': "Autore",
                                'sort': false,
                                'classes': ''
                            },
                            'status': {
                                'name': "Stato",
                                'sort': false,
                                'classes': 'inline-flex items-center px-3 py-0.5 rounded-full text-sm font-medium bg-gray-100 text-gray-800'
                            },
                        },
                        records: [{
                            "id": "c769dfc7-73d4-44b1-83cb-72e8cf37c007",
                            "title": "Durable Rubber Gloves",
                            "description": "Cum maxime eveniet officiis omnis magnam. Esse sint ipsam dicta ipsum. Aut saepe omnis delectus ipsum veritatis. Amet ex ea deleniti illo sunt. Eligendi harum laboriosam quas voluptas.",
                            "date": "1970-01-19T08:25:03.128+00:00",
                            "category": "Games",
                            "author": "Manfredi Costa",
                            "type": "Domanda",
                            "price": 1918.7,
                            "location": "Moscow",
                            "status": "Discreto"
                        }, {
                            "id": "15bc5e9a-43fa-4448-b2c9-86be8c1aabac",
                            "title": "Lightweight Steel Wallet",
                            "description": "In et sunt beatae ullam sed. Sequi blanditiis quas qui fugiat. Eum odio suscipit.",
                            "date": "1970-01-19T13:38:03.195+00:00",
                            "category": "Baby, Music & Sports",
                            "author": "Rosalino Fior",
                            "type": "Domanda",
                            "price": 1904.4,
                            "location": "Harare",
                            "status": "Buono"
                        }, {
                            "id": "e28ae3ba-b11a-4cbb-b6c4-26461ce5f1c0",
                            "title": "Gorgeous Granite Table",
                            "description": "Iure vel dolores doloremque temporibus occaecati. Quis animi sequi voluptatem iusto omnis illo consequuntur. Blanditiis impedit fugiat a porro ut. Reiciendis voluptatum sit voluptatem voluptatem similique.",
                            "date": "1970-01-19T16:17:36.536+00:00",
                            "category": "Games & Jewelry",
                            "author": "Laerte Donati",
                            "type": "Domanda",
                            "price": 1832.1,
                            "location": "Beijing",
                            "status": "Buono"
                        }, {
                            "id": "e2b653de-5bbf-49fd-ad34-b48801ede752",
                            "title": "Intelligent Plastic Gloves",
                            "description": "Temporibus et possimus eligendi est ut. Alias perspiciatis odio quibusdam commodi. Aut suscipit aut qui. Quidem aliquam pariatur harum eum at nulla. Consequuntur facere sed provident in est rerum.",
                            "date": "1970-01-19T16:50:27.287+00:00",
                            "category": "Baby & Garden",
                            "author": "Dott. Marianita De luca",
                            "type": "Offerta",
                            "price": 1830.7,
                            "location": "San Marino",
                            "status": "Buono"
                        }, {
                            "id": "205cc46d-0ede-429e-8068-e3c17b68cae9",
                            "title": "Awesome Paper Lamp",
                            "description": "Dicta vero iusto maiores saepe vitae iste expedita. Voluptates nesciunt consequatur. Blanditiis libero qui. Et a ratione et repudiandae. Nam quia sit facilis.",
                            "date": "1970-01-19T11:55:17.089+00:00",
                            "category": "Health",
                            "author": "Dr. Gavino Palmieri",
                            "type": "Domanda",
                            "price": 1803.4,
                            "location": "Porto-Novo",
                            "status": "Ottimo"
                        }, {
                            "id": "facf5158-d648-4fb4-b08e-93931df88410",
                            "title": "Lightweight Plastic Car",
                            "description": "Quis neque animi ea et omnis quia quo. Est aut aut est. Nihil sunt odio. Non sint rerum.",
                            "date": "1970-01-19T10:44:39.070+00:00",
                            "category": "Clothing, Electronics & Sports",
                            "author": "Donatella Martini",
                            "type": "Domanda",
                            "price": 1737.5,
                            "location": "Addis Ababa",
                            "status": "Discreto"
                        }, {
                            "id": "c5fa6934-b0ff-4c4e-8688-39bdc6b7a2ef",
                            "title": "Lightweight Silk Shirt",
                            "description": "Assumenda quibusdam cupiditate. Deserunt expedita optio fuga. Quia molestiae ut dolor.",
                            "date": "1970-01-19T16:07:41.045+00:00",
                            "category": "Beauty, Clothing & Sports",
                            "author": "Anastasio Bianchi",
                            "type": "Domanda",
                            "price": 1691.5,
                            "location": "Tirana",
                            "status": "Ottimo"
                        }, {
                            "id": "04c767e2-511a-4ab1-8c91-2a089e0b8b2b",
                            "title": "Ergonomic Concrete Coat",
                            "description": "Nemo consequuntur necessitatibus qui a et. Sed et a consequatur autem enim blanditiis. Magni rerum perferendis nulla.",
                            "date": "1970-01-19T16:59:55.102+00:00",
                            "category": "Music",
                            "author": "Eliziario Marino",
                            "type": "Offerta",
                            "price": 1643.1,
                            "location": "Muscat",
                            "status": "Discreto"
                        }, {
                            "id": "4c0271b7-0b62-4e01-9237-190e4b2bd464",
                            "title": "Durable Paper Chair",
                            "description": "Molestiae iste quam rerum necessitatibus. Dolorem molestiae sit voluptas eaque quisquam. Exercitationem similique atque eum provident in. Earum quo commodi et explicabo enim. Recusandae saepe quibusdam ab et rerum voluptatem earum.",
                            "date": "1970-01-19T10:57:24.784+00:00",
                            "category": "Garden & Kids",
                            "author": "Mariapia Sartori",
                            "type": "Domanda",
                            "price": 1631.6,
                            "location": "Taipei",
                            "status": "Discreto"
                        }, {
                            "id": "98621e4b-1755-427f-8c0d-5b25e40d54e2",
                            "title": "Incredible Bronze Clock",
                            "description": "Numquam eos illum consequatur sit eos aut libero. Aut consequuntur sed. Sit exercitationem id aperiam iure. Qui cupiditate iure minima enim esse. Laudantium tempore dicta porro cupiditate tempore.",
                            "date": "1970-01-19T09:46:58.558+00:00",
                            "category": "Baby, Beauty & Clothing",
                            "author": "Prisca Rizzo",
                            "type": "Domanda",
                            "price": 1614.2,
                            "location": "Castries",
                            "status": "Discreto"
                        }, {
                            "id": "6660058c-a912-4d91-bd6f-58369b83d02a",
                            "title": "Rustic Copper Chair",
                            "description": "Voluptatibus qui fugiat est asperiores quis praesentium omnis. Nostrum voluptatibus et eum commodi voluptatem voluptas facilis. Hic asperiores veniam.",
                            "date": "1970-01-19T11:37:47.299+00:00",
                            "category": "Automotive & Sports",
                            "author": "Sabino Galli",
                            "type": "Domanda",
                            "price": 1543.6,
                            "location": "Windhoek",
                            "status": "Buono"
                        }, {
                            "id": "1b8faf2f-5dbb-414a-93e4-a0eaa75cf05b",
                            "title": "Durable Rubber Knife",
                            "description": "Natus omnis sapiente commodi. Aperiam officiis unde. Quia eos est voluptas rerum voluptatem a quibusdam.",
                            "date": "1970-01-19T09:43:28.374+00:00",
                            "category": "Kids & Sports",
                            "author": "Arduino D'amico",
                            "type": "Domanda",
                            "price": 1537.1,
                            "location": "Ulaanbaatar",
                            "status": "Buono"
                        }, {
                            "id": "3291de69-ae01-421d-a610-223913bc8f38",
                            "title": "Heavy Duty Granite Computer",
                            "description": "Aut nulla sint. Culpa eum libero in excepturi totam. Atque aspernatur nihil provident corporis.",
                            "date": "1970-01-19T11:01:43.596+00:00",
                            "category": "Garden",
                            "author": "Ninfa Valentini",
                            "type": "Domanda",
                            "price": 1481.4,
                            "location": "Ankara",
                            "status": "Buono"
                        }, {
                            "id": "bde89f65-877e-4449-ad80-ed562d107565",
                            "title": "Heavy Duty Iron Table",
                            "description": "Occaecati culpa officiis perspiciatis laudantium voluptas aliquid. Suscipit nihil accusamus tenetur rem placeat voluptatem cumque. Id illo molestias eos molestiae ab et fuga. Officiis quo rem exercitationem eaque consectetur. At quo adipisci commodi iste sint non amet.",
                            "date": "1970-01-19T12:48:51.163+00:00",
                            "category": "Automotive",
                            "author": "Sig. Alan Morelli",
                            "type": "Offerta",
                            "price": 1468.8,
                            "location": "Nuku'alofa",
                            "status": "Buono"
                        }, {
                            "id": "22196426-312c-4ae5-b68b-b8b3fafad504",
                            "title": "Rustic Wool Table",
                            "description": "Ducimus repudiandae quis cupiditate quaerat vel. Totam quasi non eligendi pariatur. Recusandae quia dolorum.",
                            "date": "1970-01-19T11:45:34.672+00:00",
                            "category": "Industrial",
                            "author": "Dott. Ione Serr",
                            "type": "Domanda",
                            "price": 1397.4,
                            "location": "Victoria",
                            "status": "Buono"
                        }, {
                            "id": "6ad7259a-fc5e-4972-85ea-dc6a72245a69",
                            "title": "Intelligent Cotton Plate",
                            "description": "Rerum quos ut sed. Ipsum reprehenderit impedit nihil exercitationem. In ab ut repudiandae velit laudantium perspiciatis accusamus. Fugit eius itaque asperiores velit sint eveniet.",
                            "date": "1970-01-19T16:17:02.506+00:00",
                            "category": "Beauty",
                            "author": "Quirino De Angelis",
                            "type": "Offerta",
                            "price": 1308.8,
                            "location": "Lisbon",
                            "status": "Ottimo"
                        }, {
                            "id": "b92d0c42-f769-403b-a017-2979b6301266",
                            "title": "Enormous Iron Watch",
                            "description": "Illo assumenda exercitationem. Maxime natus maxime est qui voluptas voluptatem. Quia ut ut exercitationem cumque.",
                            "date": "1970-01-19T10:34:03.911+00:00",
                            "category": "Electronics & Shoes",
                            "author": "Ing. Artemide Bernardi",
                            "type": "Domanda",
                            "price": 1269.8,
                            "location": "Brussels",
                            "status": "Buono"
                        }, {
                            "id": "efcc402c-6974-4350-b60f-ed4cfc8bc722",
                            "title": "Practical Iron Shirt",
                            "description": "Ea praesentium aliquam possimus placeat quisquam maiores sapiente. Repellendus temporibus expedita reprehenderit et quidem quisquam. Mollitia est qui amet est eum. Ut quos similique praesentium.",
                            "date": "1970-01-19T15:02:29.469+00:00",
                            "category": "Beauty",
                            "author": "Gianantonio Piras",
                            "type": "Offerta",
                            "price": 1252.8,
                            "location": "Kampala",
                            "status": "Discreto"
                        }, {
                            "id": "4a638b35-5e9e-47eb-8b1b-4dddbefc7e9b",
                            "title": "Aerodynamic Granite Shirt",
                            "description": "Ducimus iste praesentium quas et non quia molestiae. Laudantium quam eaque. Et eos qui asperiores dignissimos neque. Quisquam repellendus consectetur asperiores illo.",
                            "date": "1970-01-19T12:17:48.732+00:00",
                            "category": "Computers",
                            "author": "Zaccaria De luca",
                            "type": "Domanda",
                            "price": 1077.2,
                            "location": "Taipei",
                            "status": "Ottimo"
                        }, {
                            "id": "e0692cce-e835-4cdc-a51b-0873d658a777",
                            "title": "Sleek Linen Lamp",
                            "description": "Odit suscipit qui est accusantium sequi maxime iste. Aut non ab iusto iure sed molestias. Laboriosam repudiandae ut quod optio.",
                            "date": "1970-01-19T14:13:22.636+00:00",
                            "category": "Home",
                            "author": "Tazio Morelli",
                            "type": "Domanda",
                            "price": 1046.7,
                            "location": "Banjul",
                            "status": "Buono"
                        }, {
                            "id": "7ad666d4-bb17-46c6-ab05-c0173fb822af",
                            "title": "Intelligent Aluminum Wallet",
                            "description": "Nisi voluptate ratione omnis ut sint praesentium ducimus. Dolorum labore incidunt similique rerum velit consectetur eos. Molestiae sed illo corporis rerum qui. Fugiat hic aliquid nemo adipisci doloremque laboriosam. Qui eaque ipsum sed veniam sapiente et sit.",
                            "date": "1970-01-19T12:30:10.163+00:00",
                            "category": "Books, Industrial & Outdoors",
                            "author": "Clea Grassi",
                            "type": "Domanda",
                            "price": 1045.8,
                            "location": "Vaduz",
                            "status": "Discreto"
                        }, {
                            "id": "661c2bae-3bc0-4dea-8a01-6c919f65ce86",
                            "title": "Gorgeous Iron Car",
                            "description": "Libero asperiores qui aliquam reprehenderit enim sequi recusandae. Voluptatem recusandae tempora ut accusamus aut sint. Ea autem suscipit quis ipsam consectetur.",
                            "date": "1970-01-19T16:52:24.439+00:00",
                            "category": "Beauty, Clothing & Computers",
                            "author": "Soriana Ferretti",
                            "type": "Domanda",
                            "price": 1043.1,
                            "location": "London",
                            "status": "Buono"
                        }, {
                            "id": "0bbdc3ec-55d6-452e-8c7c-4c475916e7ba",
                            "title": "Incredible Granite Gloves",
                            "description": "Facilis dolore nostrum et tempora fugiat fugiat sint. Quasi alias ipsam suscipit. Architecto aut dolorum harum quam qui. Optio ut ea voluptas. Commodi est rerum voluptatem ut qui deserunt.",
                            "date": "1970-01-19T09:48:44.242+00:00",
                            "category": "Electronics",
                            "author": "Manuele Basile",
                            "type": "Offerta",
                            "price": 1010.0,
                            "location": "Nuku'alofa",
                            "status": "Buono"
                        }, {
                            "id": "5badff4f-6eb1-4f4a-8038-c1615bf76bd3",
                            "title": "Synergistic Wool Bottle",
                            "description": "Laudantium nemo quia. Iure ipsum voluptas debitis non aut a. Nobis numquam numquam iusto ad dicta aut atque. Eos suscipit aut ipsa atque dolor ullam saepe. Alias reiciendis repudiandae.",
                            "date": "1970-01-19T15:59:50.268+00:00",
                            "category": "Industrial, Music & Toys",
                            "author": "Sig. Dante Morelli",
                            "type": "Offerta",
                            "price": 942.8,
                            "location": "N'Djamena",
                            "status": "Ottimo"
                        }, {
                            "id": "f6ba79f7-6d2e-4dfa-ba46-a9402b876f22",
                            "title": "Aerodynamic Paper Gloves",
                            "description": "Illo sint ipsa quisquam totam. Voluptate maxime veritatis reprehenderit numquam voluptatem similique sed. Eos fugiat molestiae dolor facilis voluptate assumenda aut. Itaque ut quas inventore non quis. Ex eius sint quidem laborum voluptatem.",
                            "date": "1970-01-19T14:55:23.292+00:00",
                            "category": "Movies",
                            "author": "Neri Bruno",
                            "type": "Offerta",
                            "price": 941.3,
                            "location": "Maputo",
                            "status": "Buono"
                        }, {
                            "id": "a1dbe11a-8acf-4e7e-830c-c3f0859e9743",
                            "title": "Lightweight Copper Keyboard",
                            "description": "Eos non aut deleniti quis omnis repudiandae laudantium. Dignissimos eius illo incidunt culpa voluptatem asperiores nostrum. Sed quia laborum. Est rerum in quod id.",
                            "date": "1970-01-19T11:43:17.145+00:00",
                            "category": "Books & Grocery",
                            "author": "Liborio Grasso",
                            "type": "Offerta",
                            "price": 891.9,
                            "location": "Pristina",
                            "status": "Ottimo"
                        }, {
                            "id": "800f313c-fa61-43ef-b0a1-8e0eb05fcd93",
                            "title": "Enormous Granite Wallet",
                            "description": "Molestias illum modi eligendi dolor aut molestias et. Aperiam qui mollitia eum vel. Sequi nesciunt et incidunt exercitationem quis mollitia soluta.",
                            "date": "1970-01-19T11:59:13.881+00:00",
                            "category": "Beauty",
                            "author": "Ing. Diamante Vitale",
                            "type": "Domanda",
                            "price": 861.8,
                            "location": "Riga",
                            "status": "Buono"
                        }, {
                            "id": "913773cd-046f-4919-9c5a-74fbad322796",
                            "title": "Sleek Silk Clock",
                            "description": "Soluta perspiciatis exercitationem recusandae. Dolore quo impedit ea et aut. Impedit at blanditiis. Culpa aut ullam saepe. Totam dolorem fuga veritatis sunt magni tempora facere.",
                            "date": "1970-01-19T13:46:30.280+00:00",
                            "category": "Tools",
                            "author": "Ludovico Romano",
                            "type": "Domanda",
                            "price": 849.6,
                            "location": "Quito",
                            "status": "Ottimo"
                        }, {
                            "id": "1cfea8bc-e9a5-4ab9-b627-f58c7322a0db",
                            "title": "Heavy Duty Wooden Watch",
                            "description": "Labore porro voluptas nihil qui. Repellat et consequatur perferendis. Beatae fuga omnis odio est architecto nulla.",
                            "date": "1970-01-19T15:54:12.846+00:00",
                            "category": "Kids",
                            "author": "Graziano Cont",
                            "type": "Domanda",
                            "price": 808.8,
                            "location": "Kampala",
                            "status": "Discreto"
                        }, {
                            "id": "d1759ca9-c424-442a-8436-9acfa3c402f9",
                            "title": "Practical Wooden Bench",
                            "description": "Doloribus natus quo blanditiis voluptas et qui temporibus. Nam et voluptas quis exercitationem veritatis nisi. Aut sint et eius laboriosam. Facilis magnam sunt esse sapiente omnis officiis. Eius placeat rem tenetur sint officiis dicta natus.",
                            "date": "1970-01-19T13:14:08.586+00:00",
                            "category": "Health & Kids",
                            "author": "Lia Pellegrini",
                            "type": "Offerta",
                            "price": 785.0,
                            "location": "Havana",
                            "status": "Buono"
                        }, {
                            "id": "093fad17-4e3b-4e28-b0b5-f858bc5e5f28",
                            "title": "Ergonomic Steel Bench",
                            "description": "Enim voluptatem consequatur corrupti fugiat id velit. Saepe porro optio aut praesentium voluptatem eligendi aut. Et dolores ut minus maxime. Quis architecto consectetur sunt provident aut officiis eos. Pariatur ut quo nobis est nihil quam laborum.",
                            "date": "1970-01-19T08:56:13.931+00:00",
                            "category": "Computers, Health & Industrial",
                            "author": "Sirio Fior",
                            "type": "Domanda",
                            "price": 769.1,
                            "location": "Ankara",
                            "status": "Discreto"
                        }, {
                            "id": "172989e8-05bb-484e-936c-cfc9546ada55",
                            "title": "Awesome Granite Keyboard",
                            "description": "Saepe quaerat animi. Unde non hic pariatur nulla. Tenetur vel dolor autem magni.",
                            "date": "1970-01-19T12:12:28.416+00:00",
                            "category": "Health & Movies",
                            "author": "Ausonio Costantin",
                            "type": "Domanda",
                            "price": 746.2,
                            "location": "San Salvador",
                            "status": "Buono"
                        }, {
                            "id": "b47201d9-6f65-4ff4-b5ce-d0f82c02606b",
                            "title": "Gorgeous Bronze Wallet",
                            "description": "Quisquam dolore laudantium. Qui doloremque error voluptas placeat. Blanditiis ad in. Repellendus aspernatur quasi aspernatur doloribus voluptatem officia consequatur. Quisquam quam qui voluptatibus eius.",
                            "date": "1970-01-19T12:39:46.775+00:00",
                            "category": "Games & Health",
                            "author": "Zelida Martino",
                            "type": "Offerta",
                            "price": 736.2,
                            "location": "Maputo",
                            "status": "Discreto"
                        }, {
                            "id": "1829880c-d980-4322-a740-6ceae2f786c8",
                            "title": "Enormous Copper Bottle",
                            "description": "Aut veritatis asperiores harum dolores. Nulla velit aut aliquam unde eum. Eum id quo aut et autem rerum.",
                            "date": "1970-01-19T11:40:26.063+00:00",
                            "category": "Outdoors & Sports",
                            "author": "Oreste D'angelo",
                            "type": "Offerta",
                            "price": 715.2,
                            "location": "Baku",
                            "status": "Buono"
                        }, {
                            "id": "d04f2f3d-35ab-4d2e-85d3-70dfaebbfe49",
                            "title": "Lightweight Iron Car",
                            "description": "Error ut nam consequuntur ratione illum excepturi molestiae. Commodi commodi qui nemo iure quibusdam. Vel praesentium architecto nisi nihil. Et voluptatem ut iusto laudantium voluptas.",
                            "date": "1970-01-19T15:55:32.573+00:00",
                            "category": "Baby, Beauty & Industrial",
                            "author": "Bettino Rizzo",
                            "type": "Domanda",
                            "price": 703.3,
                            "location": "Bucharest",
                            "status": "Discreto"
                        }, {
                            "id": "957fb8f3-e17d-4cb2-a794-2089684a80dd",
                            "title": "Mediocre Iron Clock",
                            "description": "Debitis consequatur explicabo et. Itaque voluptatem blanditiis. Aliquid enim recusandae at quae debitis quia. Et voluptatibus est rerum omnis.",
                            "date": "1970-01-19T14:07:42.012+00:00",
                            "category": "Outdoors",
                            "author": "Dott. Diana Bellini",
                            "type": "Offerta",
                            "price": 676.4,
                            "location": "Luanda",
                            "status": "Discreto"
                        }, {
                            "id": "88a8a59e-b7ca-4114-8dea-fbeca1ebd79c",
                            "title": "Fantastic Cotton Gloves",
                            "description": "Hic ducimus illo totam. Enim modi corporis molestiae et. Dolor ducimus debitis ducimus aliquid autem eius et. Molestiae repellat ipsam architecto quia qui similique.",
                            "date": "1970-01-19T12:07:52.357+00:00",
                            "category": "Health, Shoes & Toys",
                            "author": "Dott. Fulvio Silvestri",
                            "type": "Domanda",
                            "price": 659.6,
                            "location": "Khartoum",
                            "status": "Buono"
                        }, {
                            "id": "d00fb5f9-7b92-4481-9a15-45f263e4d086",
                            "title": "Incredible Aluminum Wallet",
                            "description": "Non velit vel quia maxime perspiciatis quibusdam. Aut a est hic recusandae. Deleniti vel et ut ad animi saepe non.",
                            "date": "1970-01-19T08:43:09.830+00:00",
                            "category": "Music",
                            "author": "Thea Sala",
                            "type": "Domanda",
                            "price": 646.6,
                            "location": "Bujumbura",
                            "status": "Discreto"
                        }, {
                            "id": "63a0ef62-ce5c-45ca-8260-fb15cada1982",
                            "title": "Heavy Duty Concrete Keyboard",
                            "description": "Dolor inventore accusamus culpa. Aspernatur nihil aperiam et in laboriosam deleniti. Facere et quo nihil voluptas quod quod qui. Sit minus qui laborum et.",
                            "date": "1970-01-19T12:17:34.527+00:00",
                            "category": "Kids",
                            "author": "Dr. Egisto Damico",
                            "type": "Offerta",
                            "price": 633.0,
                            "location": "Sanaa",
                            "status": "Discreto"
                        }, {
                            "id": "a033dca6-555c-475b-b283-4b8199688181",
                            "title": "Incredible Granite Watch",
                            "description": "Placeat et id asperiores veritatis aut. Quae accusamus qui quibusdam necessitatibus est adipisci omnis. Nostrum voluptatem dolorum expedita. Eligendi consequatur quae repellat. Est modi officiis aliquam.",
                            "date": "1970-01-19T16:11:39.135+00:00",
                            "category": "Baby, Computers & Games",
                            "author": "Emanuel Ross",
                            "type": "Domanda",
                            "price": 554.0,
                            "location": "Moscow",
                            "status": "Discreto"
                        }, {
                            "id": "8605e3f0-f968-4757-98b2-15f5c57ca03d",
                            "title": "Ergonomic Rubber Chair",
                            "description": "Et nam voluptates magnam tenetur eligendi ea ullam. Fugiat delectus qui. Ut qui aut et sunt animi laboriosam commodi.",
                            "date": "1970-01-19T09:24:44.561+00:00",
                            "category": "Clothing & Home",
                            "author": "Dr. Giobbe Giordano",
                            "type": "Offerta",
                            "price": 538.3,
                            "location": "Cairo",
                            "status": "Buono"
                        }, {
                            "id": "3919c3f9-432b-4480-a3b0-e41b20b1ae0e",
                            "title": "Lightweight Wooden Bottle",
                            "description": "Nostrum quod quas est qui veritatis sit. Qui omnis beatae quaerat quo porro. Cum eligendi id nihil. Ea quia tempore ut similique assumenda et. Et non ea possimus.",
                            "date": "1970-01-19T15:18:13.658+00:00",
                            "category": "Music & Tools",
                            "author": "Mariagiulia Esposito",
                            "type": "Domanda",
                            "price": 507.9,
                            "location": "Melekeok",
                            "status": "Buono"
                        }, {
                            "id": "1d628c99-4f6f-45b3-b88b-9a0a44f24dfd",
                            "title": "Practical Rubber Watch",
                            "description": "Minus incidunt recusandae iste aut. Nobis ut est. Tempora quo ullam omnis quia esse provident reprehenderit. Non quis voluptatibus soluta quos non. Esse dolor voluptates.",
                            "date": "1970-01-19T13:33:04.110+00:00",
                            "category": "Games, Garden & Shoes",
                            "author": "Eufemia Ferrara",
                            "type": "Offerta",
                            "price": 466.1,
                            "location": "Brussels",
                            "status": "Discreto"
                        }, {
                            "id": "723e14c8-07f5-4b86-86fa-09a6442a10aa",
                            "title": "Gorgeous Granite Bag",
                            "description": "Nostrum eaque qui aut suscipit sit. Voluptas tempora minima molestiae. Quod eveniet omnis quod culpa. Occaecati amet aut. Corrupti voluptate sint nihil et.",
                            "date": "1970-01-19T09:24:04.231+00:00",
                            "category": "Clothing",
                            "author": "Artemide Messina",
                            "type": "Offerta",
                            "price": 409.5,
                            "location": "Madrid",
                            "status": "Buono"
                        }, {
                            "id": "f58c7967-b54e-4c3c-b9d9-e16535dc1828",
                            "title": "Intelligent Leather Bench",
                            "description": "Sapiente atque illum architecto eaque voluptatem ratione. Qui voluptas unde sunt nulla incidunt tenetur numquam. Iure est sint beatae quisquam accusamus error. Ab temporibus quidem voluptatem.",
                            "date": "1970-01-19T16:03:33.306+00:00",
                            "category": "Baby",
                            "author": "Damiana Gentile",
                            "type": "Domanda",
                            "price": 313.8,
                            "location": "Belmopan",
                            "status": "Buono"
                        }, {
                            "id": "6cb83f38-0fbd-42d0-94e6-1ece5834d82b",
                            "title": "Sleek Silk Table",
                            "description": "Similique est fugiat. Eius possimus quisquam voluptatem at quas. Eos saepe voluptatum quos voluptatem magnam.",
                            "date": "1970-01-19T08:59:47.618+00:00",
                            "category": "Home",
                            "author": "Ulrico Basile",
                            "type": "Offerta",
                            "price": 166.1,
                            "location": "Rabat",
                            "status": "Buono"
                        }, {
                            "id": "8751de95-fc19-4d46-badc-aa0d913800bc",
                            "title": "Synergistic Aluminum Plate",
                            "description": "Vel voluptatem et aut. Repellendus eaque ut. Minima iste aliquid omnis non et voluptate. Dicta maxime ut culpa magni. Qui et recusandae impedit sunt.",
                            "date": "1970-01-19T16:50:26.752+00:00",
                            "category": "Electronics, Garden & Shoes",
                            "author": "Filomena Lombardo",
                            "type": "Offerta",
                            "price": 156.5,
                            "location": "Paris",
                            "status": "Buono"
                        }, {
                            "id": "028d96cd-47d1-4a5e-bd0d-18c44235ae6f",
                            "title": "Lightweight Bronze Bench",
                            "description": "Corrupti necessitatibus architecto adipisci rerum iure distinctio qui. Consequuntur sint cumque repellat dolore non quia porro. Quo dolor vel aut.",
                            "date": "1970-01-19T09:03:12.025+00:00",
                            "category": "Clothing, Electronics & Shoes",
                            "author": "Fortunata Caputo",
                            "type": "Offerta",
                            "price": 56.6,
                            "location": "Montevideo",
                            "status": "Buono"
                        }, {
                            "id": "d4e49175-990e-4756-ab04-e5272b507c84",
                            "title": "Gorgeous Plastic Clock",
                            "description": "Dolores ut et. Facilis ut qui laudantium dignissimos neque. Consequatur error asperiores ut. Error esse mollitia dignissimos.",
                            "date": "1970-01-19T15:35:10.471+00:00",
                            "category": "Jewelry",
                            "author": "Erminia Sartori",
                            "type": "Domanda",
                            "price": 28.1,
                            "location": "Vienna",
                            "status": "Buono"
                        }, {
                            "id": "aca06a55-ae0c-43ba-a968-f6b819bdaf9a",
                            "title": "Synergistic Wool Pants",
                            "description": "Ut totam deserunt quia. Qui sunt sed est minus enim accusamus. Perferendis aliquid qui facere quia.",
                            "date": "1970-01-19T10:28:57.646+00:00",
                            "category": "Health, Outdoors & Toys",
                            "author": "Sig. Fabiano Mazza",
                            "type": "Offerta",
                            "price": 9.4,
                            "location": "Mogadishu",
                            "status": "Discreto"
                        }]
                    }
                }
            }
        },
        computed: {}
    }

    // This starter template is using Vue 3 experimental <script setup> SFCs
    // Check out https://github.com/vuejs/rfcs/blob/script-setup-2/active-rfcs/0000-script-setup.md
</script>