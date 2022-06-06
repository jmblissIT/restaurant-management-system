<template>
    <div>
        <nav class="navbar navbar-expand-lg bg-light">
  <div class="container-fluid">
    <router-link class="navbar-brand" to="/">Restaurant</router-link>
    <div class="collapse navbar-collapse" id="navbarSupportedContent">
      <ul class="navbar-nav me-auto mb-2 mb-lg-0">
        <li class="nav-item">
          <router-link class="nav-link active" to="/add">ADD</router-link>
        </li>
        <li class="nav-item">
          <router-link class="nav-link" to="/update">Update</router-link>
        </li>
        <li class="nav-item">
          <a v-on:click="logout" class="nav-link">Logout</a>
        </li>
      </ul>
    </div>
  </div>
</nav>
    </div>
</template>

<script>
export default {
    name:'Header',
    methods:{
        logout()
        {
            localStorage.clear();
            this.$router.push({name: 'Login'})
        }
    }
}
</script>
