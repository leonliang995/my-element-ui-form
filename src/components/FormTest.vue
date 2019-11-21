  <template>
  <div>
    <h3>YForm表单</h3>
    <hr>
    <!-- v-model实现 -->
    <!-- <y-input :value="model.username" @input="model.username=$event"></y-input> -->
    <y-form :model="model" :rules="rules" ref="yForm">
      <y-form-item label="用户名" prop="username">
        <y-input v-model="model.username"></y-input>
      </y-form-item>
      <y-form-item label="确认密码" prop="password">
        <y-input type="password" v-model="model.password"></y-input>
      </y-form-item>
      <y-form-item>
        <el-button type="primary" @click="submitForm('yForm')">提交</el-button>
      </y-form-item>
    </y-form>
  </div>
</template>
  
  <script>
import YInput from './YInput.vue';
import YFormItem from './YFormItem.vue';
import YForm from './YForm.vue';
export default {
  components: {
    YInput, YFormItem, YForm
  },
  data () {
    return {
      // 数据模型
      model: { username: "tom", password: "" },
      // 校验规则
      rules: {
        username: [{ required: true, message: "请输入用户名" }],
        password: [{ required: true, message: "请输入密码" }]
      }
    };
  },
  methods: {
    submitForm (form) {
      // 表单全局校验
      this.$refs[form].validate(valid => {
        if (valid) {
          alert("请求登录!");
        } else {
          alert("校验失败！");
        }
      });
    }
  }

}
  </script>
  
  <style lang="scss" scoped>
</style>