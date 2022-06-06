<template>
    <Header />
    <h1>Welcome on Restaurant Update Page</h1>
    <div class="container">
    <form>
            <input type="text" name="name" v-model="restaurant.name" placeholder="Enter Name Here"/>
            <input type="text" name="contact" v-model="restaurant.contact" placeholder="Enter Contact Here"/>
            <input type="text" name="address" v-model="restaurant.address" placeholder="Enter Address Here"/>
            <button type="button" v-on:click="updateRestaurant">Update Restaurant</button>
    </form>
    </div>
</template>
<script>
import Header from './Header.vue'
import axios from 'axios'
export default {
    name:'Update',
    components: {
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
        async updateRestaurant()
        {
            //console.log(this.restaurant);
            const result = await axios.put("http://localhost:3000/restaurant/"+this.$route.params.id,{
              name:this.restaurant.name,
              contact: this.restaurant.contact,
              address: this.restaurant.address  
            });
            //console.log(result);
            if(result.status==200)
            {
                this.$router.push({name:'Home'});
            }
        }
    },
    async mounted()
    {
        let user = localStorage.getItem('user-info');
        if(!user)
        {
            this.$router.push({name:'SignUp'})
        }
        //console.warn(this.$route.params.id)
        const result = await axios.get('http://localhost:3000/restaurant/'+this.$route.params.id);
        this.restaurant=result.data
    }
}
</script>
