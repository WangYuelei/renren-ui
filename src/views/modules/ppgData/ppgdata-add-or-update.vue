<template>
  <el-dialog :visible.sync="visible" :title="!dataForm.dataid ? $t('add') : $t('update')" :close-on-click-modal="false" :close-on-press-escape="false">
    <el-form :model="dataForm" :rules="dataRule" ref="dataForm" @keyup.enter.native="dataFormSubmitHandle()" :label-width="$i18n.locale === 'en-US' ? '120px' : '80px'">
          <el-form-item label="被采集者ID" prop="patientid">
          <el-input v-model="dataForm.patientid" placeholder="被采集者ID"></el-input>
      </el-form-item>
          <el-form-item label="采集人ID" prop="operatorid">
          <el-input v-model="dataForm.operatorid" placeholder="采集人ID"></el-input>
      </el-form-item>
          <el-form-item label="采集设备" prop="collectingdevice">
          <el-input v-model="dataForm.collectingdevice" placeholder="采集设备"></el-input>
      </el-form-item>
          <el-form-item label="设备采样率" prop="samplerate">
          <el-input v-model="dataForm.samplerate" placeholder="设备采样率"></el-input>
      </el-form-item>
          <el-form-item label="采集 设备名称" prop="devicemodel">
          <el-input v-model="dataForm.devicemodel" placeholder="采集 设备名称"></el-input>
      </el-form-item>
          <el-form-item label="设备唯一标识码" prop="devicesn">
          <el-input v-model="dataForm.devicesn" placeholder="设备唯一标识码"></el-input>
      </el-form-item>
          <el-form-item label="操作系统版本" prop="osversion">
          <el-input v-model="dataForm.osversion" placeholder="操作系统版本"></el-input>
      </el-form-item>
          <el-form-item label="" prop="deviceid">
          <el-input v-model="dataForm.deviceid" placeholder=""></el-input>
      </el-form-item>
          <el-form-item label="LED1(1050nm)原始数据：波形" prop="led1050nm">
          <el-input v-model="dataForm.led1050nm" placeholder="LED1(1050nm)原始数据：波形"></el-input>
      </el-form-item>
          <el-form-item label="LED2(940nm) 原始数据：波形" prop="led940nm">
          <el-input v-model="dataForm.led940nm" placeholder="LED2(940nm) 原始数据：波形"></el-input>
      </el-form-item>
          <el-form-item label="LED3(650nm) 原始数据：波形" prop="led650nm">
          <el-input v-model="dataForm.led650nm" placeholder="LED3(650nm) 原始数据：波形"></el-input>
      </el-form-item>
          <el-form-item label="环境光原始数据：波形" prop="environmentLight">
          <el-input v-model="dataForm.environmentLight" placeholder="环境光原始数据：波形"></el-input>
      </el-form-item>
          <el-form-item label="MTP10 电路板温度（单位：mV）" prop="mtp10TemperatureSelf">
          <el-input v-model="dataForm.mtp10TemperatureSelf" placeholder="MTP10 电路板温度（单位：mV）"></el-input>
      </el-form-item>
          <el-form-item label="MTP10 指夹探头温度（单位：mV）" prop="mtp10RadiationTemperature">
          <el-input v-model="dataForm.mtp10RadiationTemperature" placeholder="MTP10 指夹探头温度（单位：mV）"></el-input>
      </el-form-item>
          <el-form-item label="热敏电阻" prop="ntcConductionThermal">
          <el-input v-model="dataForm.ntcConductionThermal" placeholder="热敏电阻"></el-input>
      </el-form-item>
          <el-form-item label="SHT30 电路板温度*100 后的值（单位：℃）" prop="sht30EnvironmentTemperature">
          <el-input v-model="dataForm.sht30EnvironmentTemperature" placeholder="SHT30 电路板温度*100 后的值（单位：℃）"></el-input>
      </el-form-item>
          <el-form-item label="SHT30 电路板湿度*100 后的值（单位：%RH）" prop="sht30EnvironmentHumidity">
          <el-input v-model="dataForm.sht30EnvironmentHumidity" placeholder="SHT30 电路板湿度*100 后的值（单位：%RH）"></el-input>
      </el-form-item>
          <el-form-item label="SHT30 指夹探头温度*100 后的值（单位：℃）" prop="sht30FingerTemperature">
          <el-input v-model="dataForm.sht30FingerTemperature" placeholder="SHT30 指夹探头温度*100 后的值（单位：℃）"></el-input>
      </el-form-item>
          <el-form-item label="SHT30 指夹探头湿度*100 后的值（单位：%RH）" prop="sht30FingerHumidity">
          <el-input v-model="dataForm.sht30FingerHumidity" placeholder="SHT30 指夹探头湿度*100 后的值（单位：%RH）"></el-input>
      </el-form-item>
          <el-form-item label="上次用餐时间" prop="lasteatingtime">
          <el-input v-model="dataForm.lasteatingtime" placeholder="上次用餐时间"></el-input>
      </el-form-item>
          <el-form-item label="电池电压" prop="batteryVoltage">
          <el-input v-model="dataForm.batteryVoltage" placeholder="电池电压"></el-input>
      </el-form-item>
          <el-form-item label="蓝牙采集设备设备号" prop="bgdevicenumber">
          <el-input v-model="dataForm.bgdevicenumber" placeholder="蓝牙采集设备设备号"></el-input>
      </el-form-item>
          <el-form-item label="采集结束时间" prop="testendtime">
          <el-input v-model="dataForm.testendtime" placeholder="采集结束时间"></el-input>
      </el-form-item>
          <el-form-item label="上传时间" prop="uploadtime">
          <el-input v-model="dataForm.uploadtime" placeholder="上传时间"></el-input>
      </el-form-item>
          <el-form-item label="" prop="recordupdatetime">
          <el-input v-model="dataForm.recordupdatetime" placeholder=""></el-input>
      </el-form-item>
          <el-form-item label="0正常,1删除" prop="recordisdeleted">
          <el-input v-model="dataForm.recordisdeleted" placeholder="0正常,1删除"></el-input>
      </el-form-item>
          <el-form-item label="硬件版本号" prop="bgdeviceversion">
          <el-input v-model="dataForm.bgdeviceversion" placeholder="硬件版本号"></el-input>
      </el-form-item>
          <el-form-item label="修改人" prop="reviser">
          <el-input v-model="dataForm.reviser" placeholder="修改人"></el-input>
      </el-form-item>
          <el-form-item label="备注" prop="note">
          <el-input v-model="dataForm.note" placeholder="备注"></el-input>
      </el-form-item>
          <el-form-item label="" prop="sypressure">
          <el-input v-model="dataForm.sypressure" placeholder=""></el-input>
      </el-form-item>
          <el-form-item label="" prop="sypressure2">
          <el-input v-model="dataForm.sypressure2" placeholder=""></el-input>
      </el-form-item>
          <el-form-item label="" prop="diapressure">
          <el-input v-model="dataForm.diapressure" placeholder=""></el-input>
      </el-form-item>
          <el-form-item label="" prop="diapressure2">
          <el-input v-model="dataForm.diapressure2" placeholder=""></el-input>
      </el-form-item>
          <el-form-item label="对比血糖" prop="contrastbloodsugar">
          <el-input v-model="dataForm.contrastbloodsugar" placeholder="对比血糖"></el-input>
      </el-form-item>
          <el-form-item label="进食状态 0:未知 1:餐前 2:餐后" prop="eatingstatus">
          <el-input v-model="dataForm.eatingstatus" placeholder="进食状态 0:未知 1:餐前 2:餐后"></el-input>
      </el-form-item>
          <el-form-item label="真实血糖" prop="truebs">
          <el-input v-model="dataForm.truebs" placeholder="真实血糖"></el-input>
      </el-form-item>
          <el-form-item label="是否替换过标定(工作站用) 0 否 1 是" prop="isreplace">
          <el-input v-model="dataForm.isreplace" placeholder="是否替换过标定(工作站用) 0 否 1 是"></el-input>
      </el-form-item>
          <el-form-item label="替换标定类型(工作站用)" prop="replaceaitype">
          <el-input v-model="dataForm.replaceaitype" placeholder="替换标定类型(工作站用)"></el-input>
      </el-form-item>
      </el-form>
    <template slot="footer">
      <el-button @click="visible = false">{{ $t('cancel') }}</el-button>
      <el-button type="primary" @click="dataFormSubmitHandle()">{{ $t('confirm') }}</el-button>
    </template>
  </el-dialog>
