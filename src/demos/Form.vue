<template>
  <layout>
    <x-nav slot="header" back="/">
      <div slot="title">Form</div>
    </x-nav>
    <x-body slot="body">
      <br />
      <x-form :model="form" :submit="submit">
        <x-form-item label="姓名" prop="name" :rules="[
          {required: true, message: '姓名不能为空'},
          {min: 2, message: '姓名不能小于两字符'}
          ]">
          <x-input v-model="form.name" placeholder="请输入姓名"/>
        </x-form-item>
        <x-form-item label="手机号码" prop="mobile" :rules="[
          {required: true, message: '手机号码不能为空'},
          {pattern: /^1[3|4|5|7|8][0-9]{9}$/, message: '手机号码格式不正确'}
          ]">
          <x-input v-model="form.mobile" placeholder="请输入手机号码"/>
        </x-form-item>
        <x-form-item label="邮箱地址" prop="email" :rules="[
          {required: true, message: '邮箱地址不能为空'},
          {pattern: /[\w!#$%&'*+/=?^_`{|}~-]+(?:\.[\w!#$%&'*+/=?^_`{|}~-]+)*@(?:[\w](?:[\w-]*[\w])?\.)+[\w](?:[\w-]*[\w])?/, message: '邮箱地址格式不正确'}
          ]">
          <x-input v-model="form.email" placeholder="请输入邮箱地址"/>
        </x-form-item>
        <x-form-item label="兴趣爱好">
          <x-select v-model="form.hobby">
            <x-option value="1">篮球</x-option>
            <x-option value="2">足球</x-option>
            <x-option value="3">羽毛球</x-option>
          </x-select>
        </x-form-item>
        <x-form-item label="开启消息醒">
          <x-switch v-model="form.enable"/>
        </x-form-item>
        <div style="padding:20px 10px;">
          <x-button type="primary" native-type="submit" size="large">保存</x-button>
        </div>
      </x-form>
    </x-body>
  </layout>
</template>

<script>
import { children } from 'utils/mixins/page'
export default {
  mixins: [children],
  methods: {
    submit () {
      this.$toast({
        type: 'loading',
        content: '数据中...',
        onClose: () => {
          this.$toast({
            type: 'success',
            content: '数据提交成功！'
          })
        }
      })
    }
  },
  data () {
    return {
      form: {
        name: '',
        mobile: '',
        email: '',
        hobby: '',
        enable: false
      }
    }
  }
}
</script>

<style lang="scss">

</style>
