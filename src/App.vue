<template>
  <div id="app">
    <div class="wrapper">

      <textarea value="" class="form-control" id="editor" name="code"></textarea>
    </div>
  </div>
</template>

<script>
import * as CodeMirror from 'codemirror/lib/codemirror'
import 'codemirror/theme/monokai.css'
import 'codemirror/theme/night.css'
import 'codemirror/lib/codemirror.css'
import 'codemirror/mode/javascript/javascript'
import 'codemirror/mode/clike/clike'
import 'codemirror/mode/go/go'
import 'codemirror/mode/htmlmixed/htmlmixed'
import 'codemirror/mode/http/http'
import 'codemirror/mode/php/php'
import 'codemirror/mode/python/python'
import 'codemirror/mode/http/http'
import 'codemirror/mode/sql/sql'
import 'codemirror/mode/vue/vue'
import 'codemirror/mode/xml/xml'
import 'codemirror/addon/scroll/simplescrollbars.css'
import 'codemirror/addon/scroll/simplescrollbars'
import 'codemirror/addon/selection/active-line'
export default {
  name: 'App',
  mounted(){
    let myTextarea = document.getElementById('editor');
    this.CodeMirrorEditor = CodeMirror.fromTextArea(myTextarea, {
      mode:'javascript',//编辑器语言
      theme:'night', //编辑器主题
      extraKeys: {"Ctrl": "autocomplete"},//ctrl可以弹出选择项 
      lineNumbers: false,//显示行号
      smartIndent:true,//自动缩进
      scrollbarStyle:null,//是否展示滚动条
      lineWrapping: false
    });
    this.CodeMirrorEditor.setSize('auto','auto');
  }
}
</script>

<style>
*{
  margin:0;
  padding:0;
  font-family:"微软雅黑";
}
.wrapper{
  width:600px;
  min-height:500px;
  border-radius:10px;
  margin:20px auto;
}
.CodeMirror{
  border:1px solid black;
  border-radius:10px;
  font-size:15px;
  width:600px;
  padding:20px;
}
</style>
