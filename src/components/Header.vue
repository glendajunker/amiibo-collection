<template>
  <header class="navbar">
    <a href="/" class="logo-amiibo"
      ><img src="../assets/logo-amiibo.png" alt="amiibo logo"
    /></a>
    <nav>
      <ul>
        <li><router-link to="/character-lineup">Lineup</router-link></li>
        <li><router-link to="/browse-games">Games</router-link></li>
        <li><router-link to="/browse-series">Series</router-link></li>
      </ul>
    </nav>
    <!-- <form id="navbar-search">
             <input type="text" placeholder="Search character, series, game...">
         </form> -->
  </header>
</template>

<script>
export default {};
</script>

<style scoped>
.navbar {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  align-items: center;
  padding: 1em 2em;
}

.logo-amiibo {
  flex-grow: 1;
  flex-basis: 0;
}

.logo-amiibo img {
  width: 150px;
}

nav {
  flex-grow: 1;
  flex-basis: 0;
  text-align: center;
}

ul {
  display: flex;
  justify-content: space-evenly;
  list-style-type: none;
  padding: 0;
}

li {
  float: left;
  font-size: 0.9em;
  font-weight: 600;
  color: #000;
  padding: 0 1em;
}

#navbar-search {
  flex-grow: 1;
  flex-basis: 0;
  text-align: right;
}

#navbar-search input {
  padding: 0.5em 1.5em;
  border-radius: 30px;
  border: 1px solid #848484;
  box-sizing: border-box;
  max-width: 250px;
  width: 80%;
}

#navbar-search input:focus {
  border: 1px solid #000;
  outline: none;
}

#navbar-search input:hover {
  border: 1px solid #000;
}

@media only screen and (max-width: 600px) {
  .navbar {
    flex-direction: column;
  }
  #navbar-search {
    text-align: center;
  }
}
</style>
