<template>
  <div>
    <v-layout class="px-3 pb-2">
      <v-flex xs2>
        <v-btn @click="addBrand" color="info" small>新增品牌</v-btn>
      </v-flex>
      <v-spacer/>
      <v-flex xs4>
        <v-text-field label="搜索" hide-details append-icon="search" v-model="key"/>
      </v-flex>
    </v-layout>
    <v-data-table
      :headers="headers"
      :items="brands"
      :pagination.sync="pagination"
      :total-items="totalBrands"
      :loading="loading"
      class="elevation-1"
    >
      <template slot="items" slot-scope="props">
        <td class="text-xs-center">{{ props.item.id }}</td>
        <td class="text-xs-center">{{ props.item.name }}</td>
        <td class="text-xs-center"><img v-if="props.item.image" :src="props.item.image" width="130" height="40"/></td>
        <td class="text-xs-center">{{ props.item.letter }}</td>
        <td class="text-xs-center">
          <v-btn flat icon color="info">
            <v-icon>edit</v-icon>
          </v-btn>
          <v-btn flat icon color="error">
            <v-icon>delete</v-icon>
          </v-btn>
        </td>
      </template>
    </v-data-table>
  </div>
</template>

<script>
    export default {
      name: "MyBrand",
      data(){
        return {
          headers : [
            {text: "品牌id",value: "id",align: "center",sortable: "true"},
            {text: "品牌名称",value: "name",align: "center",sortable: "false"},
            {text: "品牌LOGO",value: "image",align: "center",sortable: "false"},
            {text: "品牌首字母",value: "letter",align: "center",sortable: "true"},
            {text: "操作",align: "center",sortable: false}
          ],
          brands : [],
          pagination : {},
          totalBrands : 0,
          loading : false,
          key : "",
          show: false,
        }
      },
      created(){  //加载页面的时候执行
        this.brands = [
          {
            id: 2032,
            name: "OPPO",
            image: "1.jpg",
            letter: "O"
          },
          {
            id: 2033,
            name: "飞利浦（PHILIPS）",
            image: "2.jpg",
            letter: "F"
          },
          {
            id: 2034,
            name: "华为（HUAWEI）",
            image: "3.jpg",
            letter: "H"
          },
          {
            id: 2036,
            name:"酷派（Coolpad）",
            image: "4.jpg",
            letter: "K"
          },
          {
            id: 2037,
            name: "魅族（MEIZU）",
            image: "5.jpg",
            letter: "M"
          }
        ];
        this.totalBrands = 15;

        //去后台查询
        this.loadBrands();
      },
      watch: {  //监控空间变化取值 如  input
        key(){
          this.pagination.page = 1;
          this.loadBrands();
        },
        pagination: {
          deep : true,
          handler(){
            this.loadBrands();
          }
        }
      },
      methods: {
        addBrand() {
          this.brand = {};
          this.isEdit = false;
          this.show = true;
        },
        loadBrands(){
          this.loading = true;
          this.$http.get("/item/brand/page",{
            params: {
              //搜索条件
              page: this.pagination.page,  //当前页
              rows: this.pagination.rowsPerPage, //每页大小
              sortBy: this.pagination.sortBy,  //排序字段
              desc : this.pagination.descending, //是否降序
              key: this.key,
            }
          }).then(resp => {
            this.brands = resp.data.items;
            this.totalBrands = resp.data.total;
            this.loading = false;
          });
        }
      }
    }
</script>

<style scoped>

</style>
