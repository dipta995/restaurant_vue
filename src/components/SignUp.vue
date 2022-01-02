<template>
    <main>
        <div class="inputbox">
            <label>Name</label>
            <input v-model="name" type="text"  class="input-style" />
        </div>
        <div class="inputbox">
            <label>Email</label>
            <input v-model="email" type="email" class="input-style" />
        </div>
        <div class="inputbox">
            <label>Phone No</label>
            <input v-model="phone" type="text"  class="input-style" />
        </div>
        <div class="inputbox">
            <label>Password</label>
            <input v-model="password" type="password"  class="input-style" />
        </div>
        <div class="inputbox">
            <label>Address</label>
            <textarea v-model="address"  class="input-style"></textarea>
        </div>
         
            <input v-on:click="signUp" type="submit" value="sign up"  class="input-submit" />
        
    </main>
</template>
<script>
import axios from 'axios'
export default {
    name: 'SignUp',
    data()
    {
        return {
            name:'',
            email:'',
            phone:'',
            password:'',
            address:''
        }
    },
    methods: {
        async signUp()
        {
            console.warn("Signup",this.name,this.email,this.password)
            let result = await axios.post("http://localhost:3000/users",{
                name:this.name,
                email:this.email,
                phone:this.phone,
                password:this.password,
                address:this.address
            });
            console.warn(result);
            if(result.status==201)
            {
                localStorage.setItem("user-info",JSON.stringify(result.data));
                this.$router.push({name:'Home'});
            }
           
        }
    },
    mounted() {
        let user =localStorage.getItem('user-info');
        if(user)
        {
            this.$router.push({name:'Home'});
        }
    },
}

</script>
<style>
main{
    height:400px;
    margin:0 auto;
    width:960px;
}
label{
   
   width:200px;
   margin-top:12px;
    float:left;
    

}
    .input-style{
        float:left;
        padding:10px;
        width:400px;
        border: 1px solid green;
        border-radius:10px;
    }
.inputbox{
    height:50px;
    }
    .input-submit{
    margin-top:40px;
    margin-left:-750px;
    padding:10px 20px;
    color:white;
    background-color:green;
    border:2px solid green;
    border-radius:5px;


    }
     
</style>