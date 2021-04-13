<template>
  <Layout>
    <div class='say-content'>
      <h1>添加</h1>
      <h3>请添加您想要的英雄</h3>
      <div class='say-form'>
        <div class='form-item'>
          <h4>英雄昵称</h4>
          <input type="text" v-model="from.nickname">
          <p class='form-verify' v-show="verify(from.nickname)">请填写英雄昵称</p>
        </div>
        <div class='form-item'>
          <h4>英雄名称</h4>
          <input type="text" v-model="from.name">
          <p class='form-verify' v-show="verify(from.name)">请填写英雄名称</p>
        </div>
        <div class='form-item'>
          <h4>英雄类型</h4>
          <input type="text" v-model="from.type">
          <p class='form-verify' v-show="verify(from.type)">请填写英雄类型</p>
        </div>
      </div>
      <h4>英雄背景</h4>
      <textarea cols="30" rows="10" v-model="from.content"></textarea>
      <p class='form-verify' v-show="verify(from.content)">请填写英雄背景</p>
      <div class='btn' @click="submit">提交</div>
    </div>
  </Layout>
</template>

<script>
import axios from 'axios'
export default {
  name: 'About',
  metaInfo: {
    title: 'About'
  },
  data () {
    return {
      from: {
        nickname: '',
        name: '',
        type: '',
        content: '',
      }
    }
  },
  methods: {
    submit () {
      if (this.verify(this.from)) return
      axios({
        method: 'POST',
        url: this.imageUrl + '/contacts',
        data: this.from
      }).then(res => {
        console.log(res)
      })
    },
    verify (data) {
      let falg = false
      if (data instanceof Object) {
        for (let i in data) {
          if (data[i] === '') {
            falg = true
            break
          }
        }
      } else {
        falg = data === ''
      }
      return falg
    }
  }
}
</script>

<style>
.say-content {
  padding: 100px 300px;
}
.say-form {
  margin-top: 50px;
  display: flex;
}
.form-item {
  margin-right: 40px;
}
input {
  width: 200px;
  height: 30px;
}
.form-verify{
  color: red;
  margin: 5px 0 0 0;
}
textarea {
  width: 700px;
  height: 300px;
  padding: 10px;
  font-size: 20px;
}
.btn {
  margin-top: 50px;
  width: 100px;
  height: 30px;
  border-radius: 5px;
  line-height: 30px;
  background: cadetblue;
  color: #fff;
  text-align: center;
  cursor: pointer;
}
</style>