</template>

<script>
    import debounce from 'lodash/debounce'

    export default {
  data () {
    return {
      visible: false,
      dataForm: {
        dataid: '',
        patientid: '',
        operatorid: '',
        collectingdevice: '',
        samplerate: '',
        devicemodel: '',
        devicesn: '',
        osversion: '',
        deviceid: '',
        led1050nm: '',
        led940nm: '',
        led650nm: '',
        environmentLight: '',
        mtp10TemperatureSelf: '',
        mtp10RadiationTemperature: '',
        ntcConductionThermal: '',
        sht30EnvironmentTemperature: '',
        sht30EnvironmentHumidity: '',
        sht30FingerTemperature: '',
        sht30FingerHumidity: '',
        lasteatingtime: '',
        batteryVoltage: '',
        bgdevicenumber: '',
        testendtime: '',
        uploadtime: '',
        recordupdatetime: '',
        recordisdeleted: '',
        bgdeviceversion: '',
        reviser: '',
        note: '',
        sypressure: '',
        sypressure2: '',
        diapressure: '',
        diapressure2: '',
        contrastbloodsugar: '',
        eatingstatus: '',
        truebs: '',
        isreplace: '',
        replaceaitype: ''
      }
    }
  },
  computed: {
    dataRule () {
      return {
        patientid: [
          { required: true, message: this.$t('validate.required'), trigger: 'blur' }
        ],
        operatorid: [
          { required: true, message: this.$t('validate.required'), trigger: 'blur' }
        ],
        collectingdevice: [
          { required: true, message: this.$t('validate.required'), trigger: 'blur' }
        ],
        samplerate: [
          { required: true, message: this.$t('validate.required'), trigger: 'blur' }
        ],
        devicemodel: [
          { required: true, message: this.$t('validate.required'), trigger: 'blur' }
        ],
        devicesn: [
          { required: true, message: this.$t('validate.required'), trigger: 'blur' }
        ],
        osversion: [
          { required: true, message: this.$t('validate.required'), trigger: 'blur' }
        ],
        deviceid: [
          { required: true, message: this.$t('validate.required'), trigger: 'blur' }
        ],
        led1050nm: [
          { required: true, message: this.$t('validate.required'), trigger: 'blur' }
        ],
        led940nm: [
          { required: true, message: this.$t('validate.required'), trigger: 'blur' }
        ],
        led650nm: [
          { required: true, message: this.$t('validate.required'), trigger: 'blur' }
        ],
        environmentLight: [
          { required: true, message: this.$t('validate.required'), trigger: 'blur' }
        ],
        mtp10TemperatureSelf: [
          { required: true, message: this.$t('validate.required'), trigger: 'blur' }
        ],
        mtp10RadiationTemperature: [
          { required: true, message: this.$t('validate.required'), trigger: 'blur' }
        ],
        ntcConductionThermal: [
          { required: true, message: this.$t('validate.required'), trigger: 'blur' }
        ],
        sht30EnvironmentTemperature: [
          { required: true, message: this.$t('validate.required'), trigger: 'blur' }
        ],
        sht30EnvironmentHumidity: [
          { required: true, message: this.$t('validate.required'), trigger: 'blur' }
        ],
        sht30FingerTemperature: [
          { required: true, message: this.$t('validate.required'), trigger: 'blur' }
        ],
        sht30FingerHumidity: [
          { required: true, message: this.$t('validate.required'), trigger: 'blur' }
        ],
        lasteatingtime: [
          { required: true, message: this.$t('validate.required'), trigger: 'blur' }
        ],
        batteryVoltage: [
          { required: true, message: this.$t('validate.required'), trigger: 'blur' }
        ],
        bgdevicenumber: [
          { required: true, message: this.$t('validate.required'), trigger: 'blur' }
        ],
        testendtime: [
          { required: true, message: this.$t('validate.required'), trigger: 'blur' }
        ],
        uploadtime: [
          { required: true, message: this.$t('validate.required'), trigger: 'blur' }
        ],
        recordupdatetime: [
          { required: true, message: this.$t('validate.required'), trigger: 'blur' }
        ],
        recordisdeleted: [
          { required: true, message: this.$t('validate.required'), trigger: 'blur' }
        ],
        bgdeviceversion: [
          { required: true, message: this.$t('validate.required'), trigger: 'blur' }
        ],
        reviser: [
          { required: true, message: this.$t('validate.required'), trigger: 'blur' }
        ],
        note: [
          { required: true, message: this.$t('validate.required'), trigger: 'blur' }
        ],
        sypressure: [
          { required: true, message: this.$t('validate.required'), trigger: 'blur' }
        ],
        sypressure2: [
          { required: true, message: this.$t('validate.required'), trigger: 'blur' }
        ],
        diapressure: [
          { required: true, message: this.$t('validate.required'), trigger: 'blur' }
        ],
        diapressure2: [
          { required: true, message: this.$t('validate.required'), trigger: 'blur' }
        ],
        contrastbloodsugar: [
          { required: true, message: this.$t('validate.required'), trigger: 'blur' }
        ],
        eatingstatus: [
          { required: true, message: this.$t('validate.required'), trigger: 'blur' }
        ],
        truebs: [
          { required: true, message: this.$t('validate.required'), trigger: 'blur' }
        ],
        isreplace: [
          { required: true, message: this.$t('validate.required'), trigger: 'blur' }
        ],
        replaceaitype: [
          { required: true, message: this.$t('validate.required'), trigger: 'blur' }
        ]
      }
    }
  },
  methods: {
    init () {
      this.visible = true
      this.$nextTick(() => {
        this.$refs['dataForm'].resetFields()
        if (this.dataForm.dataid) {
          this.getInfo()
        }
      })
    },
    // 获取信息
    getInfo () {
      this.$http.get(`/ppgData/ppgdata/${this.dataForm.dataid}`).then(({ data: res }) => {
        if (res.code !== 0) {
          return this.$message.error(res.msg)
        }
        this.dataForm = {
          ...this.dataForm,
          ...res.data
        }
      }).catch(() => {})
    },
    // 表单提交
    dataFormSubmitHandle: debounce(function () {
      this.$refs['dataForm'].validate((valid) => {
        if (!valid) {
          return false
        }
        this.$http[!this.dataForm.dataid ? 'post' : 'put']('/ppgData/ppgdata/', this.dataForm).then(({ data: res }) => {
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
        }).catch(() => {})
      })
    }, 1000, { 'leading': true, 'trailing': false })
  }
}
</script>
