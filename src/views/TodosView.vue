<template>
    <div class="container">

        <nav aria-label="breadcrumb text-right">
        <ol class="breadcrumb ">
            <li class="breadcrumb-item"><a href="/">Home</a></li>
            <li class="breadcrumb-item active" aria-current="page">Albums</li>
        </ol>
        </nav>

        <!-- Isi Konten -->
        <div class="card">
            <div class="card-body">
                
                <h3>List Todos</h3>

                <div class="row grid">

                    <div class="col-lg-10 offset-1 mt-3">
                        <table class="table table-bordered table-hover table-striped">
                            <thead class="thead-dark">
                                <tr>
                                    <th class="text-center" width="5%" scope="col">#</th>
                                    <th class="text-center" scope="col">Title</th>
                                    <th class="text-center" scope="col">User ID</th>
                                    <th class="text-center" scope="col">Status</th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr v-for="(todo, index) in todos" :key="todo.id">
                                    <th class="text-center" scope="row">{{ index + 1 }}</th>
                                    <td class="text-left text-capitalize">{{ todo.title }}</td>
                                    <td class="text-center">#00{{ todo.userId }}</td>
                                    <td class="text-center" v-html="todo.completed ? '<span class=&quot;badge text-bg-success p-2&quot;>Completed</span>' : '<span class=&quot;badge text-bg-warning p-2&quot;>Pending</span>'"></td>
                                </tr>
                            </tbody>
                        </table>
                    </div>

                </div>
            </div>
        </div>


    </div>
</template>

<script>
    import axios from 'axios';
    export default {
        data() {
            return {
                todos: [],
            };
        },
        created() {
            this.fetchTodos();
        },
        methods: {
        async fetchTodos() {
            try {
                const response = await axios.get('https://jsonplaceholder.typicode.com/todos?_limit=50');
                this.todos = response.data;
            } catch (error) {
                console.error('Error fetching todos:', error);
            }
        },
        },
    };

    // export default {
        // data() {
        //     return {
        //     todos: [],
        //     };
        // },
        // created() {
        //     this.fetchTodos();
        // },
        // methods: {
        //     async fetchTodos() {
        //     try {
        //         const response = await axios.get('https://jsonplaceholder.typicode.com/todos');
        //         this.todos = response.data;
        //     } catch (error) {
        //         console.error('Error fetching todos:', error);
        //     }
        //     },
        // },
    // };
    
</script>

