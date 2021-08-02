<template>
  <div class="container">
    <global-header :user="currentUser"> </global-header>

    <validate-form @form-submit="onFormSubmit">
      <div class="mb-3">
        <label class="form-label">邮箱地址</label>
        <validate-input
          :rules="emailRules"
          v-model="emailVal"
          type="text"
          placeholder="请输入邮箱地址"
        ></validate-input>
      </div>
      <div class="mb-3">
        <label class="form-label">Password</label>
        <validate-input
          :rules="passwordRules"
          v-model="passwordVal"
          type="password"
          placeholder="请输入密码"
        ></validate-input>
      </div>
      <template #submit>
        <span class="btn btn-danger">Submit</span>
      </template>
    </validate-form>
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive, ref } from "vue";
import "bootstrap/dist/css/bootstrap.min.css";
import GlobalHeader, { UserProps } from "./components/GlobalHeader.vue";
import ValidateInput, { RulesProp } from "./components/ValidateInput.vue";
import ValidateForm from "./components/ValidateForm.vue";

const currentUser: UserProps = {
  isLogin: true,
  name: "cxx",
  id: 1,
  // isLogin: false,
};

export default defineComponent({
  name: "Form",
  components: {
    GlobalHeader,
    ValidateInput,
    ValidateForm,
  },
  setup() {
    const passwordVal = ref("");
    const passwordRules: RulesProp = [
      { type: "required", message: "密码不能为空" },
    ];
    const emailVal = ref("viking");
    const emailRules: RulesProp = [
      {
        type: "required",
        message: "电子邮箱不能为空",
      },
      {
        type: "email",
        message: "请输入正确的电子邮箱格式",
      },
    ];
    const onFormSubmit = (result: boolean) => {
      console.log("1234", result);
    };
    const emailReg =
      /^[A-Za-z0-9\u4e00-\u9fa5]+@[a-zA-Z0-9_-]+(\.[a-zA-Z0-9_-]+)+$/;
    const emailRef = reactive({
      val: "",
      error: false,
      message: "",
    });
    const validateEmail = () => {
      if (emailRef.val.trim() === "") {
        emailRef.error = true;
        emailRef.message = "can not be empty";
      } else if (!emailReg.test(emailRef.val)) {
        emailRef.error = true;
        emailRef.message = "should be valid email";
      }
    };
    return {
      currentUser: currentUser,
      emailRef,
      validateEmail,
      emailRules,
      emailVal,
      passwordVal,
      passwordRules,
      onFormSubmit,
    };
  },
});
</script>

<style scoped>
</style>