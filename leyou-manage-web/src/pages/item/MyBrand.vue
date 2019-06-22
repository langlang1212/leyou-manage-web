<template>
  <div>
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
          ],
          brands : [],
          pagination : {},
          totalBrands : 0,
          loading : false,
        }
      },
      created(){
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
      }
    }
</script>

<style scoped>

</style>
