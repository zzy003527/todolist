<template>
    <div id="group-List">
        <ul
            class="infinite-list"
            style="overflow: auto"
        >
            <li
                v-for="i in theList"
                :key="i.id"
                class="infinite-list-item"
            >
                <every-list :index="i.id">
                    <template #word>
                        {{ i.val }}
                    </template>
                </every-list>
            </li>
        </ul>
    </div>
</template>

<script lang="ts">
import { inject } from 'vue'

// 引入组件
import everyList from './everyList.vue'

export default {
    name: 'groupList',
    components: {
        everyList
    },
    setup() {
        // 列表数据
        let theList = inject('theList')

        return {
            theList
        }
    }
}
</script>
 
<style lang="less" scoped>
#groupList {
    width: 400px;
    height: 640px;
    background-color: red;
}

// 列表样式
.infinite-list {
    height: 550px;
    width: 610px;
    padding: 0;
    margin: 15px 0;
    list-style: none;
}
.infinite-list .infinite-list-item {
    display: flex;
    align-items: center;
    justify-content: center;
    height: 50px;
    background: var(--el-color-primary-light-9);
    margin: 10px;
    // width: 500px;
    white-space: pre-wrap;
    color: var(--el-color-primary);
}
.infinite-list .infinite-list-item + .list-item {
    margin-top: 10px;
}
</style>