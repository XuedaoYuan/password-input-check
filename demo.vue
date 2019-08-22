<template>
  <div class="custom-input__container">
    <div class="tips" v-show="showTips">
      <div class="title">至少包含</div>
      <div :class="{'ok': uppercaseStatus}">一个大写字母</div>
      <div :class="{'ok': lowercaseStatus}">一个小写字母</div>
      <div :class="{'ok': numberStatus}">一个数字</div>
      <div :class="{'ok': lengthStatus}">10个字符</div>
    </div>
    <input
      type="password"
      @input="handleInput"
      v-model="password"
      @focus="hanldeFocus"
      @blur="handleBlur"
    />
  </div>
</template>

<script>
const uppercaseReg = /[A-Z]{1,}/
const lowercaseReg = /[a-z]{1,}/
const numberReg = /[0-9]{1,}/
const passwordLength = 10
export default {
  data() {
    return {
      uppercaseStatus: false,
      lowercaseStatus: false,
      numberStatus: false,
      lengthStatus: false,
      password: '',
      showTips: false
    }
  },
  methods: {
    hanldeFocus() {
      this.showTips = true
    },
    handleBlur() {
      this.showTips = false
    },
    handleInput() {
      const password = this.password
      if (uppercaseReg.test(password)) {
        this.uppercaseStatus = true
      } else {
        this.uppercaseStatus = false
      }
      if (lowercaseReg.test(password)) {
        this.lowercaseStatus = true
      } else {
        this.lowercaseStatus = false
      }
      if (numberReg.test(password)) {
        this.numberStatus = true
      } else {
        this.numberStatus = false
      }

      if (password.length >= passwordLength) {
        this.lengthStatus = true
      } else {
        this.lengthStatus = false
      }
      return (
        this.uppercaseStatus &&
        this.lowercaseStatus &&
        this.numberStatus &&
        this.lengthStatus
      )
    }
  }
}
</script>

<style scoped lang="stylus">
.custom-input__container {
  display: inline-block;
  border: 1px solid #ccc;
  padding: 0 10px;
  border-radius: 2px;
  position: relative;

  .tips {
    width: 120px;
    padding: 18px 18px;
    background-color: #fff;
    position: absolute;
    right: -60px;
    bottom: 38px;
    border: 1px solid #ccc;

    .title {
      color: #bbb;
      margin-bottom: 10px;
    }

    div {
      font-size: 12px;
      line-height: 20px;
    }

    div.ok {
      color: rgb(91, 193, 115);
      text-decoration: line-through;
    }
  }

  input {
    outline: none;
    width: 220px;
    height: 38px;
    border: none;
    font-size: 16px;
    line-height: 38px;
  }
}
</style>
