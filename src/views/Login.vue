<template>
    <section class="container-fluid">
        <div class="row justify-content-center">
            <div class="col-lg-4">
                <div class="login-panel bg-white text-left">
                    <span style="color:#A4CC36;font-weight: bold; font-size:65px "> PIX</span>
                    <span style="color:#004B6C;font-weight: bold;font-size:65px ">Select</span>
                    <br>
                    <form action="">
                        <div class="form-group">
                             <lable class="input-label">Company ID</lable>
                            <input v-model="companyId" type="number" class="form-control" placeholder="ID">
                        </div>
                        <div class="form-group">
                             <lable class="input-label">Email</lable>
                            <input v-model="email" type="text" class="form-control" placeholder="Email">
                        </div>
                        <div class="form-group">
                             <lable class="input-label">Password</lable>
                            <input v-model="password" type="password" class="form-control" placeholder="Password">
                        </div>
                        <br>
                        <div class="form-group d-flex justify-content-center">
                            <button class="btn btn-primary w-25" id="login" @click.prevent="login">Login</button>
                            
                        </div>
                    </form>
                </div>
            </div>
        </div>
    </section>
</template>

<script>
import axios from 'axios';

export default {
    
    data() {
        return {
            url: process.env.VUE_APP_API_ENDPOINT || "/",
            companyId: null,
            email:'',
            password: '',
            isLoggingIn: false,
            isAlertShow: false
        }
    },
    methods: {
        
        login() {
            console.log("companyıd", this.companyId);
            axios.post(`https://marketing.pixselect.com.tr:50300/login`, {
                companyId: this.companyId,
                username: this.email,
                password: this.password,
            },{withCredentials: true}).then((response) => {
                console.log("response", response)
          this.$router.push({name: 'home'})
        })
        },

        redirect() {
            this.$router.push({name: 'home'})
        }
    }
}
</script>

<style lang="scss">
.widget {
    margin: 0;
    height: unset;
}
.login-panel {
    position: relative;
    padding: 200px 0;
    .alert {
        opacity: 0;
        position: absolute;
        width: 100%;
        top: 100px;
        transition: all .5s;
        &.alert-primary {
            background-color: #007BFF;
            color: #fff;
            font-size: 18px;
            border: none;
        }
        .widget {
            position: absolute;
            right: 5px;
            top: 0;
            margin: 10px;
        }
    }
}
</style>