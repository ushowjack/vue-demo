<template>
    <el-table
            border
            :data="dataSource"
            @selection-change="handleSelectionChange">
        <!--选择-->
        <el-table-column
                v-if="hasSelection"
                type="selection"
                width="55">
        </el-table-column>
        <!--序号-->
        <el-table-column
                v-if="hasIndex"
                type="index"
                width="55">
        </el-table-column>
        <!--数据源-->
        <el-table-column v-for="(column, index) in columns"
                         v-if="column.isShow"
                         header-align="center"
                         :sortable="column.hasSort"
                         :key="column.prop"
                         :prop="column.prop"
                         :label="column.label">
        </el-table-column>
        <!--操作-->
        <slot name="handle-column">
        </slot>
    </el-table>
</template>

<script type="text/ecmascript-6">
    /*向父组件传递的数据：
     * commitSelection     被选中的数据
     *
     * */
    export default {
        name: 'tm-table',

        props: {
            //是否可以选择
            hasSelection: {
                type: Boolean,
                default: function () {
                    return false
                }
            },
            //是否有序列项
            hasIndex: {
                type: Boolean,
                default: function () {
                    return false
                }
            },
            // 这是相应的字段展示
            columns: {
                type: Array,
                default: function () {
                    return []
                }
            },
            // 这是数据源
            dataSource: {
                type: Array,
                default: function () {
                    return []
                }
            },

        },
        methods: {
            //将选中的行发送到父组件
            handleSelectionChange(val) {
                const selectionArr = [];
                val.forEach(function (el) {
                    selectionArr.push(el);
                });
                this.$emit('commitSelection', selectionArr);
            },
        }
    }
</script>

<style lang="less" rel="stylesheet/less" scoped>
    .el-table {
        width: 100%
    }
</style>