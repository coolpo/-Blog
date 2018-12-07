## Welcome to GitHub Pages

- [追随前人的脚步系列之《理解JavaScript执行上下文和执行栈》](https://github.com/coolpo/blog/issues/2)
- [追随前人的脚步系列之《理解JavaScript执行上下文和变量》](https://github.com/coolpo/blog/issues/3)
- [测试链接](https://github.com/coolpo/blog/blob/master/pages/notes01.md)

### 现在是2018年11月24日02:57:53

```JavaScript
// 暂存 小程序云开发 上传代码
// 上传图片
  doUpload: function () {
    // 选择图片
    wx.chooseImage({
      count: 1,
      sizeType: ['compressed'],
      sourceType: ['album', 'camera'],
      success: function (res) {

        wx.showLoading({
          title: '上传中',
        })

        const filePath = res.tempFilePaths[0]

        // 上传图片
        const cloudPath = 'my-image' + filePath.match(/\.[^.]+?$/)[0]
        wx.cloud.uploadFile({
          cloudPath,
          filePath,
          success: res => {
            console.log('[上传文件] 成功：', res)

            app.globalData.fileID = res.fileID
            app.globalData.cloudPath = cloudPath
            app.globalData.imagePath = filePath

            wx.navigateTo({
              url: '../storageConsole/storageConsole'
            })
          },
          fail: e => {
            console.error('[上传文件] 失败：', e)
            wx.showToast({
              icon: 'none',
              title: '上传失败',
            })
          },
          complete: () => {
            wx.hideLoading()
          }
        })

      },
      fail: e => {
        console.error(e)
      }
    })
  },
```
