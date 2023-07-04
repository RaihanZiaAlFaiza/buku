<template>
  <div id="app">
    <nav class="navbar navbar-expand-lg">
      <div class="container">
        <router-link to="/" class="navbar-brand">REY BOOK STORE</router-link>
        <ul class="navbar-nav ml-auto">
          <li class="nav-item">
            <router-link to="/" class="nav-link">Home</router-link>
          </li>
          <li class="nav-item">
            <router-link to="/books" class="nav-link">Book Store</router-link>
          </li>
          <li class="nav-item">
            <router-link to="/categories" class="nav-link">kategori</router-link>
          </li>
          <li class="nav-item">
            <router-link to="/Member" class="nav-link">Member</router-link>
          </li>
          <li class="nav-item">
            <router-link to="/Desc" class="nav-link">informasi</router-link>
          </li>
        </ul>
      </div>
    </nav>
    <div class="container mt-4">
      <router-view></router-view>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
};
</script>

<style>
#app {
  font-family: Arial, Helvetica, sans-serif;
}

.navbar-expand-lg {
  background-color: #8fb5bc;
}
.navbar-brand {
  padding: 5px 10px;
  text-decoration: none;
  color: white;
  font-family: "Times New Roman";
  font-size: large;
}
.nav-item {
  display: flex;
  align-items: center;
  border: 1px solid #fff0f0;
  border-radius: 20px;
  list-style: none;
  margin-left: 20px;
  align-items: center;
  text-decoration: none;
  float: left;
  color: white;
  font-weight: 500;
}
.navbar-nav {
  text-align: center;
  padding: 10px;
}
.navbar-nav li:hover {
  color: #06060b;
  font-size: 20px;
  transition: 0.2s;
  background-color: rgb(212, 195, 195);
}
</style>
