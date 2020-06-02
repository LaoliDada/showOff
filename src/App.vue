<template>
  <div id="app">
    <div class='wrapper'>
      <div class="toolbar">
        <input class="color-tool" type="color" v-model="bgcolor">
        <button class='create-pic-btn' @click="createPic">生成图片</button>
      </div>
      <div id="bg-wrapper" class="bg-wrapper" :style="{backgroundColor:bgcolor}">
        <div class="content-wrapper">
          <div class="header cm-s-monokai CodeMirror">
            <div class='menu-btn'></div>
            <div class='menu-btn'></div>
            <div class='menu-btn'></div>
          </div>
          <textarea :value="textVal" class="form-control" id="editor" name="code"></textarea>
        </div>
      </div>
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
  data(){
      return {
        bgcolor:"#ABB8C3",
        textVal:`const pluckDeep = key => obj => key.split('.').reduce((accum, key) => accum[key], obj)

              const compose = (...fns) => res => fns.reduce((accum, next) => next(accum), res)

              const unfold = (f, seed) => {
                const go = (f, seed, acc) => {
                  const res = f(seed)
                  return res ? go(f, res[1], acc.concat([res[0]])) : acc
                }
                return go(f, seed, [])
              }`
      }
    },
    methods:{
      createPic(){
        let canvas = document.createElement("canvas");
        let img = document.createElement("img");
        let ctx = canvas.getContext("2d");
        let bgWrapper = document.getElementById('bg-wrapper');
        canvas.width = bgWrapper.clientWidth;
        canvas.height = bgWrapper.clientHeight;
        ctx.drawImage(bgWrapper, 0, 0, canvas.width, canvas.height);
        img.src = canvas.toDataURL();
        document.body.append(img);
      }
    },
  mounted(){
    let myTextarea = document.getElementById('editor');
    this.CodeMirrorEditor = CodeMirror.fromTextArea(myTextarea, {
      mode:'javascript',//编辑器语言
      theme:'monokai', //编辑器主题
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
body,html{
  width:100;
  background:#121212;
}
*{
  margin:0;
  padding:0;
  font-family:"微软雅黑";
}
.toolbar{
  padding-bottom:10px;
}
.create-pic-btn{
  border:1px solid #ccc;
  height:30px;
  width:100px;
  vertical-align: text-bottom;
  margin-left: 20px;
  cursor:pointer;
}
.wrapper{
  width:900px;
  border: 3px solid #fff;
  border-radius: 8px;
  padding: 16px;
  margin:30px auto;
}
.color-tool{
  border:1px solid #ccc;
  width:30px;
  height:30px;
}
.content-wrapper{
  width:800px;
  border-radius:10px;
  margin:20px auto;
  box-shadow: rgba(0, 0, 0, 0.55) 0px 20px 68px;
}
.bg-wrapper{
  padding:20px 0;
}
.menu-btn{
  width:14px;
  height:14px;
  border-radius:7px;
  margin-right:10px;
  display:inline-block;
}
.header.CodeMirror{
    border: none;
    border-radius: 10px 10px 0 0;
    font-size: 15px;
    height:24px;
    width:800px;
    box-sizing: border-box;
    padding:5px 10px 0px;
}
.menu-btn:first-of-type{
  background:rgb(255, 95, 86);
}
.menu-btn:nth-of-type(2){
  background:rgb(255, 189, 46);
}
.menu-btn:last-of-type{
  background:rgb(39, 201, 63);
}
.CodeMirror{
  border:1px solid black;
  border-top:0px;
  border-radius:0 0px 10px 10px;
  font-size:15px;
  width:800px;
  padding:10px;
  padding-bottom:40px;
}
</style>
