<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <button @click="fetchData" type="button">New Joke</button>
    <input v-model="firstName">
    <input v-model="lastName">
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data: function () {
    return {
      msg: 'Joke Loading...',
      firstName: 'Todd',
      lastName: 'Eidson'
    }
  },
  created () {
    this.fetchData()
  },
  methods: {
    fetchData: function () {
      fetch('https://api.chucknorris.io/jokes/random')
      .then((response) => {
        console.log(response)
        return response.text()
      })
      .then((data) => {
        console.log(data)
        this.msg = JSON.parse(data)['value']
          .replace(/chuck/gi, this.firstName)
          .replace(/norris/gi, this.lastName)
      })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
