<template>
  <div class="container login-container">
        <div class="row">
            <div class="col-md-2">

            </div>
            <div class="col-md-8 login-form-1">
                <h3>Sign In Please</h3>
                <form @submit.prevent="PostLogin">
                    <p v-if="message" :class="[className]">{{ message }}</p>
                    <div class="form-group">
                        <input type="email" required class="form-control" placeholder="Your Email *" v-model="result.email" />
                    </div>
                    <div class="form-group">
                        <input type="password" autocomplete="off" required class="form-control" placeholder="Your Password *" v-model="result.password" />
                    </div>
                    <div class="form-group">
                        <input type="submit" class="btnSubmit" value="Login" />
                    </div>
                    <div class="form-group">
                        <a href="#" class="ForgetPwd">Forget Password?</a>
                    </div>
                </form>
            </div>
            <div class="col-md-2">

            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios';
export default {
    data(){
        return {
            result: {},
            message: '',
            className: ''
        }
        
    },
    created(){
        // console.log(this.result)
        if(localStorage.getItem('jwtToken')){
            this.$router.push({
                name: 'posts'
            })
        }
    },
    methods: {
        PostLogin(){
            this.message = ''
            axios.post('http://localhost:8000/api/v1/login', this.result).then(res => {
                // console.log(res)
                // alert(res.data.message)
                this.message = res.data.message;
                this.className = 'alert alert-success'
                
                localStorage.setItem('jwtToken', res.data.token)

                setTimeout(function(){ 
                    location.href = '/'
                 }, 2000);

            }).catch(err => {
                // console.log(err)
                this.message = err.response.data.message
                this.className = 'alert alert-danger'
            });
            // alert('wew')
            // console.log(this.result)
        }
    }
}
</script>

<style>
.login-container{
    margin-top: 5%;
    margin-bottom: 5%;
}
.login-form-1{
    padding: 5%;
    box-shadow: 0 5px 8px 0 rgba(0, 0, 0, 0.2), 0 9px 26px 0 rgba(0, 0, 0, 0.19);
}
.login-form-1 h3{
    text-align: center;
    color: #333;
}
.login-form-2{
    padding: 5%;
    background: #0062cc;
    box-shadow: 0 5px 8px 0 rgba(0, 0, 0, 0.2), 0 9px 26px 0 rgba(0, 0, 0, 0.19);
}
.login-form-2 h3{
    text-align: center;
    color: #fff;
}
.login-container form{
    padding: 10%;
}
.btnSubmit
{
    width: 50%;
    border-radius: 1rem;
    padding: 1.5%;
    border: none;
    cursor: pointer;
}
.login-form-1 .btnSubmit{
    font-weight: 600;
    color: #fff;
    background-color: #0062cc;
}
.login-form-2 .btnSubmit{
    font-weight: 600;
    color: #0062cc;
    background-color: #fff;
}
.login-form-2 .ForgetPwd{
    color: #fff;
    font-weight: 600;
    text-decoration: none;
}
.login-form-1 .ForgetPwd{
    color: #0062cc;
    font-weight: 600;
    text-decoration: none;
}

</style>