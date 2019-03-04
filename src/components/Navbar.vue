<template>
  <nav class="navbar navbar-dark bg-dark navbar-expand-lg">
    <router-link
      to="/dashboard"
      class="navbar-brand"
    >Fleet Management</router-link>
    <button
      class="navbar-toggler"
      type="button"
      data-toggle="collapse"
      data-target="#navbarSupportedContent"
      aria-controls="navbarSupportedContent"
      aria-expanded="false"
      aria-label="Toggle navigation"
    >
      <span class="navbar-toggler-icon"></span>
    </button>

    <div
      class="collapse navbar-collapse"
      id="navbarSupportedContent"
    >
      <ul class="navbar-nav ml-auto">
        <li class="nav-item">
          <a
            class="nav-link"
            href="#"
          >Home</a>
        </li>
        <li class="nav-item">
          <a
            class="nav-link"
            href="#"
          >Fleets</a>
        </li>
        <li class="nav-item">
          <a
            class="nav-link"
            href="#"
          >Log out</a>
        </li>
      </ul>
    </div>
  </nav>
</template>
