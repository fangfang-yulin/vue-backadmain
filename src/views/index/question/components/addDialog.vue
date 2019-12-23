<template>
  <!-- 新增对话框 -->
  <el-dialog class="add-dialog" fullscreen title="新增题库" :visible.sync="$parent.addFormVisible">
    <el-form ref="addForm" :model="addForm" :rules="addFormRules">
      <el-form-item label="学科" prop="subject" :label-width="formLabelWidth">
        <el-select v-model="addForm.subject" placeholder="请选择学科">
          <el-option v-for="item in $parent.subjectList" :key="item.id" :label="item.name" :value="item.id"></el-option>
        </el-select>
      </el-form-item>
      <el-form-item label="阶段" prop="step" :label-width="formLabelWidth">
        <el-select v-model="addForm.step" placeholder="请选择阶段">
          <el-option label="初级" :value="1"></el-option>
          <el-option label="中级" :value="2"></el-option>
          <el-option label="高级" :value="3"></el-option>
        </el-select>
      </el-form-item>
      <el-form-item label="企业" prop="enterprise" :label-width="formLabelWidth">
        <el-select v-model="addForm.enterprise" placeholder="请选择企业">
          <el-option
            v-for="item in $parent.enterpriseList"
            :key="item.id"
            :label="item.name"
            :value="item.id"
          ></el-option>
        </el-select>
      </el-form-item>
      <el-form-item label="城市" prop="city" :label-width="formLabelWidth">
        <!-- 将value值 设置为 label的选项 -->
        <el-cascader :props="props" v-model="addForm.city" :options="options"></el-cascader>
      </el-form-item>
      <el-form-item label="题型" prop="type" :label-width="formLabelWidth">
        <el-radio-group v-model="addForm.type">
          <el-radio :label="1">单选</el-radio>
          <el-radio :label="2">多选</el-radio>
          <el-radio :label="3">简答</el-radio>
        </el-radio-group>
      </el-form-item>
      <el-form-item label="难度" prop="difficulty" :label-width="formLabelWidth">
        <el-radio-group v-model="addForm.difficulty">
          <el-radio :label="1">简单</el-radio>
          <el-radio :label="2">一般</el-radio>
          <el-radio :label="3">困难</el-radio>
        </el-radio-group>
      </el-form-item>
    </el-form>
    <div slot="footer" class="dialog-footer">
      <el-button @click="$parent.addFormVisible = false">取 消</el-button>
      <el-button type="primary" @click="submitForm">确 定</el-button>
    </div>
  </el-dialog>
</template>

<script>
// 导入 新增接口
import { subjectAdd } from "../../../../api/subject.js";
// 导入 省市区数据
import { regionData } from "element-china-area-data";
export default {
  data() {
    return {
      // 级联选择器的数据
      options: regionData,
      // 级联选择器绑定的 选项
      props: { expandTrigger: "hover", value: "label" },
      // 表单数据
      addForm: {
        // 编号
        rid: "",
        // 名字
        name: "",
        // 简称
        short_name: "",
        // 简介
        intro: "",
        // 备注
        remark: ""
      },
      // 宽度
      formLabelWidth: "80px",
      // 添加表单验证规则
      addFormRules: {
        rid: [{ required: true, message: "题库编号不能为空", trigger: "blur" }],
        name: [{ required: true, message: "题库名称不能为空", trigger: "blur" }]
      }
    };
  },
  methods: {
    submitForm() {
      this.$refs.addForm.validate(valid => {
        if (valid) {
          // 对
          subjectAdd(this.addForm).then(res => {
            // window.console.log(res);
            if (res.code === 201) {
              this.$message.warning("题库编号已经存在了，请重新输入");
            } else if (res.code === 200) {
              this.$message.success("恭喜你，新增成功啦！");
              // 关闭弹框
              this.$parent.addFormVisible = false;
              // 调用父组件的 获取数据方法
              this.$parent.getData();
            }
          });
        } else {
          // 错
          this.$message.error("小老弟，数据不太对哦，检查一下呗！");
          return false;
        }
      });
    }
  }
};
</script>

<style lang="less">
.add-dialog {
  // 设置宽度
  .el-dialog {
    width: 602px;
  }
  // 对话框
  .el-dialog__header {
    background: linear-gradient(to right, #01c4fa, #1394fa);
    // 文字
    span {
      color: white;
    }
    i {
      color: white;
    }
  }
}
</style>
