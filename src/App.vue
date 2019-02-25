<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/login">login</router-link>
    </div>
    <router-view/>
  </div>
</template>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
  #nav {
    width: 100%;
    margin : 0;
    padding: 3em;
    background: #373a4d;

    font-size: 2rem;
    font-weight: bold;
    list-style: none;
    
  }
  a{
    text-decoration: none;
    color: #fff;
  }
  a:focus{
    color: #fff;
  }
</style>
