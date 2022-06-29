<template>
  <el-dialog
    :title="!dataForm.id ? '新增' : '修改'"
    :close-on-click-modal="false"
    :visible.sync="visible">
    <el-form :model="dataForm" :rules="dataRule" ref="dataForm" @keyup.enter.native="dataFormSubmit()" label-width="110px">
    <el-form-item label="任务名称" prop="taskName">
      <el-input v-model="dataForm.taskName" placeholder="任务名称"></el-input>
    </el-form-item>

    <!-- <el-form-item label="状态" prop="status">
      <el-input v-model="dataForm.status" placeholder="状态"></el-input>
    </el-form-item> -->

    <el-form-item label="周期" prop="cycle">
      <el-input v-model="dataForm.cycle" placeholder="周期"></el-input>
    </el-form-item>
    <el-form-item label="bean名称" prop="beanName">
      <el-input v-model="dataForm.beanName" placeholder="bean名称"></el-input>
    </el-form-item>
    <el-form-item label="参数" prop="args">
      <el-input v-model="dataForm.args" placeholder="参数"></el-input>
    </el-form-item>

    <!-- <el-form-item label="执行人所属ID" prop="cardholderId">
      <el-input v-model="dataForm.cardholderId" placeholder="执行人所属ID"></el-input>
    </el-form-item>
    <el-form-item label="执行人" prop="cardholder">
      <el-input v-model="dataForm.cardholder" placeholder="执行人"></el-input>
    </el-form-item> -->

    <el-form-item label="执行人" prop="cardholderId">
      <el-select v-model="dataForm.cardholderId" placeholder="请选择" filterable clearable>
        <el-option
          v-for="item in payUsers"
          :key="item.id"
          :label="item.memberName"
          :value="item.id">
        </el-option>
      </el-select>
    </el-form-item>


    <el-form-item label="cron表达式" prop="cron">
      <el-input v-model="dataForm.cron" placeholder="cron表达式"></el-input>
    </el-form-item>
    <!-- <el-form-item label="计划执行时间" prop="planExecutionTime">
      <el-input v-model="dataForm.planExecutionTime" placeholder="计划执行时间"></el-input>
    </el-form-item> -->
       <el-form-item label="计划执行时间" prop="planExecutionTime">
      <el-date-picker
          v-model="dataForm.planExecutionTime"
          type="datetime"
          placeholder="选择日期时间"
          align="right"
          :picker-options="pickerOptions"
          value-format="yyyy-MM-dd HH:mm:ss">
      </el-date-picker>
    </el-form-item>

    <!-- <el-form-item label="上次执行时间" prop="upFinishTime">
      <el-input v-model="dataForm.upFinishTime" placeholder="上次执行时间"></el-input>
    </el-form-item>
    <el-form-item label="上次执行完成时间" prop="upExecutionTime">
      <el-input v-model="dataForm.upExecutionTime" placeholder="上次执行完成时间"></el-input>
    </el-form-item>
    <el-form-item label="上次执行结果" prop="upResult">
      <el-input v-model="dataForm.upResult" placeholder="上次执行结果"></el-input>
    </el-form-item>
    <el-form-item label="耗时" prop="consumingTime">
      <el-input v-model="dataForm.consumingTime" placeholder="耗时"></el-input>
    </el-form-item>
    <el-form-item label="下次执行时间" prop="nextTime">
      <el-input v-model="dataForm.nextTime" placeholder="下次执行时间"></el-input>
    </el-form-item> -->

    <el-form-item label="备注" prop="description">
      <el-input v-model="dataForm.description" placeholder="备注"></el-input>
    </el-form-item>
    <!-- <el-form-item label="创建人ID" prop="createrId">
      <el-input v-model="dataForm.createrId" placeholder="创建人ID"></el-input>
    </el-form-item>
    <el-form-item label="创建人" prop="creater">
      <el-input v-model="dataForm.creater" placeholder="创建人"></el-input>
    </el-form-item>
    <el-form-item label="创建时间" prop="createTime">
      <el-input v-model="dataForm.createTime" placeholder="创建时间"></el-input>
    </el-form-item>
    <el-form-item label="修改人ID" prop="updaterId">
      <el-input v-model="dataForm.updaterId" placeholder="修改人ID"></el-input>
    </el-form-item>
    <el-form-item label="修改人" prop="updater">
      <el-input v-model="dataForm.updater" placeholder="修改人"></el-input>
    </el-form-item>
    <el-form-item label="修改时间" prop="updateTime">
      <el-input v-model="dataForm.updateTime" placeholder="修改时间"></el-input>
    </el-form-item>
    <el-form-item label="是否显示[1-显示，0-不显示]" prop="showStatus">
      <el-input v-model="dataForm.showStatus" placeholder="是否显示[1-显示，0-不显示]"></el-input>
    </el-form-item>
    <el-form-item label="排序" prop="sort">
      <el-input v-model="dataForm.sort" placeholder="排序"></el-input>
    </el-form-item>
    <el-form-item label="检索首字母" prop="firstLetter">
      <el-input v-model="dataForm.firstLetter" placeholder="检索首字母"></el-input>
    </el-form-item> -->
    </el-form>
    <span slot="footer" class="dialog-footer">
      <el-button @click="visible = false">取消</el-button>
      <el-button type="primary" @click="dataFormSubmit()">确定</el-button>
    </span>
  </el-dialog>
