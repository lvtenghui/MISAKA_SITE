<template>
    <HelloWorld :dataList="pageData"/>
</template>
  
  <script>
  import HelloWorld from './HelloWorld.vue'
  
        export default {
        name: 'testPage',
        components: {
            HelloWorld
        },
        data () {
            return {
            pageData: [{
                name: '页面1',
                    id: 1,
                    style: '#55efc4'
                }, {
                    name: '页面2',
                    id: 2,
                    style: '#fab1a0'
                }, {
                    name: '页面3',
                    id: 3,
                    style: '#fdcb6e'
                }, {
                    name: '页面4',
                    id: 4,
                    style: '#0984e3'
                }]
                }
            }
        }
  </script>
  
  <style>
 *{
    margin: 0;
    padding: 0;
  }
  html,body{font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  }
</style>