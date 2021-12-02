# 加载图片

仅仅只是演示加载效果，在图片加载的时候组件会自动显示加载的效果，`不推荐`直接修改 showLoadIng 属性，除非你很明确知道你在做什么！

```html
<n-button type="primary" @click="loadImg" style="margin-bottom:10px"
  >{{showLoadIng ? "完成加载" : "加载图片"}}</n-button
>
<n-space>
  <div style="margin-right: 10px">
    <n-tag type="success"> 默认样式 </n-tag>
    <div>
      <n-image
        width="100"
        src="https://07akioni.oss-cn-beijing.aliyuncs.com/07akioni.jpeg"
        :canPreview="false"
        ref="nImageRef1"
      ></n-image>
    </div>
  </div>
  <div>
    <n-tag type="success"> loading插槽样式 </n-tag>
    <div>
      <n-image
        width="200"
        src="https://07akioni.oss-cn-beijing.aliyuncs.com/07akioni.jpeg"
        :canPreview="false"
        ref="nImageRef2"
      >
        <template #loading>
          <n-progress type="circle" :percentage="percentage" />
        </template>
      </n-image>
    </div>
  </div>
</n-space>
```

```js
import { defineComponent, ref } from 'vue'

export default defineComponent({
  setup () {
    const nImageRef1 = ref(null)
    const nImageRef2 = ref(null)
    const percentage = ref(0)
    const TimeFun = ref(null)
    const showLoadIng = ref(false)
    return {
      loadImg () {
        nImageRef1.value.showLoadIng = !showLoadIng.value
        nImageRef2.value.showLoadIng = !showLoadIng.value
        showLoadIng.value = !showLoadIng.value
        if (showLoadIng.value) {
          TimeFun.value = setInterval(() => {
            percentage.value =
              percentage.value < 100 ? percentage.value + 1 : 100
          }, 1000)
        } else {
          clearInterval(TimeFun.value)
          percentage.value = 0
        }
      },
      nImageRef1,
      nImageRef2,
      percentage,
      showLoadIng
    }
  }
})
```