</template>

<script>
  export default {
    data () {
      return {
        payUsers:[],
        visible: false,
        dataForm: {
          id: 0,
          taskName: '',
          status: '',
          cycle: '',
          beanName: '',
          args: '',
          cardholderId: '',
          cardholder: '',
          cron: '',
          planExecutionTime: '',
          upFinishTime: '',
          upExecutionTime: '',
          upResult: '',
          consumingTime: '',
          nextTime: '',
          description: '',
          createrId: '',
          creater: '',
          createTime: '',
          updaterId: '',
          updater: '',
          updateTime: '',
          showStatus: '',
          sort: '',
          firstLetter: ''
        },
        dataRule: {
          taskName: [
            { required: true, message: '任务名称不能为空', trigger: 'blur' }
          ],
          status: [
            { required: false, message: '状态不能为空', trigger: 'blur' }
          ],
          cycle: [
            { required: false, message: '周期不能为空', trigger: 'blur' }
          ],
          beanName: [
            { required: false, message: 'bean名称不能为空', trigger: 'blur' }
          ],
          args: [
            { required: false, message: '参数不能为空', trigger: 'blur' }
          ],
          cardholderId: [
            { required: true, message: '执行人所属ID不能为空', trigger: 'blur' }
          ],
          cardholder: [
            { required: false, message: '执行人不能为空', trigger: 'blur' }
          ],
          cron: [
            { required: false, message: 'cron表达式不能为空', trigger: 'blur' }
          ],
          planExecutionTime: [
            { required: true, message: '计划执行时间不能为空', trigger: 'blur' }
          ],
          upFinishTime: [
            { required: false, message: '上次执行时间不能为空', trigger: 'blur' }
          ],
          upExecutionTime: [
            { required: false, message: '上次执行完成时间不能为空', trigger: 'blur' }
          ],
          upResult: [
            { required: false, message: '上次执行结果不能为空', trigger: 'blur' }
          ],
          consumingTime: [
            { required: false, message: '耗时不能为空', trigger: 'blur' }
          ],
          nextTime: [
            { required: false, message: '下次执行时间不能为空', trigger: 'blur' }
          ],
          description: [
            { required: false, message: '备注不能为空', trigger: 'blur' }
          ],
          createrId: [
            { required: true, message: '创建人ID不能为空', trigger: 'blur' }
          ],
          creater: [
            { required: true, message: '创建人不能为空', trigger: 'blur' }
          ],
          createTime: [
            { required: true, message: '创建时间不能为空', trigger: 'blur' }
          ],
          updaterId: [
            { required: true, message: '修改人ID不能为空', trigger: 'blur' }
          ],
          updater: [
            { required: true, message: '修改人不能为空', trigger: 'blur' }
          ],
          updateTime: [
            { required: true, message: '修改时间不能为空', trigger: 'blur' }
          ],
          showStatus: [
            { required: true, message: '是否显示[1-显示，0-不显示]不能为空', trigger: 'blur' }
          ],
          sort: [
            { required: true, message: '排序不能为空', trigger: 'blur' }
          ],
          firstLetter: [
            { required: true, message: '检索首字母不能为空', trigger: 'blur' }
          ]
        },
        pickerOptions: {
          shortcuts: [{
            text: '今天',
            onClick(picker) {
              picker.$emit('pick', new Date());
            }
          }, {
            text: '昨天',
            onClick(picker) {
              const date = new Date();
              date.setTime(date.getTime() - 3600 * 1000 * 24);
              picker.$emit('pick', date);
            }
          }, {
            text: '一周前',
            onClick(picker) {
              const date = new Date();
              date.setTime(date.getTime() - 3600 * 1000 * 24 * 7);
              picker.$emit('pick', date);
            }
          }]
        }
      }
    },
    methods: {
      init (id) {
        this.getPayUsers();
        this.dataForm.id = id || 0
        this.visible = true
        this.$nextTick(() => {
          this.$refs['dataForm'].resetFields()
          if (this.dataForm.id) {
            this.$http({
              url: this.$http.adornUrl(`/todo/thing/info/${this.dataForm.id}`),
              method: 'get',
              params: this.$http.adornParams()
            }).then(({data}) => {
              if (data && data.code === 0) {
                this.dataForm.taskName = data.thing.taskName
                this.dataForm.status = data.thing.status
                this.dataForm.cycle = data.thing.cycle
                this.dataForm.beanName = data.thing.beanName
                this.dataForm.args = data.thing.args
                this.dataForm.cardholderId = data.thing.cardholderId
                this.dataForm.cardholder = data.thing.cardholder
                this.dataForm.cron = data.thing.cron
                this.dataForm.planExecutionTime = data.thing.planExecutionTime
                this.dataForm.upFinishTime = data.thing.upFinishTime
                this.dataForm.upExecutionTime = data.thing.upExecutionTime
                this.dataForm.upResult = data.thing.upResult
                this.dataForm.consumingTime = data.thing.consumingTime
                this.dataForm.nextTime = data.thing.nextTime
                this.dataForm.description = data.thing.description
                this.dataForm.createrId = data.thing.createrId
                this.dataForm.creater = data.thing.creater
                this.dataForm.createTime = data.thing.createTime
                this.dataForm.updaterId = data.thing.updaterId
                this.dataForm.updater = data.thing.updater
                this.dataForm.updateTime = data.thing.updateTime
                this.dataForm.showStatus = data.thing.showStatus
                this.dataForm.sort = data.thing.sort
                this.dataForm.firstLetter = data.thing.firstLetter
              }
            })
          }
        })
      },
      // 表单提交
      dataFormSubmit () {
        this.$refs['dataForm'].validate((valid) => {
          if (valid) {
            this.$http({
              url: this.$http.adornUrl(`/todo/thing/${!this.dataForm.id ? 'save' : 'update'}`),
              method: 'post',
              data: this.$http.adornData({
                'id': this.dataForm.id || undefined,
                'taskName': this.dataForm.taskName,
                'status': this.dataForm.status,
                'cycle': this.dataForm.cycle,
                'beanName': this.dataForm.beanName,
                'args': this.dataForm.args,
                'cardholderId': this.dataForm.cardholderId,
                'cardholder': this.dataForm.cardholder,
                'cron': this.dataForm.cron,
                'planExecutionTime': this.dataForm.planExecutionTime,
                'upFinishTime': this.dataForm.upFinishTime,
                'upExecutionTime': this.dataForm.upExecutionTime,
                'upResult': this.dataForm.upResult,
                'consumingTime': this.dataForm.consumingTime,
                'nextTime': this.dataForm.nextTime,
                'description': this.dataForm.description,
                'createrId': this.dataForm.createrId,
                'creater': this.dataForm.creater,
                'createTime': this.dataForm.createTime,
                'updaterId': this.dataForm.updaterId,
                'updater': this.dataForm.updater,
                'updateTime': this.dataForm.updateTime,
                'showStatus': this.dataForm.showStatus,
                'sort': this.dataForm.sort,
                'firstLetter': this.dataForm.firstLetter
              })
            }).then(({data}) => {
              if (data && data.code === 0) {
                this.$message({
                  message: '操作成功',
                  type: 'success',
                  duration: 1500,
                  onClose: () => {
                    this.visible = false
                    this.$emit('refreshDataList')
                  }
                })
              } else {
                this.$message.error(data.msg)
              }
            })
          }
        })
      },
      getPayUsers(){
        //发送请求获取当前节点最新的数据
      this.$http({
        url: this.$http.adornUrl('/todo/thing/payUserVos'),
        method: "get"
      })
        .then(({ data }) => {
          //请求成功
          // console.log("要回显的数据", data);
          this.payUsers=data.data;
        })
        .catch(() => {});
      }
    }
  }
</script>
