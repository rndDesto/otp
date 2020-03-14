<template>
  <div class="home">
    <div class="otp" :class="{error: isError}">
      <input
        v-for="item in 4"
        :key="item"
        :data-otp="item"
        @keyup="onKeyDown"
        @focus="onBlockText"
        type="text"
        :maxlength="max"
        v-model="otpNum[item-1]"
      />
    </div>
    <p @click="onSubmitOtp">verify</p>
  </div>
</template>

<script>
// @ is an alias to /src

export default {
  name: 'Home',
  data () {
    return {
      max: 1,
      otpNum: [],
      otpCode: '1234',
      isError: false
    }
  },
  methods: {
    onNextForm (e) {
      const element = e.target
      const next = element.nextElementSibling
      if (next) {
        next.focus()
      }
      // e = (e) ? e : window.event;
      // var charCode = (e.which) ? e.which : e.keyCode;
      // console.log("keyup = ",charCode)
    },
    onPrevForm (e) {
      const element = e.target
      const prev = element.previousSibling
      if (prev) {
        prev.focus()
      }

      console.log('prev = ', prev)
    },
    onBlockText (e) {
      e.target.select()
    },
    onKeyDown (e) {
      e = e || window.event
      var charCode = e.which ? e.which : e.keyCode
      console.log('keydown = ', charCode)
      this.onNextForm(e)
      if (charCode === 39) {
        this.onNextForm(e)
      } else if (charCode === 37) {
        this.onPrevForm(e)
      }
      // if ((charCode > 31 && (charCode < 48 || charCode > 57)) && charCode !== 46) {
      //   evt.preventDefault();;
      // } else {
      //   return true;
      // }
    },
    onSubmitOtp () {
      const otp = this.otpNum.join('').toString()
      if (this.otpCode === otp) {
        console.log('sukses')
        this.isError = false
      } else {
        console.log('galgal')
        this.isError = true
      }
    }
  }
}
</script>

<style lang="scss" scoped>
.otp{
  &.error{
    input{
      border-color: red
      }
  }
}
</style>
