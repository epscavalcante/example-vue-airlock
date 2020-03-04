<template>
  <b-card header-bg-variant="transparent" header-border-variant="light" class="border-0 w-100">
    <template v-slot:header>
      <div class="text-center">
        <img src="https://laravel.com/assets/img/components/logo-airlock.svg" class=""/>
      </div>
    </template>
    
    <router-view />
  </b-card>
</template>

<style>
html,
body {
  height: 100%;
  width: 600px;
  max-height: 500px;
  background-color: #f5f5f5;
  display: flex;
  -ms-flex-align: center;
  align-items: center;
  justify-content: center;
  padding: 40px;
  margin: auto;
  display: -ms-flexbox;
  display: flex;
  -ms-flex-align: center;
  align-items: center;
  justify-content: center;
  background-color: #f5f5f5;
  border-radius: 35px;
}
</style>
