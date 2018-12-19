<script>
export default {
  onShow(){
    console.log('显示了');
    wx.showModal({
      title: '友情提示', //提示的标题,
      content: '长按可删除备忘事项 谨慎操作', //提示的内容,
      showCancel: true, //是否显示取消按钮,
      cancelText: '', //取消按钮的文字，默认为取消，最多 4 个字符,
      cancelColor: '#000000', //取消按钮的文字颜色,
      confirmText: '确定', //确定按钮的文字，默认为取消，最多 4 个字符,
      confirmColor: '#3CC51F', //确定按钮的文字颜色,
      success: res => {
        if (res.confirm) {
          console.log('用户点击确定')
        } else if (res.cancel) {
          console.log('用户点击取消')
        }
      }
    });
  }
}
</script>

<style>
</style>
