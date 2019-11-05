<template>
  <div id="app">
    <input type="number" align='middle' v-model="limit" value=this.limit  />
    <Numbers @clicked="pick"/>
  </div>
</template>

<script>
import Numbers from '@/components/Numbers';

export default {
  name: 'App',
  components: {Numbers},
  data()
  {
    return {
      limit: 100
    }
  },
  // recieves new limit if triggered by click in child element
  methods: {
    pick(value) {
      this.limit = value
    }
  }
}
</script>

<style scoped>

#app{
  background: rgb(2,0,36);
background: linear-gradient(90deg, rgba(2,0,36,1) 0%,     rgba(9,121,76,1.16150210084033612) 35%, rgba(0,212,255,1) 100%);
  display: inline-block;
  width: 100%;
  height: 100%;

}

input{
  display: flex;
  margin:auto;
  margin-top:2em;
  margin-bottom: 2em;
  padding: 1em;
  text-align: center;
  border-radius: 50%;
  font-size: 2em;
  font-family: "Helvetica Neue";
  border: 2px  solid white;
  background-color: rgba(0,0,0,0);
  color: white;

}
</style>
