<template>
  <nav class="navbar navbar-dark sticky-top bg-dark flex-md-nowrap p-0">
    <router-link class="navbar-brand col-sm-3 col-md-2 mr-0" to="/"
      >ООО Рога и копыта</router-link
    >
    <input
      class="form-control form-control-dark w-100 m-1 p-1"
      type="text"
      placeholder="Поиск"
      aria-label="Поиск"
    />
    <ul class="navbar-nav px-3">
      <li class="nav-item text-nowrap">
        <a class="nav-link" href="#">Войти</a>
      </li>
    </ul>
  </nav>
  <router-view />
</template>

<style lang="less"></style>
