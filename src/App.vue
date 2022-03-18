<template>
  <nav>
    <router-link to="/">جميع الاسهم</router-link> |
    <router-link to="/addStock">اضافة سهم</router-link>
  </nav>
  <router-view />
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Cairo:wght@200;300;400;500;600;700;800;900&display=swap');
*{
  padding: 0;
  margin: 0;
  box-sizing: border-box;
  font-family: 'Cairo', sans-serif;
  
}



nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
  text-decoration: none;
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>
