<template>
  <layout>
    <x-nav slot="header" back="/">
      <div slot="title">Qrcode</div>
    </x-nav>
    <x-body slot="body" v-if="pageState.into">
      <div class="qrcode-demo">
        <qrcode text="http://vue.bittyos.com/"/>
      </div>
    </x-body>
  </layout>
</template>
<script>
import { children } from 'utils/mixins/page'
export default {
  mixins: [children]
}
</script>
<style lang="scss">
  .qrcode-demo{
    text-align:center;
    padding:1rem;
  }
</style>
