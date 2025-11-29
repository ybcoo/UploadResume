<template>
  <main class="mainContainer">
    <aside class="left">
      <header class="header">
        <span class="titleOne">Finish!</span>
        <span class="titleOne">Upload Your Resume</span>
        <span class="contentOne"
          >Upload your resume, the platform will help you parse and optimize, you can also skip this
          step</span
        >
      </header>
      <footer class="footer">
        <img class="pic" :src="pic" alt="Fail" />
      </footer>
    </aside>
    <section class="right">
      <div class="body">
        <header class="header">
          <span class="titleTwo">Upload file</span>
        </header>
        <main class="main">
          <a-upload
            draggable
            action="/"
            :file-list="fileList"
            :show-file-list="false"
            :auto-upload="false"
            :multiple="true"
            @change="onChange"
            style="
              width: 100%;
              height: 100%;
              display: flex;
              justify-content: center;
              align-items: center;
            "
          >
            <template #upload-button>
              <div class="slotContent">
                <img :src="iconSvg?.upload" alt="" />
                <span class="contentTwo">
                  Drag your resume file to this area, or click on the area to select the appropriate
                  file to upload</span
                >
              </div>
            </template>
          </a-upload>
        </main>
        <section class="uploadList">
          <div class="item" v-for="(item, index) in fileList">
            <div>{{ item?.name }}</div>
            <img
              class="deleteItem"
              @click="deleteItem(index)"
              :src="iconSvg?.delete"
              alt="delete"
            />
          </div>
        </section>
        <footer class="footer">
          <button class="button" disabled>Last step</button>
          <button class="button" :disabled="!fileList?.length">Finish</button>
        </footer>
        <div class="step" style="display: flex; justify-content: center">
          <div class="line">
            <div class="line-left">
              <div class="stepRadius">
                <img :src="check" alt="" />
              </div>
            </div>
            <div class="line-middle">
              <div class="stepRadius">
                <img :src="check" alt="" />
              </div>
            </div>
            <div class="line-right">
              <div class="stepRadius">
                <span style="font-size: 11px; font-weight: 500; color: #ffffff">3</span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
  </main>
</template>
<script setup lang="ts">
import pic from "@/assets/image/pic.png";
import check from "@/assets/image/check.png";
import { iconSvg } from "@/assets/icon/icon";
import { ref } from "vue";
const fileList = ref<any>([]);
const onChange = (_: any, fileItem: any) => {
  if (fileItem) {
    fileList.value.push(fileItem);
  }
};
const deleteItem = (index: number) => {
  fileList.value.splice(index, 1);
};
</script>
<style lang="scss" scoped>
.mainContainer {
  width: 100%;
  height: 100%;
  background-color: #f8fbf9;
  display: flex;
  @media (max-width: 1400px) {
    flex-direction: column;
    overflow-y: auto;
  }
}
.left {
  flex: 1;
  padding-top: 103px;
  display: flex;
  flex-direction: column;
  .header {
    padding: 0 77px 0 102px;
    display: flex;
    flex-direction: column;
    flex: 1;
  }
  .footer {
    flex: 1 1 auto;
    max-height: 569px;
    overflow: hidden;
    @media (max-width: 1400px) {
      display: flex;
      justify-content: center;
    }
    .pic {
      max-width: 763px;
      width: 100%;
      height: 100%;
      max-height: 569px;
    }
  }
}
.body {
  padding: 0 129px 0 129px;
  background-color: #ffffff;
  border-radius: 32px;
  width: 100%;
  height: 100%;
  overflow-y: auto; //部分电脑高度未必为1080 兜底操作
  @media (max-width: 1400px) {
    overflow: hidden;
    min-height: 922px;
  }
  @media (max-width: 600px) {
    padding: 0;
  }
  .header {
    @media (max-width: 600px) {
      display: flex;
      justify-content: center;
    }
  }
  .main {
    width: 100%;
    height: 100%;
    max-width: 685px;
    max-height: 420px;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: #f2faff;
    border: 1px dashed #0538bb;
    border-radius: 15px;
    @media (max-width: 1400px) {
      max-width: 100%;
    }
  }
  .footer {
    display: flex;
    justify-content: center;
    gap: 29px;
    padding: 0px 0px 104px 0px;
    width: 100%;
  }
  .uploadList {
    display: flex;
    flex-direction: column;
    height: 98px;
    padding-top: 10px;
    padding-bottom: 10px;
    gap: 10px;
    overflow-y: auto;
    .item {
      background-color: #f7f8fa;
      padding: 5px;
      display: flex;
      justify-content: space-between;
    }
  }
}
.right {
  flex: 1;
  //   padding-top: 103px;
  padding: 103px 102px 55px 0px;
  @media (max-width: 1400px) {
    padding: 103px 0px 55px 0px;
  }
}
.titleOne {
  color: #000000;
  font-size: 40px;
  font-weight: 400;
}
.titleTwo {
  color: #060326;
  font-size: 36px;
  font-weight: 500;
  padding: 30px 0px 53px 0px;
  display: inline-block;
}
.contentOne {
  padding-top: 20px;
  font-size: 20px;
  font-weight: 400;
  color: #a5a5a5;
}
.contentTwo {
  display: inline-block;
  padding-left: 93px;
  padding-right: 93px;
  text-align: center;
  font-size: 16px;
  font-weight: 400;
  color: #a5a5a5;
}
.slotContent {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  gap: 14px;
}

.button {
  flex: 0 1 272px;
  height: 67px;
  background-color: #1b5aff;
  color: #ffffff;
  border-radius: 8px;
  font-size: 24px;
  font-weight: 400;
}
button:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}
::v-deep .arco-upload {
  width: 100%;
}
.deleteItem {
  cursor: pointer;
}
.stepRadius {
  width: 26px;
  height: 26px;
  border-radius: 50%;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #85a7ff;
}
.step {
  width: 100%;
  .line {
    display: flex;
    flex: 1;
    height: 4px;
    max-width: 343px;
    background-color: #85a7ff;
    border-radius: 2px;
    justify-content: space-between;
    align-items: center;
    padding-left: 28px;
    padding-right: 28px;
  }
}

// ::v-deep .arco-steps-item-title{
//   height: 26px;
//   padding: 0;
//   margin: 0;
// }
// ::v-deep .arco-steps-icon{
//   width: 26px;
//   height: 26px;
// }
// ::v-deep(.arco-steps-item),
// ::v-deep(.arco-steps-item-node){
//   margin: 0;
//   padding: 0;
// }
//
</style>
