<template>
  <el-dialog :visible.sync="visible" :title="!dataForm.patientid ? $t('add') : $t('update')"
             :close-on-click-modal="false" :close-on-press-escape="false">
    <el-form :model="dataForm" :rules="dataRule" ref="dataForm" @keyup.enter.native="dataFormSubmitHandle()"
             :label-width="$i18n.locale === 'en-US' ? '120px' : '80px'">
      <el-form-item label="姓名" prop="patientname">
        <el-input v-model="dataForm.patientname" placeholder="姓名"></el-input>
      </el-form-item>
      <el-form-item label="性别" prop="sex">
        <el-input v-model="dataForm.sex" placeholder="性别"></el-input>
      </el-form-item>
      <el-form-item label="生日" prop="birthday">
        <el-date-picker v-model="dataForm.birthday" placeholder="生日" value-format="yyyy-MM-dd HH:mm:ss"></el-date-picker>
      </el-form-item>
      <el-form-item label="身高" prop="height">
        <el-input v-model="dataForm.height" placeholder="身高"></el-input>
      </el-form-item>
      <el-form-item label="体重" prop="weight">
        <el-input v-model="dataForm.weight" placeholder="体重"></el-input>
      </el-form-item>
    </el-form>
    <template slot="footer">
      <el-button @click="visible = false" >{{ $t('cancel') }}</el-button>
      <el-button type="primary" @click="dataFormSubmitHandle()">{{ $t('confirm') }}</el-button>
    </template>
  </el-dialog>
</template>

<script>
import debounce from 'lodash/debounce'

export default {
  data() {
    return {
      visible: false,
      dataForm: {
        patientid: '',
        patientname: '',
        age: '',
        sex: '',
        birthday: '',
        height: '',
        weight: '',
        bmi: '',
        operatorid: '',
        createtime: '',
        recordisdeleted: '',
        recordupdatetime: '',
        reviser: ''
      }
    }
  },
  computed: {
    dataRule() {
      return {
        patientname: [
          {required: true, message: this.$t('validate.required'), trigger: 'blur'}
        ],
        age: [
          {required: true, message: this.$t('validate.required'), trigger: 'blur'}
        ],
        sex: [
          {required: true, message: this.$t('validate.required'), trigger: 'blur'}
        ],
        birthday: [
          {required: true, message: this.$t('validate.required'), trigger: 'blur'}
        ],
        height: [
          {required: true, message: this.$t('validate.required'), trigger: 'blur'}
        ],
        weight: [
          {required: true, message: this.$t('validate.required'), trigger: 'blur'}
        ],
        bmi: [
          {required: true, message: this.$t('validate.required'), trigger: 'blur'}
        ],
        operatorid: [
          {required: true, message: this.$t('validate.required'), trigger: 'blur'}
        ]
      }
    }
  },
  methods: {
    init() {
      this.visible = true
      this.$nextTick(() => {
        this.$refs['dataForm'].resetFields()
        if (this.dataForm.patientid) {
          this.getInfo()
        }
      })
    },
    // 获取信息
    getInfo() {
      this.$http.get(`/patient/patient/${this.dataForm.patientid}`).then(({data: res}) => {
        if (res.code !== 0) {
          return this.$message.error(res.msg)
        }
        this.dataForm = {
          ...this.dataForm,
          ...res.data
        }
      }).catch(() => {
      })
    },
    // 表单提交
    dataFormSubmitHandle: debounce(function () {
      this.$refs['dataForm'].validate((valid) => {
        if (!valid) {
          return false
        }
        this.$http[!this.dataForm.patientid ? 'post' : 'put']('/patient/patient/', this.dataForm).then(({data: res}) => {
          if (res.code !== 0) {
            return this.$message.error(res.msg)
          }
          this.$message({
            message: this.$t('prompt.success'),
            type: 'success',
            duration: 500,
            onClose: () => {
              this.visible = false
              this.$emit('refreshDataList')
            }
          })
        }).catch(() => {
        })
      })
    }, 1000, {'leading': true, 'trailing': false})
  }
}
</script>
