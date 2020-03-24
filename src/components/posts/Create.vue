<template>
    <div class="tambah-posts">
        <div class="container-fluid">
            <h1>Tambah Data Posts</h1>
            <div class="row" style="margin-top: 40px">
                <div class="col-md-12">
                    <form @submit.prevent="PostStore">
                        <div class="form-group">
                            <label for="title">Title:</label>
                            <input type="text" class="form-control" placeholder="Enter Title" v-model="posts.title">
                            <p v-if="validation.title" class="text-danger">{{ validation.title[0] }}</p>
                        </div>
                        <div class="form-group">
                            <label for="content">Content:</label>
                            <textarea placeholder="Content" class="form-control" v-model="posts.content" cols="30" rows="5"></textarea>
                            <p v-if="validation.content" class="text-danger">{{ validation.content[0] }}</p>
                        </div>
                        
                        <router-link class="btn btn-danger" :to="{name: 'posts'}">Back</router-link>
                        &nbsp;
                        <button type="submit" class="btn btn-primary">Submit</button>
                    </form>
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
                posts: {},
                validation: []
            }
        },
        created() {
            
        },
        methods: {
            PostStore() {
                axios.post('http://localhost:8000/api/v1/posts', this.posts).then(res => {
                    // console.log(res);
                    alert(res.data.message)
                    this.$router.push({
                        name: 'posts'
                    })
                }).catch(err => {
                    // console.log(err.response.data);
                    this.validation = err.response.data.data;
                    // console.log(this.validation);
                });
            }
            
        }

    }
</script>