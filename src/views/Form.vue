<template>
  <div class="form">
    <div class="form-title">入力フォーム</div>
    <div class="form-template">
      <form-component
        v-for="form in formValue"
        :key="form.id"
        :form="form"
        :validationMessage="validationMessage"
        @change-value="changeValue"
      />
      <div>
        <button @click="submit">登録</button>
      </div>
    </div>
  </div>
</template>

<script>
import FormComponent from "@/components/FormComponent.vue";

import { GENDER_LIST } from "@/mixins/genderList";
import { PREFECTURE_LIST } from "@/mixins/prefectureList";
import { BROWSER_LIST } from "@/mixins/browserList";

import { validationMethod } from "@/common/validationMethod";

export default {
  name: "Form",
  components: {
    FormComponent,
  },
  data() {
    return {
      formValue: [
        {
          id: 1,
          value: "",
          keyName: "name",
          label: "名前",
          formType: "TextField",
        },
        {
          id: 2,
          value: null,
          keyName: "age",
          label: "年齢",
          formType: "NumberField",
        },
        {
          id: 3,
          value: null,
          keyName: "gender",
          data: GENDER_LIST,
          label: "性別",
          formType: "RadioButton",
        },
        {
          id: 4,
          value: null,
          keyName: "prefecture",
          data: PREFECTURE_LIST,
          label: "都道府県",
          formType: "SelectBox",
        },
        {
          id: 5,
          value: [],
          keyName: "browser",
          data: BROWSER_LIST,
          label: "使用したことのあるブラウザ",
          formType: "CheckBox",
        },
      ],
      validationSetting: {
        //バリデーションの条件を詰め込んだもの
        name: {
          name: "名前", //メッセージ出力時に使う文字列
          required: true, //必須かどうか
          length: [1, 32], //何文字以上何文字以下の指定
        },
        age: {
          name: "年齢",
          required: true,
          length: [1, 4],
          format: ["Number"],
        },
        gender: {
          name: "性別",
          required: true,
          format: ["Number"],
        },
        prefecture: {
          name: "都道府県",
          required: true,
          format: ["Number"],
        },
        browser: {
          name: "ブラウザ",
          required: false,
          format: ["Array"],
        },
      },
      validationStatus: true,
      validationMessage: {
        //引っかかってる場合のみメッセージが入ります
        name: "",
        age: "",
        gender: "",
        prefecture: "",
        browser: "",
      },
    };
  },
  methods: {
    changeValue(key, value) {
      this.formValue[key - 1].value = value;
    },
    validate() {
      const formValueObject = {};
      this.formValue.forEach((form) => {
        formValueObject[form.keyName] = form.value;
      });
      return validationMethod(
        formValueObject,
        this.validationSetting,
        this.validationMessage
      );
    },
    submit() {
      const validationResult = this.validate();
      this.validationStatus = validationResult.status;
      this.validationMessage = validationResult.message;
    },
  },
};
</script>

<style lang="scss">
.form {
  width: 640px;
  padding: 16px;
  &-title {
    font-size: 24px;
  }
  &-template {
    width: 100%;
    padding: 16px;
  }
}
</style>