<template>
  <div class="hello">
    <h1>Login</h1>
    <h2>{{ msg }}</h2>

    <form>
      <input v-model="username" placeholder="username or email">
      <p>User: {{ username }}</p>
      <br/>
      <input v-model="password" type="password" placeholder="your password">
      <p>Password: {{ password }}</p>

      <button v-on:click="loginJwt">JWT 登录</button>
    </form>
    <ul>
      <li><router-link :to="{ name: 'Home', params: { id: 'fromloginpanel' }}" >跳转到Foo(普通链接的例子）</router-link></li>
      <li v-on:click="gotoFoo">跳转到Foo(Javascript 跳转的例子)</li>
      <li v-on:click="gotoFooAfter2Seconds">跳转到Foo(显示Loading)</li>
      <li v-on:click="showMessage">显示Toast Message</li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'Login',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      username: 'admin',
      password: 'admpwd'
    }
  },
  created () {
    // 组件加载完毕会调用此函数
    console.log('created called')
    // CommonUtil.setTitle('首页')
    // this.$store.commit('setShowBottomMenu', true) // 显示底部菜单
    // this.$store.commit('setTab', 'home') // 设置底部高亮菜单为setting
  },
  methods: {
    loginJwt () {
      let vm = this
      this.$auth.login(this.$data.username, this.$data.password, function (response) {
        vm.$router.push({name: 'Home', params: { from: 'login' }})
      }, function (response) {
        vm.$data.msg = (response.status + ' --- ' + response.body + '---' + response.text())
      })
    },
    gotoFoo () {
      // JavaScript跳转到foo页面，并传递参数id=457；除了router.push外还可以router.replace
      this.$router.push({name: 'foo', params: { id: 457 }})
    },
    gotoHome () {
      this.$router.push({ path: '/' })
    },
    gotoFooAfter2Seconds () {
      // 这是一个显示loading的例子，故意延时了2s，以便看清loading
      // this.$store.commit('setShowLoadding', true) // 显示Loading
      // window.setTimeout(this.gotoFoo, 2000)
    },
    showMessage () {
      // this.$store.commit('showToast', 'Hello world. hello again, Hello, again and again.')
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
