<template>
  <div class="home">
    <el-tabs :tab-position="tabPosition">
      <el-tab-pane>
        <span slot="label"><i class="el-icon-date"></i> 我的行程</span>
        <div class="test">
          <el-upload
            class="upload-demo"
            :on-change="onChange"
            :file-list="fileList">
            <el-button size="small" type="primary">点击上传</el-button>
          </el-upload>
          <div id="container"></div>
        </div>
      </el-tab-pane>
      <el-tab-pane>
        <span slot="label"><i class="el-icon-date"></i> 行程管理</span>
        <hello-world></hello-world>
      </el-tab-pane>
      <el-tab-pane label="角色管理">角色管理</el-tab-pane>
      <el-tab-pane label="定时任务补偿">定时任务补偿</el-tab-pane>
    </el-tabs>
  </div>
</template>

<script>
import HelloWorld from '../components/HelloWorld'
import * as monaco from 'monaco-editor'
// import axios from '../api/network'
export default {
  components: { HelloWorld },
  name: 'Home',
  data () {
    return {
      fileList: [],
      tabPosition: 'left',
      text: '',
      xmlDoc: '',
      editor: null
    }
  },
  mounted () {
    this.parseXml()
    this.initEditor()
  },
  methods: {
    initEditor () {
      // 初始化编辑器，确保dom已经渲染
      this.editor = monaco.editor.create(document.getElementById('container'), {
        value: '111', // 编辑器初始显示文字
        language: 'xml', // 语言支持自行查阅demo
        automaticLayout: true, // 自动布局
        theme: 'vs-dark' // 官方自带三种主题vs, hc-black, or vs-dark
      })
      this.editor.setValue('22222')
    },
    parseXml () {
      // axios.get('../assets/UpgradeRes.xml').then((res) => {
      //   console.log(res)
      // })
    },
    onChange (data) {
      var reader = new FileReader()
      reader.onload = res => {
        this.editor.setValue('3333')
        console.log(res.target.result)
        this.editor.setValue(res.target.result)
      }
      reader.readAsText(data.raw)
    }
  }
}
</script>
<style scoped>
.test{
  width: 100%;
  height: 100%;
  color: #fff;
}
#container{
  height: 800px;
  text-align: left;
}
</style>
