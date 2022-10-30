<template>
  <el-card shadow="never" class="aui-card--fill">
    <div class="mod-ppgData__ppgdata}">
      <el-form :inline="true" :model="dataForm" @keyup.enter.native="getDataList()">
        <el-form-item>
          <el-input v-model="dataForm.dataid" placeholder="dataid" clearable></el-input>
        </el-form-item>
        <el-form-item>
          <el-button @click="getDataList()">{{ $t('query') }}</el-button>
        </el-form-item>
        <el-form-item>
          <el-button type="info" @click="exportHandle()">{{ $t('export') }}</el-button>
        </el-form-item>
        <el-form-item>
          <el-button v-if="$hasPermission('ppgData:ppgdata:save')" type="primary" @click="addOrUpdateHandle()">{{ $t('add') }}</el-button>
        </el-form-item>
        <el-form-item>
          <el-button v-if="$hasPermission('ppgData:ppgdata:delete')" type="danger" @click="deleteHandle()">{{ $t('deleteBatch') }}</el-button>
        </el-form-item>
      </el-form>
      <el-table v-loading="dataListLoading" :data="dataList" border @selection-change="dataListSelectionChangeHandle" style="width: 100%;">
        <el-table-column type="selection" header-align="center" align="center" width="50"></el-table-column>
        <el-table-column prop="dataid" label="记录id" header-align="center" align="center"></el-table-column>
        <el-table-column prop="patientid" label="被采集者id" header-align="center" align="center"></el-table-column>
        <el-table-column prop="operatorid" label="采集人id" header-align="center" align="center"></el-table-column>
        <el-table-column prop="collectingdevice" label="采集设备" header-align="center" align="center"></el-table-column>
        <el-table-column prop="devicesn" label="设备唯一标识码" header-align="center" align="center"></el-table-column>
        <el-table-column prop="lasteatingtime" label="上次用餐时间" header-align="center" align="center"></el-table-column>
        <el-table-column prop="bgdevicenumber" label="蓝牙采集设备设备号" header-align="center" align="center"></el-table-column>
        <el-table-column prop="testendtime" label="采集结束时间" header-align="center" align="center"></el-table-column>
        <el-table-column prop="uploadtime" label="上传时间" header-align="center" align="center"></el-table-column>
        <el-table-column prop="bgdeviceversion" label="硬件版本号" header-align="center" align="center"></el-table-column>
        <el-table-column prop="note" label="备注" header-align="center" align="center"></el-table-column>
        <el-table-column prop="contrastbloodsugar" label="对比血糖" header-align="center" align="center"></el-table-column>
        <el-table-column prop="eatingstatus" label="进食状态" header-align="center" align="center"></el-table-column>
        <el-table-column prop="truebs" label="真实血糖" header-align="center" align="center"></el-table-column>
        <el-table-column :label="$t('handle')" fixed="right" header-align="center" align="center" width="150">
          <template v-slot="scope">
            <el-button v-if="$hasPermission('ppgData:ppgdata:update')" type="text" size="small" @click="addOrUpdateHandle(scope.row.id)">{{ $t('update') }}</el-button>
            <el-button v-if="$hasPermission('ppgData:ppgdata:delete')" type="text" size="small" @click="deleteHandle(scope.row.id)">{{ $t('delete') }}</el-button>
          </template>
        </el-table-column>
      </el-table>
      <el-pagination
        :current-page="page"
        :page-sizes="[10, 20, 50, 100]"
        :page-size="limit"
        :total="total"
        layout="total, sizes, prev, pager, next, jumper"
        @size-change="pageSizeChangeHandle"
        @current-change="pageCurrentChangeHandle">
      </el-pagination>
      <!-- 弹窗, 新增 / 修改 -->
      <add-or-update v-if="addOrUpdateVisible" ref="addOrUpdate" @refreshDataList="getDataList"></add-or-update>
    </div>
  </el-card>
</template>

<script>
    import mixinViewModule from '@/mixins/view-module'
    import AddOrUpdate from './ppgdata-add-or-update'

    export default {
  mixins: [mixinViewModule],
  data () {
    return {
      mixinViewModuleOptions: {
        getDataListURL: '/ppgData/ppgdata/page',
        getDataListIsPage: true,
        exportURL: '/ppgData/ppgdata/export',
        deleteURL: '/ppgData/ppgdata',
        deleteIsBatch: true
      },
      dataForm: {
        dataid: ''
      }
    }
  },
  components: {
    AddOrUpdate
  }
}
</script>
