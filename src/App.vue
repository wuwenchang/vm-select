<template>
  <div id="app">
    <div ></div>
    <vm-select :options="options" search label="name" labelKey="id" multiple v-model="selected"></vm-select>
  </div>
</template>
<script>
import vmSelect from './components/vm-select/'
export default {
  data () {
    return {
      options: [
        { id: '1', name: 'Atari 2600' },
        { id: '2', name: 'Atari 5200', age: 18 },
        { id: '3', name: 'Nintendo 2600安师大撒啊SD手机啊是哦哦睡啦哦哦撒u没撒事' },
        { id: '4', name: 'Nintendo 5200', age: 17 },
        { id: '5', name: 'GameBoy 2600', age: 20 },
        { id: '6', name: 'GameBoy 5200' },
        { id: '7', name: 'WiiU 2600' },
        { id: '8', name: 'WiiU 3600' },
        { id: '9', name: 'WiiU 4600' }
      ],
      selected: ['3', '4', '5']
    }
  },
  components: {
    vmSelect
  }
}
</script>
<style lang="less">
body {
  margin: 0;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  max-width: 1000px;
  margin: 0 auto;
}
#nav {
  padding: 30px;
  a {
    font-weight: bold;
    color: #2c3e50;
    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
