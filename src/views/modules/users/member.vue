<template>
  <div class="mod-config">
    <el-form :inline="true" :model="dataForm" @keyup.enter.native="getDataList()">
      <el-form-item>
        <el-input v-model="dataForm.key" placeholder="参数名" clearable></el-input>
      </el-form-item>
      <el-form-item>
        <el-button @click="getDataList()">查询</el-button>
        <el-button type="primary" @click="addOrUpdateHandle()">新增</el-button>
        <el-button type="danger" @click="deleteHandle()" :disabled="dataListSelections.length <= 0">批量删除</el-button>
      </el-form-item>
    </el-form>
    <el-table
      :data="dataList"
      border
      v-loading="dataListLoading"
      @selection-change="selectionChangeHandle"
      style="width: 100%;">
      <el-table-column
        type="selection"
        header-align="center"
        align="center"
        width="50">
      </el-table-column>
      <el-table-column
        width="170"
        prop="id"
        header-align="center"
        align="center"
        label="序号">
      </el-table-column>
      <el-table-column
        prop="nickName"
        header-align="center"
        align="center"
        label="昵称">
      </el-table-column>
      <el-table-column
        prop="memberName"
        header-align="center"
        align="center"
        label="姓名">
      </el-table-column>
      <el-table-column
        prop="age"
        header-align="center"
        align="center"
        label="年龄">
      </el-table-column>
      <el-table-column
       :formatter="formatRole"
        prop="sex"
        header-align="center"
        align="center"
        label="性别">
      </el-table-column>
      <el-table-column
        prop="industry"
        header-align="center"
        align="center"
        label="行业">
      </el-table-column>
      <el-table-column
        :formatter="formatDateAll"
        prop="birthDate"
        header-align="center"
        align="center"
        width="120"
        label="出生日期">
      </el-table-column>
      <el-table-column
        :formatter="formatDate"
        prop="birthday"
        header-align="center"
        align="center"
        label="生日">
      </el-table-column>
      <el-table-column
        prop="birthAddress"
        header-align="center"
        align="center"
        label="出生地址">
      </el-table-column>
      <el-table-column
        prop="address"
        header-align="center"
        align="center"
        label="现住址">
      </el-table-column>
      <el-table-column
        prop="tel"
        header-align="center"
        align="center"
        label="电话">
      </el-table-column>
      <el-table-column
        prop="mobile"
        header-align="center"
        align="center"
        label="座机">
      </el-table-column>
      <el-table-column
        prop="email"
        header-align="center"
        align="center"
        width="110"
        label="邮箱">
      </el-table-column>
      <el-table-column
        prop="weixin"
        header-align="center"
        align="center"
        label="微信">
      </el-table-column>
      <el-table-column
        prop="qq"
        header-align="center"
        align="center"
        label="QQ">
      </el-table-column>
      <el-table-column
        prop="douyin"
        header-align="center"
        align="center"
        label="抖音">
      </el-table-column>
      <el-table-column
        prop="weibo"
        header-align="center"
        align="center"
        label="微博">
      </el-table-column>
      <el-table-column
        prop="hobby"
        header-align="center"
        align="center"
        label="爱好">
      </el-table-column>
      <el-table-column
        prop="description"
        header-align="center"
        align="center"
        label="备注">
      </el-table-column>
      
      <!-- <el-table-column
        prop="createrId"
        header-align="center"
        align="center"
        label="创建人ID">
      </el-table-column>
      <el-table-column
        prop="creater"
        header-align="center"
        align="center"
        label="创建人">
      </el-table-column>
      <el-table-column
        prop="createTime"
        header-align="center"
        align="center"
        label="创建时间">
      </el-table-column>
      <el-table-column
        prop="updaterId"
        header-align="center"
        align="center"
        label="修改人ID">
      </el-table-column>
      <el-table-column
        prop="updater"
        header-align="center"
        align="center"
        label="修改人">
      </el-table-column>
      <el-table-column
        prop="updateTime"
        header-align="center"
        align="center"
        label="修改时间">
      </el-table-column>
      <el-table-column
        prop="showStatus"
        header-align="center"
        align="center"
        label="是否显示[1-显示，0-不显示]">
      </el-table-column>
      <el-table-column
        prop="sort"
        header-align="center"
        align="center"
        label="排序">
      </el-table-column>
      <el-table-column
        prop="firstLetter"
        header-align="center"
        align="center"
        label="检索首字母">
      </el-table-column> -->
      <el-table-column
        fixed="right"
        header-align="center"
        align="center"
        width="150"
        label="操作">
        <template slot-scope="scope">
          <el-button type="text" size="small" @click="addOrUpdateHandle(scope.row.id)">修改</el-button>
          <el-button type="text" size="small" @click="deleteHandle(scope.row.id)">删除</el-button>
        </template>
      </el-table-column>
    </el-table>
    <el-pagination
      @size-change="sizeChangeHandle"
      @current-change="currentChangeHandle"
      :current-page="pageIndex"
      :page-sizes="[10, 20, 50, 100]"
      :page-size="pageSize"
      :total="totalPage"
      layout="total, sizes, prev, pager, next, jumper">
    </el-pagination>
    <!-- 弹窗, 新增 / 修改 -->
    <add-or-update v-if="addOrUpdateVisible" ref="addOrUpdate" @refreshDataList="getDataList"></add-or-update>
  </div>
