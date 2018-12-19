<template>
  <div class="beiwang">
    <div class="header">
      <input class="input-box" type="text" placeholder="添加待办事项" v-model="actions">
      <button class="add" @click="addaction">+</button>
    </div>
    <div class="content">
      <ul v-for="(item,index) in todolist" :key="index">
        <li @longtap="removeactions(index)">{{item}}</li>
      </ul>
    </div>
  </div>
</template>

<script>
  export default {
    data: function() {
      return {
        actions: "",
        todolist: []
        // todolist: []
      };
    },
    methods: {
      addaction() {
        console.log("触发了");
        console.log(this.actions);
        if (this.actions == "") {
          wx.showToast({
            title: "输入内容不能为空", //提示的内容,
            icon: "none", //图标,
            duration: 2000, //延迟时间,
            mask: true, //显示透明蒙层，防止触摸穿透,
            success: res => {}
          });
        } else {
          this.todolist.unshift(this.actions);
          this.actions = "";
          console.log(this.todolist);
        }
      },
      removeactions(index) {
        wx.showModal({
          title: "友情提示", //提示的标题,
          content: "真的要删除吗", //提示的内容,
          showCancel: true, //是否显示取消按钮,
          cancelText: "取消", //取消按钮的文字，默认为取消，最多 4 个字符,
          cancelColor: "#000000", //取消按钮的文字颜色,
          confirmText: "确定", //确定按钮的文字，默认为取消，最多 4 个字符,
          confirmColor: "#3CC51F", //确定按钮的文字颜色,
          success: res => {
            if (res.confirm) {
              console.log("用户点击确定");
              this.todolist.splice(index, 1);
              console.log(this.todolist);
            } else if (res.cancel) {
              console.log("用户点击取消");
            }
          }
        });
      }
    },
    onShow() {
      console.log('显示了');
      wx.getStorage({
        key: 'wantdo',
        success: (res) => {
          console.log(res.data)
        },
        fail: () => {},
        complete: () => {}
      })
    },
    onHide() {
      //console.log('卸载了');
      //页面卸载时保存
      wx.setStorage({
        key: "wantdo",
        data: this.todolist
      });
    },
    created() {
      // 调用应用实例的方法获取全局数据
    }
  };
</script>

<style scoped>
  .beiwang {
    padding: 0 20rpx;
  }
  .header {
    display: flex;
    height: 100rpx;
    margin: 20rpx 0;
  }
  .header .add {
    width: 130rpx;
    height: 90rpx;
    line-height: 90rpx;
    background-color: #c7edcc;
    display: block;
    margin-left: 20rpx;
  }
  .input-box {
    flex: 1;
    border: 1px solid gray;
    border-radius: 10rpx;
    height: 90rpx;
    padding-left: 20rpx;
    font-size: 30rpx;
  }
  .content ul li {
    border: 2rpx solid lightgray;
    margin-top: 40rpx;
    font-size: 30rpx;
    border-radius: 20rpx;
    /* height: 60rpx; */
    line-height: 60rpx;
    padding-left: 30rpx;
    overflow: hidden;
    word-wrap: break-word;
    /* height: 40rpx;
    line-height: 40rpx; */
  }
</style>
