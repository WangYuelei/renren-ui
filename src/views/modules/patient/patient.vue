<template>
  <el-card shadow="never" class="aui-card--fill">
    <div class="mod-patient__patient}">
      <el-form :inline="true" :model="dataForm" @keyup.enter.native="getDataList()">
        <el-form-item>
          <el-input v-model="dataForm.operatorid" placeholder="采集者id" clearable></el-input>
        </el-form-item>
        <el-form-item>
          <el-input v-model="dataForm.patientid" placeholder="人员id" clearable></el-input>
        </el-form-item>
        <el-form-item>
          <el-input v-model="dataForm.patientname" placeholder="姓名" clearable></el-input>
        </el-form-item>
        <span class="demonstration">创建时间</span>
        <el-date-picker
            v-model="dataForm.createStart"
            type="date"
            placeholder="起始日期">
        </el-date-picker>
        <span class="demonstration">-</span>
        <el-date-picker
            v-model="dataForm.createEnd"
            type="date"
            placeholder="结束日期">
        </el-date-picker>
        <el-form-item>
          <el-button @click="getDataList()">{{ $t('query') }}</el-button>
        </el-form-item>
        <el-form-item>
          <el-button type="info" @click="exportHandle()">{{ $t('export') }}</el-button>
        </el-form-item>
        <el-form-item>
          <el-button v-if="$hasPermission('patient:patient:save')" type="primary" @click="addOrUpdateHandle()">{{ $t('add') }}</el-button>
        </el-form-item>
        <el-form-item>
          <el-button v-if="$hasPermission('patient:patient:delete')" type="danger" @click="deleteHandle()">{{ $t('deleteBatch') }}</el-button>
        </el-form-item>
      </el-form>
      <el-table v-loading="dataListLoading" :data="dataList" border @selection-change="dataListSelectionChangeHandle" style="width: 100%;">
        <el-table-column type="selection" header-align="center" align="center" width="50"></el-table-column>
        <el-table-column sortable prop="patientid" label="id" header-align="center" align="center"></el-table-column>
        <el-table-column prop="patientname" label="姓名" header-align="center" align="center"></el-table-column>
        <el-table-column prop="age" label="年龄" header-align="center" align="center" ></el-table-column>
        <el-table-column prop="sex" label="性别" header-align="center" align="center" :formatter="formatSex"></el-table-column>
        <el-table-column prop="birthday" label="生日" header-align="center" align="center" :formatter="formatDate"></el-table-column>
        <el-table-column prop="height" label="身高" header-align="center" align="center"></el-table-column>
        <el-table-column prop="weight" label="体重" header-align="center" align="center"></el-table-column>
        <el-table-column prop="bmi" label="bmi" header-align="center" align="center"></el-table-column>
        <el-table-column prop="operatorid" label="采集者id" header-align="center" align="center"></el-table-column>
        <el-table-column prop="createtime" label="创建时间" header-align="center" align="center"></el-table-column>
        <el-table-column prop="recordisdeleted" label="是否删除" header-align="center" align="center" :formatter="IsDelete"></el-table-column>
        <el-table-column prop="recordupdatetime" label="更新时间" header-align="center" align="center"></el-table-column>
        <el-table-column prop="reviser" label="修最后一次改者" header-align="center" align="center"></el-table-column>
        <el-table-column :label="$t('handle')" fixed="right" header-align="center" align="center" width="150">
          <template v-slot="scope">
            <el-button v-if="$hasPermission('patient:patient:update')" type="primary" size="small" @click="addOrUpdateHandle(scope.row.patientid)">{{ $t('update') }}</el-button>
            <el-button v-if="$hasPermission('patient:patient:delete')" type="danger" size="small" @click="deleteHandle(scope.row.patientid)" >{{ $t('delete') }}</el-button>
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
    import AddOrUpdate from './patient-add-or-update'
    export default {
  mixins: [mixinViewModule],
  data () {
    return {
      mixinViewModuleOptions: {
        getDataListURL: '/patient/patient/page',
        getDataListIsPage: true,
        exportURL: '/patient/patient/export',
        deleteURL: '/patient/patient',
        deleteIsBatch: true
      },
      dataForm: {
        patientid: '',
        operatorid:'',
        patientname:'',
        createStart:'',
        createEnd:'',
      }
    }
  },methods:{
        formatSex:function (row,column,cellValue,index) {
          return row.sex==1?'男':row.sex==2?'女':'未知'
        },
        IsDelete:function (row,column,cellValue,index) {
          return row.recordisdeleted==0?'否':row.recordisdeleted==1?'是':'未知'
        },
        formatDate:function (row){
          return row.birthday.substring(0,10);
        }
      },
  components: {
    AddOrUpdate
  }
}
</script>
