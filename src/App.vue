<template>
    <div id="app">
        <div class="common-layout">
            <el-container>
                <el-header>
                <!-- 头部标题 -->
                    <div class="title">
                        <div class="todolist-title">{{ title }}</div>
                    </div>
                </el-header>
                <el-main>
                <!-- 下方输入框和显示 -->
                    <addInput></addInput>
                    <groupList></groupList>
                </el-main>
            </el-container>
        </div>
    </div>

</template>





<script lang="ts" setup>
import { ref, reactive, provide } from 'vue'

// 引入组件
import groupList from './components/groupList.vue'
import addInput from './components/addInput.vue'

// export default {
    // name: 'app',
    // components: {
        // groupList,
        // addInput
    // },
    // setup() {
        // 数据
        let title = ref('TODO-LIST')
        const theList = reactive([
            { val: '睡觉', id: Symbol() },
            { val: '学习', id: Symbol() },
            { val: '吃饭', id: Symbol() },
            { val: '学车', id: Symbol() }
        ])

        provide('theList', theList)
        // return {
            // title,
            // theList
        // }
    // }
// }
</script>

<style lang="less">
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;

    width: 700px;
    height: 700px;
    margin: 0 auto;
    box-shadow: #999 0px 0px 5px 2px;
    // background-color: pink;
}

.title {
    width: 700px;
    height: 60px;
}
.todolist-title {
    font-size: 25px;
    font-weight: 900;
    display: inline-block;
    margin: 10px auto;
}
</style>
