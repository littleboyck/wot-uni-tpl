<!-- eslint-disable antfu/top-level-function -->
<script setup lang="ts">
import VueOfficeExcel from '@vue-office/excel'
// 引入相关样式
import('@vue-office/excel/lib/index.css')

definePage({
  name: 'doc',
  style: {
    navigationBarTitleText: '文档预览',
    navigationStyle: 'custom',
  },
})
const excel = 'https://501351981.github.io/vue-office/examples/dist/static/test-files/test.xlsx'
const options = ref({
  width: '100%',
  height: '100%',
  page: 1,
  pageCount: 1,
  pageSize: 1,
  pageIndex: 1,
  pageTotal: 1,
  pageNumber: 1,
})

// eslint-disable-next-line unused-imports/no-unused-vars
const renderedHandler = (data: any) => {
  console.log('渲染完成')
}

const errorHandler = (error: any) => {
  console.log('渲染失败', error)
}
</script>

<template>
  <vue-office-excel
    :src="excel"
    :options="options"
    style="width: 100vw;height: 100dvh;"
    @rendered="renderedHandler"
    @error="errorHandler"
  />
</template>
