<template>
    <Header />
    <h1>Welcome on Add Restaurant Page</h1>
    <div class="container">
    <form>
            <input type="text" name="name" v-model="restaurant.name" placeholder="Enter Name Here"/>
            <input type="text" name="contact" v-model="restaurant.contact" placeholder="Enter Contact Here"/>
            <input type="text" name="address" v-model="restaurant.address" placeholder="Enter Address Here"/>
            <button type="button" v-on:click="addRestaurant">Add New Restaurant</button>
    </form>
    </div>
</template>

<script>
import Header from './Header.vue'
import axios from 'axios'
export default {
    name: 'Add',
    components:{
        Header
    },
    data()
    {
        return {
            restaurant : {
                name:'',
                address:'',
                contact:''
            }
        }
    },
    methods:{
        async addRestaurant()
        {
            //console.log(this.restaurant);
            const result = await axios.post("http://localhost:3000/restaurant",{
              name:this.restaurant.name,
              contact: this.restaurant.contact,
              address: this.restaurant.address  
            });
            //console.log(result);
            if(result.status==201)
            {
                this.$router.push({name:'Home'});
            }
        }
    },
    mounted()
    {
        let user = localStorage.getItem('user-info');
        if(!user)
        {
            this.$router.push({name:'SignUp'})
        }
    }
}
</script>
