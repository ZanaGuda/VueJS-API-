<template>
  <div id="app">
    <router-link to="/">Home</router-link>
    <router-view/>
  </div>
</template>

<style>
#app {
  padding: 30px;
  padding-top:40px
}


nav a {
  font-weight: bold;
  color: #2c3e50;
 
}
a{
  font-size: 20px;
}

nav a.router-link-exact-active {
  color: #42b983;
}
.router-link-exact-active.router-link-active{
  display: flex;
  justify-content: center;
}
</style>
