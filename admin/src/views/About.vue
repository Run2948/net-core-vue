<template>
    <div class="about">
        <h1>This is an about page</h1>
        <h1>base-api: {{url}}</h1>
    </div>
</template>

<script>export default {
  data () {
    return {
      url: process.env.VUE_APP_BASE_URL + ':' + process.env.VUE_APP_BASE_PORT
    }
  }
}</script>
