<template>
  <div class="">
    <app-header></app-header>
<<<<<<< HEAD
    <div class="complete-detail">
        <div class="complete-detail-title">深圳公交失物招领系统上线</div>
        <div class="commenter--item">
          <div class="commenter--item-left">
            <div>编码: 20170407</div>
            <div>类型:  跟帖</div>
            <div>任务描述: 直升机飞行千里救援患病老人</div>
          </div>
          <div class="commenter--item-right">
            <div>发布人: 超管1</div>
            <div>发布时间：2017-04-05 09：30</div>
            <div>结束时间：2017-04-10 09：30</div>
          </div>
        </div>
        <textarea class="complete-detail-text"></textarea>
        <div class="complete-detail-pic">
          <div class="">pic1</div>
          <div class="">pic2</div>
          <div class="">pic3</div>
        </div>
    </div>
=======
    <div v-show="showloading" class="showloading"><span class="el-icon-loading" ></span>数据加载中</div>
    <div class="taskdown--nodata" v-show="nodata">暂无数据</div>
    <div class="complete-detail">
        <div class="complete-detail-title">任务详情</div>
        <div class="commenter--item">
          <div class="commenter--item-left">
            <div>发布人: {{taskerdetailarr.sendusername}}</div>
            <div>类型:  {{taskerdetailarr.typeName}}</div>
            <div>事件分类: {{taskerdetailarr.eventtypename}}</div>
            <div>任务描述: {{taskerdetailarr.remarks}}</div>
            <div class="">网址:<a :href="taskerdetailarr.url">{{taskerdetailarr.url}}</a></div>
          </div>
          <div class="commenter--item-right">
            <div>发布时间：{{taskerdetailarr.senddate}}</div>
            <div>结束时间：{{taskerdetailarr.enddate}}</div>
            <div>接收人员：{{taskerdetailarr.receivename}}</div>
          </div>
        </div>
    </div>
    <div class="complete-detail">
        <div class="complete-detail-title">执行任务展示列表</div>
        <div class="" v-show="nodatalist">暂无数据</div>
        <div class="commenter--item-warp">
          <div class="commenter--item" v-for="(i, value) in issueDetailArr">
            <div class="commenter--item-left">
              <div>序号: {{i.id}}</div>
              <div>操作账号:  {{i.login_name}}</div>
              <div>发帖标题: {{i.title}}</div>
              <div>发帖内容: {{i.content}}</div>
              <div>失败原因: {{i.error_msg}}</div>
            </div>
            <div class="commenter--item-right">
              <div>执行状态: {{i.status}}</div>
              <div>执行时间: {{i.excute_time}}</div>
              <div class="commenter--item-right-pic">
                <span v-if="i.pic === '无'">暂无图片</span>
                <img v-else :src="i.pic" alt="" @click="showPic(i.pic)">
              </div>
            </div>
          </div>
        </div>
    </div>
    <el-dialog title="图片放大提示" v-model="dialogVisible.show" size="tiny" id="showpic">
      <img :src="dialogVisible.src" alt="">
      <span slot="footer" class="dialog-footer">
        <el-button type="primary" @click="dialogVisible.show = false">确 定</el-button>
      </span>
    </el-dialog>
>>>>>>> fe67524103ffe3546281d2a8dd81bc4e27082d3f
  </div>
</template>

