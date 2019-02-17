<template>
  <div class="highlight">
    <div class="pre-code" @click="show = !show">{{show ? '收起源码' : '查看源码'}}&lt;/&gt;</div>
    <pre class="highlight" v-show="show">
      <code>
        <slot></slot>
      </code>
    </pre>
  </div>
</template>
<script>
export default {
  name: 'vCode',
  data () {
    return {
      show: false
    }
  }
}
</script>
