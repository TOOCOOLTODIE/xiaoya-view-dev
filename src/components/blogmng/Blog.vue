<template>
  <div>
    {{ msg }}
    <tinymce-editor v-model="msg"
                    :disabled="disabled"
                    @onClick="onClick"
                    ref="editor"></tinymce-editor>
    <button @click="clear">清空内容</button>
    <button @click="disabled = true">禁用</button>
  </div>
</template>

<script>
  import TinymceEditor from './EditBlog'
  export default {
    components: {
      TinymceEditor
    },
    data() {
      return {
        msg: 'Welcome to Use Tinymce Editor',
        disabled: false
      }
    },
    methods: {
      //鼠标单击的事件
      onClick(e, editor) {
    
      },
      //清空内容
      clear() {
        this.$refs.editor.clear()
      }
    }
  }
</script>

<style scoped>
</style>
