<template>
  <section style="padding: 0; margin-top: 75px; " class="container-fluid page contain">
   <table v-if="stockInfo.length" class="table table-striped table-hover border-danger ">
    <thead style="background: #00a876">
      <tr style="border-radius: 41px !important;" >
        <th class="p-3" >تحكم</th>
        <th class="p-3" >#</th>
        <th class="p-3"  scope="col">رمز السهم</th>
        <th class="p-3"  scope="col">الشركة</th>
        <th class="p-3"  scope="col">عدد الاسهم</th>
        <th class="p-3"  scope="col">سعر السهم</th>
        <th class="p-3"  scope="col">تكلفة السهم</th>
        <th class="p-3"  scope="col">اجمالي القيمة</th>
        <th class="p-3"  scope="col">اجمالي التكلفة</th>
        <th class="p-3"  scope="col">التغير</th>
        <th class="p-3"  scope="col">نسبة التغير</th>
      </tr>
    </thead>
    
     <tbody  v-for="stock in stockInfo" :key="stock.id" >
        <TableBody :stock="stock" @t="t" :stockInfo="stockInfo"  @delete="handleDelete" />
      </tbody>

  </table>
   
   <h2 style="width: 100%; height: 95%; color: #ddd" class="d-flex justify-content-center align-items-center" v-else>البيانات غير متوفرة</h2>
  </section>


</template>

<script>
import addStock from "../components/addStock";
import TableBody from "../components/TableBody";

export default {
  name: "HomeView",
  components: { addStock, TableBody },
  data() {
    return {
      stockInfo: [],
    };
  },
  mounted() {
    fetch("http://localhost:3000/stocks")
      .then((res) => res.json())
      .then((data) => (this.stockInfo = data))
      .catch((err) => console.log(err));
  },
  methods: {
    handleDelete(id) {
      this.stockInfo = this.stockInfo.filter((stock) =>{
        return stock.id !== id
      });
    }
  }
};
</script>


<style>



.contain{
  width: 90vw !important;
 border-radius: 11px !important;
 overflow: hidden;
}



@-webkit-keyframes fade {
  0%   { opacity: 0; }
  100% { opacity: 1; }
}
@-moz-keyframes fade {
  0%   { opacity: 0; }
  100% { opacity: 1; }
}
@-o-keyframes fade {
  0%   { opacity: 0; }
  100% { opacity: 1; }
}
@keyframes fade {
  0%   { opacity: 0; }
  100% { opacity: 1; }
}

.page {
 animation-name: fade;
 animation-duration: 1s; 
 animation-fill-mode: forwards; 
}

</style>