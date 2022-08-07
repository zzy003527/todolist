<template>
    <div class="everyList">
        <div class="theWord">
            <slot name="word"></slot>
        </div>
        <div class="bottons">
            <el-button
                type="warning"
                @click="configOpen"
            >修改</el-button>
            <el-button
                type="danger"
                @click="deleteOpen"
            >删除</el-button>
            <el-button
                type="success"
                v-if="successShow"
                @click="changeSuccess"
            >设为完成</el-button>
            <el-tag
                class="successTag"
                type="success"
                v-if="!successShow"
            >已完成</el-tag>
        </div>
    </div>
</template>

<script lang="ts">
import { ref, inject } from 'vue'
import { ElMessage, ElMessageBox } from 'element-plus'

// 数据类型接口
interface everyEvent {
    val: string
    id: symbol
}
interface theProps {
    index: symbol
}

export default {
name: 'everyList',
props: {
    index: Symbol
},
setup(props: theProps) {
// 控制success按钮
let successShow = ref(true)
function changeSuccess() {
    successShow.value = !successShow.value
}
// 列表数据
let theList: everyEvent[] = inject('theList') as everyEvent[]

// 找出当前项数据在数组中的下标
function IndexInList(index: symbol): number {
    let it = -1
    theList.map(eve => {
        if (eve.id === index) {
            it = theList.indexOf(eve)
            return it
        }
    })
    return it
}

// 点击修改按钮弹出框
// 创建正则表达式(至少一个汉字、数字、字母、下划线)
const reg = new RegExp('[a-zA-Z0-9_\u4e00-\u9fa5]+')
const configOpen = () => {
    ElMessageBox.prompt('请输入修改的内容', '修改', {
        confirmButtonText: 'OK',
        cancelButtonText: 'Cancel',
        inputPattern: reg,
        inputErrorMessage: '请至少输入一个符号'
    })
        .then(({ value }) => {
            theList[IndexInList(props.index as symbol)].val = value
            ElMessage({
                type: 'success',
                message: `修改成功，内容为 : ${value}`
            })
        })
        .catch(() => {
            ElMessage({
                type: 'info',
                message: '取消修改'
            })
        })
}

// 删除弹出框设置
const deleteOpen = () => {
    ElMessageBox.confirm('是否确认进行删除操作?', '注意', {
        confirmButtonText: 'OK',
        cancelButtonText: 'Cancel',
        type: 'warning'
    })
        .then(() => {
            theList.splice(IndexInList(props.index as symbol), 1)
            ElMessage({
                type: 'success',
                message: '删除成功'
            })
        })
        .catch(() => {
            ElMessage({
                type: 'info',
                message: '取消删除'
            })
        })
}

return {
    successShow,
    changeSuccess,
    theList,
    IndexInList,
    configOpen,
    deleteOpen
}
}
}
</script>

<style lang="less" scoped>
.theWord {
    position: relative;
    left: -110px;
    top: 15px;
    text-align: right;
    display: inline-block;
}
.bottons {
    position: relative;
    right: -160px;
    bottom: 8px;
}

.successTag {
    margin: 0 22px;
}
</style>