</template>

<script>
  import AddOrUpdate from './member-add-or-update'
  export default {
    data () {
      return {
        dataForm: {
          key: ''
        },
        dataList: [],
        pageIndex: 1,
        pageSize: 10,
        totalPage: 0,
        dataListLoading: false,
        dataListSelections: [],
        addOrUpdateVisible: false
      }
    },
    components: {
      AddOrUpdate
    },
    activated () {
      this.getDataList()
    },
    methods: {
      // 获取数据列表
      getDataList () {
        this.dataListLoading = true
        this.$http({
          url: this.$http.adornUrl('/users/member/list'),
          method: 'get',
          params: this.$http.adornParams({
            'page': this.pageIndex,
            'limit': this.pageSize,
            'key': this.dataForm.key
          })
        }).then(({data}) => {
          if (data && data.code === 0) {
            this.dataList = data.page.list
            this.totalPage = data.page.totalCount
          } else {
            this.dataList = []
            this.totalPage = 0
          }
          this.dataListLoading = false
        })
      },
      // 每页数
      sizeChangeHandle (val) {
        this.pageSize = val
        this.pageIndex = 1
        this.getDataList()
      },
      // 当前页
      currentChangeHandle (val) {
        this.pageIndex = val
        this.getDataList()
      },
      // 多选
      selectionChangeHandle (val) {
        this.dataListSelections = val
      },
      // 新增 / 修改
      addOrUpdateHandle (id) {
        this.addOrUpdateVisible = true
        this.$nextTick(() => {
          this.$refs.addOrUpdate.init(id)
        })
      },
      // 删除
      deleteHandle (id) {
        var ids = id ? [id] : this.dataListSelections.map(item => {
          return item.id
        })
        this.$confirm(`确定对[id=${ids.join(',')}]进行[${id ? '删除' : '批量删除'}]操作?`, '提示', {
          confirmButtonText: '确定',
          cancelButtonText: '取消',
          type: 'warning'
        }).then(() => {
          this.$http({
            url: this.$http.adornUrl('/users/member/delete'),
            method: 'post',
            data: this.$http.adornData(ids, false)
          }).then(({data}) => {
            if (data && data.code === 0) {
              this.$message({
                message: '操作成功',
                type: 'success',
                duration: 1500,
                onClose: () => {
                  this.getDataList()
                }
              })
            } else {
              this.$message.error(data.msg)
            }
          })
        })
      },
      formatDate(row, column) {
          // 获取单元格数据
          let data = row[column.property]
          if(data == null) {
              return null
          }
          let dt = new Date(data)
          return (dt.getMonth() + 1) + '月' + dt.getDate()+'日'
      },
      formatDateAll(row, column) {
          // 获取单元格数据
          let data = row[column.property]
          if(data == null) {
              return null
          }
          let dt = new Date(data)
          return dt.getFullYear() + '年' + (dt.getMonth() + 1) + '月' + dt.getDate()+'日'
      },
      formatRole( row, column) {
            return row.sex == 0 ? "男" : row.sex == 1 ? "女" : "中性";
      }
    }
  }
</script>
