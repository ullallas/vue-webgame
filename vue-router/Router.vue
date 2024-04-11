<template>
  <div>
    <div>
      <router-link to="/game/index">Game Matcher</router-link>
      <router-link to="/game/number-baseball">숫자야구</router-link>
      <router-link to="/game/response-check">반응속도체크</router-link>
      <router-link to="/game/rock-scissors-paper">가위바위보</router-link>
      <router-link to="/game/lotto-generator">로또</router-link>

      <!-- <router-link to="/number-baseball">숫자야구</router-link>
      <router-link to="/response-check">반응속도체크</router-link>
      <router-link to="/rock-scissors-paper">가위바위보</router-link>
      <router-link to="/lotto-generator">로또</router-link> -->
    </div>
    <router-view></router-view>
  </div>
</template>

<script>
  import router from './routes';

  export default {
    router,
  };
</script>

<style>
  table {
    border-collapse: collapse;
  }
  td {
    border: 1px solid black;
    width: 40px;
    height: 40px;
    text-align: center;
  }
</style>