<!--
TypeScript 与组合式 API
-->
<script lang="ts" setup>
import { key } from '../types/app'
import { computed, onMounted, provide, reactive, ref, useTemplateRef } from 'vue'



// 3.为 ref() 标注类型
const age = ref<number>(21)
const gender = ref<'L' | 'G' | 'B' | 'T'>('T')

// 4.为 reactive() 标注类型
interface Book {
  title: string
  year?: number
}
const book: Book = reactive({ title: 'Vue 3 指引' })

// 5.为 computed() 标注类型【computed() 会自动从其计算函数的返回值上推导出类型，一般不用标注】
const count = ref(0)
// 推导得到的类型：ComputedRef<number>
const double = computed(() => count.value * 2)
// => TS Error: Property 'split' does not exist on type 'number'
// const result = double.value.split('')

// 6.为 provide / inject 标注类型
provide(key, 'foo') // 若提供的是非字符串值会导致错误

// 7.为模板引用标注类型



const handleChange = (v: number) => {
  count.value = v
}
</script>

<template>
  <div>
    <TypeDemo2 ref="demo2" name="w4ng" @change="handleChange" />
    <section>
      <div>count: {{ count }}</div>
      <div>double: {{ double }}</div>
    </section>
  </div>
</template>
