<template>
  <nav class="navbar navbar-dark sticky-top bg-dark flex-md-nowrap p-0">
    <router-link class="navbar-brand col-sm-3 col-md-2 mr-0" to="/"
      >ООО таблицы и пересчет</router-link
    >

    <ul class="navbar-nav px-3">
      <li class="nav-item text-nowrap">
        <router-link class="nav-link" to="/login">Войти</router-link>
      </li>
    </ul>
  </nav>
  <div class="container-fluid">
    <div class="row">
      <nav class="col-md-2 d-none d-md-block bg-light sidebar">
        <div class="sidebar-sticky">
          <ul class="nav flex-column">
            <li class="nav-item">
              <router-link class="nav-link active" to="/">
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  width="24"
                  height="24"
                  viewBox="0 0 24 24"
                  fill="none"
                  stroke="currentColor"
                  stroke-width="2"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  class="feather feather-home"
                >
                  <path
                    d="M3 9l9-7 9 7v11a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2z"
                  ></path>
                  <polyline points="9 22 9 12 15 12 15 22"></polyline>
                </svg>
                Интерактивная таблица <span class="sr-only"></span>
              </router-link>
            </li>
          </ul>
          <!--  -->
        </div>
      </nav>
      <router-view />
    </div>
  </div>
</template>

<style lang="less"></style>
