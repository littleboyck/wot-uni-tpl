<script setup lang="ts">
definePage({
  name: 'album',
  style: {
    navigationBarTitleText: '保存图片至相册',
  },
})

// navigator.share 必须在https协议下才能使用，否则navigator.share 为 undefined

async function share() {
  // alert('开始分享');
  const response = await fetch('https://picsum.photos/200/300')
  const blob = await response.blob()
  const file = new File([blob], 'demo.jpg', { type: 'image/jpeg' })

  shareImage(file)
}

// 优化的分享函数（使用 else 明确分支）
async function shareImage(imageFile: File, title = '', text = '') {
  const shareData = {
    title,
    text,
    files: [imageFile],
  }

  // 方案1: 优先使用 Web Share API
  if (navigator.canShare && navigator.canShare(shareData)) {
    // alert('xxx');
    try {
      await navigator.share(shareData)
      console.log('分享成功')
    }
    catch (error) {
      console.warn('Web Share 失败:', error)
      // if (error.name !== 'AbortError') {
      //   console.warn('Web Share 失败:', error);
      //   // 失败后自动进入降级方案
      // }
    }
  }
  // 方案2: 降级使用 FileSaver
  else {
    // eslint-disable-next-line no-alert
    alert(`您的系统不支持共享这些文件`)
    // saveAs(imageFile, filename);
  }
}
</script>

<template>
  <button @click="share()">
    分享
  </button>
</template>
