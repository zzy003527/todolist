<template>
    <div class="addInput">
        <el-input
            v-model="inputValue"
            placeholder="请输入要添加的事件"
            size="large"
            class="input"
        />
        <el-button
            type="primary"
            round
            @click="listAdd"
        >添加</el-button>
    </div>
</template>
 
<script lang="ts">
import { ref, inject } from 'vue'

// 数据类型接口
interface everyEvent {
    val: string
    id: symbol
}

export default {
    name: 'addInput',
    setup() {
        // 列表数据
        let theList: everyEvent[] = inject('theList') as everyEvent[]
        // 获取input数据
        const inputValue = ref('')

        // 判断input数据是否存在于列表数据中
        function inputInList(val: string) {
            theList.forEach(item => {
                if (val === item.val) {
                    return true
                }
            })
            return false
        }

        // 创建正则表达式(至少一个汉字、数字、字母、下划线)
        const reg = new RegExp('[a-zA-Z0-9_\u4e00-\u9fa5]+')

        function listAdd() {
            // 判断input是否为空
            if (reg.test(inputValue.value)) {
                // 把新数据填入数组
                theList.unshift({ val: inputValue.value, id: Symbol() })
            }
            // 清空input
            inputValue.value = ''
        }

        return {
            theList,
            inputValue,
            inputInList,
            listAdd
        }
    }
}
</script>

<style lang="less" scoped>
.input {
    float: left;
    margin-left: 10px;
    width: 400px;
}
</style>