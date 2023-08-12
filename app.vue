
<template>
      <div>
        <button @click="externalServiceAuth('auth-yandex')">Войти через yandex</button>
        <br /><br />
        <button @click="externalServiceAuth('auth-google')">Войти через google</button>
      </div>
</template>

<script setup>
import {useFetch} from '@vueuse/core'
function externalServiceAuth(service) {
  console.log(service);
  const url = 'http://authapi.biz/api/' + service;
  // //получение ссылки авторизации с back-end приложения и переход по ней
  postData(url).then((yandexAuthUrl) => {
        console.log(yandexAuthUrl);
        location.href = yandexAuthUrl;
  });
}

const postData = async (url = '', data = {}) => {
  const response = await fetch(url, {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json'
    },
    body: JSON.stringify(data)
  });
  return response.json();
}
</script>