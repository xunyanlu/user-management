<template>
  <div>
    <el-button type="primary" icon="el-icon-search" class="shousuo" @click="selectRouteCable">搜 索</el-button>
    <el-button type="primary" icon="el-icon-plus" @click="getPlanBillNo">新 增</el-button>
    <el-table
        :data="routeCableList"
        border
        style="width: 100%">
      <el-table-column

          prop="cable_seg_name"
          label="光缆段"
          width="250">
      </el-table-column>
      <el-table-column
          prop="station_a"
          label="A端站点"
          width="120">
      </el-table-column>
      <el-table-column
          prop="station_z"
          label="Z端站点"
          width="120">
      </el-table-column>
      <el-table-column
          prop="cable_name"
          label="光缆信息"
          width="200">
      </el-table-column>
      <el-table-column
          prop="is_main_backup"
          label="主备标识"
          width="300">
      </el-table-column>
      <el-table-column
          label="操作"
          width="100">
        <template slot-scope="scope">
          <el-button @click="handleClick(scope.row)" type="text" size="small">查看</el-button>
          <el-button type="text" size="small">编辑</el-button>
        </template>
      </el-table-column>
    </el-table>

    <!--    <el-button type="text" @click="dialogFormVisible = true">打开嵌套表单的 Dialog</el-button>-->

    <el-dialog title="新增规划设计评估记录" :visible.sync="dialogFormVisible" width="1410px">
      <el-form :model="form" inline label-position="left">
        <el-form-item label="规划工单编号:" :label-width="formLabelWidth" :style="{marginLeft: '30px'}">
          <el-input v-model="form.planDesignNO" autocomplete="off" :style="{width: '450px'}"></el-input>
        </el-form-item>
        <el-form-item label="规划设计名称:" :label-width="formLabelWidth" :style="{marginLeft: '130px'}">
          <el-input v-model="form.planDesignName" autocomplete="off" :style="{width: '450px'}"></el-input>
        </el-form-item>
        <el-form-item label="设计单位:" :label-width="formLabelWidth" :style="{marginLeft: '30px'}">
          <el-input v-model="form.designcompany" autocomplete="off" :style="{width: '450px'}"></el-input>
        </el-form-item>
        <el-form-item label="业务类型:" :label-width="formLabelWidth" :style="{marginLeft: '130px'}">
          <el-input v-model="form.specid" autocomplete="off" :style="{width: '450px'}"></el-input>
        </el-form-item>
        <el-form-item label="项目总负责人:" :label-width="formLabelWidth" :style="{marginLeft: '30px'}">
          <el-input v-model="form.projectdirector" autocomplete="off" :style="{width: '450px'}"></el-input>
        </el-form-item>
        <el-form-item label="专业负责人:" :label-width="formLabelWidth" :style="{marginLeft: '130px'}">
          <el-input v-model="form.specleader" autocomplete="off" :style="{width: '450px'}"></el-input>
        </el-form-item>
        <el-form-item label="设计人:" :label-width="formLabelWidth" :style="{marginLeft: '30px'}">
          <el-input v-model="form.designer" autocomplete="off" :style="{width: '450px'}"></el-input>
        </el-form-item>
        <el-form-item label="校审人:" :label-width="formLabelWidth" :style="{marginLeft: '130px'}">
          <el-input v-model="form.reviewer" autocomplete="off" :style="{width: '450px'}"></el-input>
        </el-form-item>

        <el-form-item label="上坐标:" :label-width="formLabelWidth" :style="{marginLeft: '30px'}">
          <el-input v-model="form.top" autocomplete="off" :style="{width: '50px'}"></el-input>
        </el-form-item>
        <el-form-item label="左坐标:" :label-width="formLabelWidth" :style="{marginLeft: '30px'}">
          <el-input v-model="form.left" autocomplete="off" :style="{width: '50px'}"></el-input>
        </el-form-item>
        <el-form-item label="下坐标:" :label-width="formLabelWidth" :style="{marginLeft: '30px'}">
          <el-input v-model="form.bottom" autocomplete="off" :style="{width: '50px'}"></el-input>
        </el-form-item>
        <el-form-item label="右坐标:" :label-width="formLabelWidth" :style="{marginLeft: '30px'}">
          <el-input v-model="form.right" autocomplete="off" :style="{width: '50px'}"></el-input>
        </el-form-item>
      </el-form>
      <!--      插入上传文件代码-->

      <el-row>
        <el-col :span="12" :flex="true">
      <el-upload
          class="upload-demo"
          action="http://localhost:8080/upload.do"
          :on-remove="handleRemove"
          :before-remove="beforeRemove"
          :limit="1"
          :on-exceed="exceedTips"
          :on-success="handleDwgSuccess1"
          :span="12">
        <div class="el-upload-CAD">1、系统CAD图纸:</div>
