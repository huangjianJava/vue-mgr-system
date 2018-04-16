<template>
    <div class="table">
        <div class="crumbs">
            <el-breadcrumb separator="/">
                <el-breadcrumb-item>we-chart表格</el-breadcrumb-item>
            </el-breadcrumb>
        </div>
        <div class="container">
            <!--<div class="handle-box">-->
                <!--<el-button type="primary" icon="delete" class="handle-del mr10" @click="delAll">批量删除</el-button>-->
                <!--<el-select v-model="select_cate" placeholder="筛选省份" class="handle-select mr10">-->
                    <!--<el-option key="1" label="广东省" value="广东省"></el-option>-->
                    <!--<el-option key="2" label="湖南省" value="湖南省"></el-option>-->
                <!--</el-select>-->
                <!--<el-input v-model="select_word" placeholder="筛选关键词" class="handle-input mr10"></el-input>-->
                <!--<el-button type="primary" icon="search" @click="search">搜索</el-button>-->
            <!--</div>-->

            <el-table :data="tableData" border style="width: 100%" ref="multipleTable" @selection-change="handleSelectionChange">
                <el-table-column type="selection" width="55"></el-table-column>
                <el-table-column prop="createDate" label="创建时间" sortable width="150">
                </el-table-column>
                <el-table-column prop="account" label="账号" width="120">
                </el-table-column>
                <el-table-column prop="name" label="姓名">
                </el-table-column>
                <el-table-column prop="age" label="年龄">
                </el-table-column>
                <el-table-column prop="sexType" label="性别">
                </el-table-column>
                <!--<el-table-column label="操作" width="180">-->
                    <!--<template slot-scope="scope">-->
                        <!--<el-button size="small"-->
                                <!--@click="handleEdit(scope.$index, scope.row)">编辑</el-button>-->
                        <!--<el-button size="small" type="danger"-->
                                <!--@click="handleDelete(scope.$index, scope.row)">删除</el-button>-->
                    <!--</template>-->
                <!--</el-table-column>-->
            </el-table>

            <div class="pagination">
                <el-pagination
                        @current-change ="handleCurrentChange"
                        layout="prev, pager, next"
                        v-bind:page-size="size"
                        v-bind:total="totalCount">
                </el-pagination>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                page: 1,
                size: 2,
                totalCount:0,
                tableData: []
            }
        },
        created(){
            this.getData();
        },
        methods: {
            getData(){
                this.$axios.get('/my/vue/we-chart/page-info',{
                    params:{page:this.page,size:this.size}}).then((res) => {
                    this.totalCount = res.data.data.total;
                    console.log("totalCount:" + this.totalCount)
                    this.tableData = res.data.data.list;
                })
            },
            handleCurrentChange(val){// 分页导航
                this.page = val;
                this.getData();
            },
            handleSelectionChange(val) {
                this.multipleSelection = val;
            }
        }
    }
</script>

<style scoped>
.handle-box{
    margin-bottom: 20px;
}
.handle-select{
    width: 120px;
}
.handle-input{
    width: 300px;
    display: inline-block;
}
</style>
