<template>
  <div id="app">
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <a class="navbar-brand">TodoList VueJS and TypeScript</a>
      <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarNavAltMarkup" aria-controls="navbarNavAltMarkup" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarNavAltMarkup">
        <div class="navbar-nav">
          <router-link class="nav-item nav-link" style="font-weight: bold" to="/">Home</router-link>
          <router-link class="nav-item nav-link" style="font-weight: bold" to="/about">Authors</router-link>
        </div>
      </div>
    </nav>
    <router-view/>
  </div>
</template>

