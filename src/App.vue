<template>
  <header>
    <div class="navbar bg-base-200">
      <div class="flex-1">
        <a class="btn btn-ghost normal-case text-xl">Krushn's Devtools</a>
      </div>
      <div class="flex-none">
        <ul class="menu menu-horizontal px-1">
          <li>
            <router-link to="/">Home</router-link>
          </li>
          <li>
            <router-link to="/gradients">Gradients</router-link>
          </li>
          <li>
            <router-link to="/about">About</router-link>
          </li>
        </ul>
      </div>
    </div>
  </header>

  <main>
    <router-view />
  </main>
</template>
