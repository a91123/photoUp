<template>
  <div>
    <div class="container">
      <div ref="memberImg" @click="member.click()" class="upload">
        <div v-if="!haveMemberPhoto" class="default">點我上傳 圖片大小盡量是150x100的倍數</div>
        <input ref="member" v-show="0" @change="handleMember" type="file" />
      </div>
      <div class="inputGroup">
        <label for="name">姓名</label>
        <input id="name" type="text" />
        <label for="phone">電話</label>
        <input id="phone" type="text" />
        <label for="address">地址</label>
        <input id="address" type="text" />
      </div>
    </div>
  </div>
</template>

<script>
import { defineComponent, ref } from 'vue'
export default defineComponent({
  name: 'Home',
  setup () {
    const member = ref()
    const memberImg = ref()
    const haveMemberPhoto = ref(false)
    const checkFile = (file) => {
      let pass = true
      const isJPG = file.type === 'image/jpeg'
      const fileSizeLimit = 1024 * 200
      // 檢查格式
      if (!isJPG) {
        alert('不是jpg')
        pass = false
      }
      // 檢查 大小
      if (file.size > fileSizeLimit) {
        pass = false
        alert('檔案超過200kb')
      }
      return pass
    }
    const handleMember = (e) => {
      const pass = checkFile(e.target.files[0])
      if (pass) {
        const objectURL = URL.createObjectURL(e.target.files[0])
        console.log(e.target.files[0])
        console.log(memberImg.value)
        memberImg.value.style.backgroundImage = `url('${objectURL}')`
        haveMemberPhoto.value = true
      }
    }
    return {
      handleMember,
      member,
      memberImg,
      haveMemberPhoto
    }
  }

})
</script>
<style>
.container {
  margin: 0 auto;
  width: 800px;
  background-color: pink;
}
.upload {
  margin: 0 auto;
  cursor: pointer;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #ccc;
  background-size: cover;
  width: 150px;
  height: 100px;
}
.default {
  color: white;
  font-size: 15px;
  text-align: center;
}
.inputGroup {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.inputGroup input {
  display: block;
}
</style>