<!--        <div class="el-upload-EXCEL1">2、波段规划EXCEL:</div>-->
<!--        <div class="el-upload-EXCEL">3、系统规划EXCEL:</div>-->

        <el-button size="small" type="primary" class="button1">点击上传</el-button>
        <div slot="tip" class="el-upload__tip1">上传dwg格式文件，不超过10MB，上传个数限制1个。</div>
<!--        <div slot="tip" class="el-upload__tip2">上传excel格式文件，不超过10MB，上传个数限制1个。</div>-->
<!--        <div slot="tip" class="el-upload__tip3">上传excel格式文件，不超过10MB，上传个数限制1个。</div>-->
      </el-upload>
        </el-col>

        <el-col :span="12" :flex="true">
      <el-upload
          class="upload-demo"
          action="http://localhost:8080/upload.do"
          :on-remove="handleRemove"
          :before-remove="beforeRemove"
          :limit="1"
          :on-exceed="exceedTips"
          :on-success="handleDwgSuccess2"
          :span="12">

        <div class="el-upload-CAD">2、波段规划EXCEL:</div>
        <el-button size="small" type="primary" class="button1">点击上传</el-button>
        <div slot="tip" class="el-upload__tip">上传excel格式文件，不超过10MB，上传个数限制1个。</div>
      </el-upload>
        </el-col>

        <el-col :span="12" :flex="true">
          <el-upload
              class="upload-demo"
              action="http://localhost:8080/upload.do"
              :on-remove="handleRemove"
              :before-remove="beforeRemove"
              :limit="1"
              :on-exceed="exceedTips"
              :on-success="handleDwgSuccess3"
              :span="12">

            <div class="el-upload-CAD">3、系统规划EXCEL:</div>
            <el-button size="small" type="primary" class="button1">点击上传</el-button>
            <div slot="tip" class="el-upload__tip">上传excel格式文件，不超过10MB，上传个数限制1个。</div>
          </el-upload>
        </el-col>
      </el-row>

      <div slot="footer" class="dialog-footer">
        <el-button type="primary" @click="createBillAndAnalyse">保存并分析</el-button>
        <el-button type="primary" @click="save">保 存</el-button>
      </div>

    </el-dialog>

  </div>

</template>

<script>
import axios from 'axios'