<script>
<<<<<<< HEAD
=======
import Vue from 'vue'
import { mapActions, mapState } from 'vuex'
import { USER_INFO } from '../../../store/storex'
>>>>>>> fe67524103ffe3546281d2a8dd81bc4e27082d3f
import appHeader from '../../common/header.vue'
export default {
  name: 'completedetail',
  data () {
    return {
<<<<<<< HEAD
      msg: 'completedetail here'
=======
      msg: 'completedetail here',
      showloading: false,
      nodatalist: false,
      nodata: false,
      dialogVisible: {
        show: false,
        src: ''
      },
      taskerdetailarr: {},
      issueDetailArr: [],
      pager: 1
>>>>>>> fe67524103ffe3546281d2a8dd81bc4e27082d3f
    }
  },
  components: {
    appHeader: appHeader
  },
<<<<<<< HEAD
  methods: {
    linkToPath (path) {
      this.$router.push({path: path})
    }
=======
  computed: mapState({
    user: state => state.user
  }),
  methods: {
    ...mapActions([USER_INFO]),
    linkToPath (path) {
      this.$router.push({path: path})
    },
    getTaskerDetail () {
      this.showloading = true
      Vue.http.options.emulateJSON = true
      if (this.$store.state.user) {
        let prefix = this.$store.state.user.CHECKED_STATUS
        let taskuserid = this.$route.query.taskuserid || ''
        let detailPageTaskUserIndexUrl = prefix + '/bms/taskUser/detailPageTaskUserIndex.action'
        this.$http.post(detailPageTaskUserIndexUrl, {taskuserid: taskuserid}).then((response) => {
          let resdata = response.body
          let states = ''
          if (resdata === '' || resdata === null || resdata === undefined) {
            this.nodata = true
            return
          }
          if (resdata.state === 1) {
            states = '未完成'
          } else if (resdata.state === 2) {
            states = '已经完成'
          } else {
            states = '超时完成'
          }
          this.taskerdetailarr.states = states
          this.taskerdetailarr.sendusername = resdata.sendusername
          this.taskerdetailarr.typeName = resdata.typeName
          this.taskerdetailarr.senddate = resdata.senddate
          this.taskerdetailarr.enddate = resdata.enddate
          this.taskerdetailarr.eventtypename = resdata.eventtypename
          this.taskerdetailarr.remarks = resdata.remarks
          this.taskerdetailarr.receivename = resdata.receivename
          this.taskerdetailarr.url = resdata.url
          this.showloading = false
        }, (response) => {
          this.$alert('网络异常!')
          this.showloading = false
        })
      }
    },
    getIssueDetail (page, rows) {
      let issueDetail = {
        page: page,
        rows: rows,
        taskuserid: ''
      }
      this.showloading = true
      Vue.http.options.emulateJSON = true
      if (this.$store.state.user) {
        let prefix = this.$store.state.user.CHECKED_STATUS
        issueDetail.taskuserid = this.$route.query.taskuserid || ''
        let queryIssueDetailsUrl = prefix + '/bms/taskUserSend/queryIssueDetails.action'
        this.$http.post(queryIssueDetailsUrl, issueDetail).then((response) => {
          console.log(response)
          let resdata = response.body.rows
          let reslen = resdata.length
          let status = ''
          let pic_ = ''
          if (reslen === 0 && page === 1) {
            this.$alert('暂无数据')
            this.nodatalist = true
          } else if (reslen === 0 && page > 1) {
            this.$alert('已显示所有数据')
            this.pager--
            this.showloading = false
            return
          }
          for (let i = 0; i < reslen; i++) {
            if (resdata[i].excute_status === 0) {
              status = '提交中'
            } else if (resdata[i].excute_status === 1) {
              status = '进行中'
            } else if (resdata[i].excute_status === 2) {
              status = '成功'
            } else {
              status = '失败'
            }
            if (resdata[i].pic === '' || resdata[i].pic === null || resdata[i].pic === undefined) {
              pic_ = '无'
            } else {
              pic_ = 'data:image/jpeg;base64,' + resdata[i].pic
            }
            this.issueDetailArr.push({
              id: resdata[i].id,
              login_name: resdata[i].login_name,
              excute_status: status,
              pic: pic_,
              excute_time: resdata[i].excute_time,
              title: resdata[i].title,
              content: resdata[i].content,
              error_msg: resdata[i].error_msg
            })
          }
          this.showloading = false
        }, (response) => {
          this.$alert('网络异常!')
          this.showloading = false
        })
      }
    },
    showPic (src) {
      this.dialogVisible.src = src
      this.dialogVisible.show = true
    }
  },
  created () {
    this.getTaskerDetail()
    this.getIssueDetail(1, 15)
  },
  mounted () {
    let tbodyWrapperEl = document.querySelector('.commenter--item-warp')
    let getTbodyScrollToBottom = () => {
      // let tbodyEl = tbodyWrapperEl.lastElementChild
      // let lastTr = [].slice.call(tbodyEl.querySelectorAll('tr'), 0).slice(-1)[0]
      let result = false
      if (tbodyWrapperEl.clientHeight + tbodyWrapperEl.scrollTop >= tbodyWrapperEl.scrollHeight) {
        result = true
      }
      return result
    }
    tbodyWrapperEl.addEventListener('scroll', (event) => {
      if (getTbodyScrollToBottom()) {
        this.pager++
        this.getIssueDetail(this.pager, 15)
      }
    })
>>>>>>> fe67524103ffe3546281d2a8dd81bc4e27082d3f
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style rel="stylesheet/scss" lang="scss" scoped>
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
<<<<<<< HEAD
=======
#showpic .el-dialog--tiny{
  width: 100%;
}
.task--detail-header{
  height: 2.6rem;
  padding: 0 0.8rem;
  background-color: #20a0ff;
  .title--news{
    display: flex;
    justify-content: space-between;
    align-items: center;
    line-height: 2.6rem;
  }
}
>>>>>>> fe67524103ffe3546281d2a8dd81bc4e27082d3f
.complete-detail{
  padding: 0 0.8rem;
  &-title{
    text-align: left;
<<<<<<< HEAD
    margin: 1rem 0;
  }
  &-text{
    margin-top: 1rem;
    width: 100%;
    height: 20rem;
    overflow-y: scroll;
=======
    margin: 0.5rem 0;
>>>>>>> fe67524103ffe3546281d2a8dd81bc4e27082d3f
  }
  &-pic{
    display: flex;
    justify-content: space-around;
    margin-top: 1rem;
<<<<<<< HEAD
=======
    text-overflow: ellipsis;
    overflow: hidden;
    white-space: nowrap;
    width: 100%;
  }
  .commenter--item-warp{
    max-height: 24rem;
    overflow-y: scroll;
>>>>>>> fe67524103ffe3546281d2a8dd81bc4e27082d3f
  }
}
.commenter--item{
  display: flex;
  justify-content: space-between;
  padding: 0.5rem 1rem;
<<<<<<< HEAD
  border: 1px dashed #13CE66;
    &-left,&-right{
      display: flex;
      flex-direction: column;
      div{
        width: 10rem;
=======
  border: 1px dashed #eee;
    &-left,&-right{
      display: flex;
      flex-direction: column;
      width: 50%;
      div,a{
>>>>>>> fe67524103ffe3546281d2a8dd81bc4e27082d3f
        text-align: left;
        white-space: nowrap;
        text-overflow:ellipsis;
         overflow:hidden;
      }
    }
    &-right{
<<<<<<< HEAD
=======
      padding-left: 0.2rem;
      &-pic{
        padding-top: 0.2rem;
        height: 3rem;
        width: 100%;
        img{
          width: 100%;
          height: 100%;
        }
      }
>>>>>>> fe67524103ffe3546281d2a8dd81bc4e27082d3f
      .btn-detail{
        margin-top: 0.5rem;
        width: 6rem;
        float: right;
      }
    }
}
</style>
