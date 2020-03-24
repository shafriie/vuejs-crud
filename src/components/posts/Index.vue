<template>
    <div class="posts">
        <div class="container-fluid">
            <h1>List Data Posts</h1>
            <div class="row" style="margin-top: 40px">
                <div class="col-md-12">
                    
                    <router-link class="btn btn-primary" to="/create">Add Data</router-link>
                    <br><br>

                    <table class="table table-striped table-hover">
                        <thead>
                            <tr>
                                <th>No</th>
                                <th>Title</th>
                                <th>Content</th>
                                <th>Action</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr v-for="(post, index) in posts" :key="index">
                                <td>{{ index + 1 }}.</td>
                                <td>{{ post.title }}</td>
                                <td>{{ post.content }}</td>
                                <td>
                                    <!-- <a href="" class="btn btn-success">Edit</a>  -->
                                    <router-link class="btn btn-success" :to="{name: 'edit', params: {id: post.id} }">Edit</router-link>
                                    &nbsp;
                                    <!-- <a href="" class="btn btn-danger">Delete</a> -->
                                    <button @click.prevent="PostDelete(post.id)" class="btn btn-danger">Delete</button>
                                </td>
                            </tr>
                        </tbody>
                    </table>

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
                posts: []
            }
        },
        created() {
            axios.get('http://localhost:8000/api/v1/posts').then(response => {
                this.posts = response.data.data
            });
        },
        methods: {
            PostDelete(id) 
            {
                if(confirm('Apakah anda ingin menghapus data ini?')){
                    axios.delete('http://localhost:8000/api/v1/posts/'+id).then(response => {
                        this.posts.splice(this.posts.indexOf(id), 1);
                        console.log(response)
                    }).catch(error => {
                        console.log(error.response)
                    });
                }
            }
        }

    }
</script>