export default {
  name: 'HelloWorld',

  data() {
    return {
      routeCableList: [],
      form: {
        planDesignNO: '',
        planDesignName: '安徽二干华为***规划设计',
        designcompany: '大唐电信',
        specid: '1',
        projectdirector: '张珊珊',
        specleader: '庄义涛',
        designer: '毛猫',
        reviewer: '葛尧',
        top:'1',
        left:'2',
        bottom:'3',
        right:'4'
      },
      dialogTableVisible: false,
      dialogFormVisible: false,
      formLabelWidth: '130px',

      dwgFileUrl: "",
    }

  },
  methods: {

    search(){

    },
    selectRouteCable() {
      //用axios对后端请求获取数据
      let _this = this;
      axios.get('http://localhost:8080/selectRouteCableList.do')
          .then(function (response) {
            // 处理成功情况
            console.log(response);
            _this.planDesignNO = response.data.data;
          })
          .catch(function (error) {
            // 处理错误情况
            console.log(error);
          })
          .then(function () {
            // 总是会执行
          });
    },

    getPlanBillNo() {
      //用axios对后端请求获取数据
      let _this = this;//axio中的this被转化了，并不是vue的实例
      axios.get('http://localhost:8080/getPlanBillNo.do')
          .then(function (response) {
            // 处理成功情况

            console.log(response);
            console.log(response.data.data);

            _this.form.planDesignNO = response.data.data;
            _this.dialogFormVisible = true;


          })
          .catch(function (error) {
            // 处理错误情况
            console.log(error);
          })
          .then(function () {
            // 总是会执行
          });
    },
    save() {
      console.log("准备保存");
      let _this = this;//axio中的this被转化了，并不是vue的实例
      axios.post('http://localhost:8080/creatBill.do', {
        "plan_bill_no": this.form.planDesignNO,
        "plan_design_name": this.form.planDesignName,
        "design_company": this.form.designcompany,
        "spec_id": this.form.specid,
        "project_director": this.form.projectdirector,
        "spec_leader": this.form.specleader,
        "designer": this.form.designer,
        "reviewer": this.form.reviewer,
        "system_cad_file_url":this.dwgFileUrl,
        "system_excel_file_url":this.ExcFileUrl,
        "channel_excel_file_url":this.ExclFileUrl,
        "cad_coord_left":this.form.left,
        "cad_coord_top":this.form.top,
        "cad_coord_right":this.form.right,
        "cad_coord_bottom":this.form.bottom
      })
          .then(function (response) {
            // 处理成功情况
            console.log("!!!", response);
            if (response.data.code == 200) {
              _this.dialogFormVisible = false;
              _this.$message({
                message: response.data.message,
                type: 'success'
              });
            } else {
              _this.$message.error(response.data.message);
            }
          })
          .catch(function (error) {
            // 处理错误情况
            console.log(error);
          })
          .then(function () {
            // 总是会执行
          });
    },

    createBillAndAnalyse() {
      console.log("准备保存");
      let _this = this;//axio中的this被转化了，并不是vue的实例
      axios.post('http://localhost:8080/createBillAndAnalyse.do', {
        "plan_bill_no": this.form.planDesignNO,
        "plan_design_name": this.form.planDesignName,
        "design_company": this.form.designcompany,
        "spec_id": this.form.specid,
        "project_director": this.form.projectdirector,
        "spec_leader": this.form.specleader,
        "designer": this.form.designer,
        "reviewer": this.form.reviewer,
        "system_cad_file_url":this.dwgFileUrl,
        "system_excel_file_url":this.ExcFileUrl,
        "channel_excel_file_url":this.ExclFileUrl,
        "cad_coord_left":this.form.left,
        "cad_coord_top":this.form.top,
        "cad_coord_right":this.form.right,
        "cad_coord_bottom":this.form.bottom
      })
          .then(function (response) {
            // 处理成功情况
            console.log("!!!", response);
            if (response.data.code == 200) {
              _this.dialogFormVisible = false;
              _this.$message({
                message: response.data.message,
                type: 'success'
              });
            } else {
              _this.$message.error(response.data.message);
            }
          })
          .catch(function (error) {
            // 处理错误情况
            console.log(error);
          })
          .then(function () {
            // 总是会执行
          });
    },

    handleRemove(file, fileList) {
      console.log(file, fileList);
    },
    beforeRemove(file, fileList) {
      return this.$confirm(`确定移除 ${file.name}？`);
    },
    handleDwgSuccess1(res) {
      this.dwgFileUrl = res.data[0];
      console.log("地址：", this.dwgFileUrl);
    },
    handleDwgSuccess2(res) {
      this.ExcFileUrl = res.data[0];
      console.log("地址：", this.ExcFileUrl);
    },
    handleDwgSuccess3(res) {
      this.ExclFileUrl = res.data[0];
      console.log("地址：", this.ExclFileUrl);
    },
    exceedTips() {
      this.$message.error("只能上传一个文件！");
    }

  }


}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.shousuo {
  position: relative;
}


</style>
