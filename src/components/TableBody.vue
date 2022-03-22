<template>
      <tr  :class="{highlight: light}">
        <td style="margin: 0 !important"><i @click="delStock" class="bi bi-x-lg"></i>
        <i @click="highlight" class="bi bi-brightness-high"></i>
        </td>
        <td>{{ stock.id }}</td>
        <td>{{ stock.symbol }}</td>
        <td>{{ stock.company }}</td>
        <td>{{ stock.count }}</td>
        <td :class="[{danger: stock.price < 0}, {success: stock.price > 0} ]">{{ stock.price }}</td>
        <td>{{ stock.cost }}</td>
        <td ref="totalPrice">{{ totalPrice }}</td>
        <td ref="totalCost">{{ totalCost }}</td>
        <td ref="stockChange">{{ stockChange }}</td>
        <td ref="stockChangePer">
          %{{
             stockChangePer
          }}
        </td>
        
      </tr>
</template>

<script>
export default {
     props: ["stock", "stockInfo"],
  data() {
    return {
       uri: "http://localhost:3000/stocks/" + this.stock.id,
      light: false,
     
    };
  },
  methods:{
   delStock() {
     fetch(this.uri, { method: "DELETE"})
     .then(() => this.$emit("delete", this.stock.id))
     .catch((err) => console.log(err))
   },
   highlight(){
     this.light = !this.light
     console.log("highlight", this.light)
   },
  //  I STOPPED HERE
  postTotals() {
     fetch(this.uri, {
      method: "POST",
      headers: { "Content-Type": "application/json "},
      body: JSON.stringify({ })
     
     })
   } 
  },
  computed: {
    totalPrice() {
    let totalPrice =  this.stock.count * this.stock.price
    return totalPrice;
    },
    totalCost(){
      let totalCost = this.stock.count * this.stock.cost
      return totalCost
    },
    stockChange() {
      let stockChange = this.stock.count * this.stock.price - this.stock.count * this.stock.cost
      return stockChange
    },
    stockChangePer(){
      let ChangePer =  ((this.stock.count * this.stock.price - this.stock.count * this.stock.cost) /
              (this.stock.count * this.stock.price)).toFixed(5) *
            100;
            return ChangePer;
    }
  }
 };

</script>

<style>
.bi{
  user-select: none;
  cursor: pointer;
  ;
}

.bi-x-lg{
  color: crimson;
}

.bi-brightness-high{
  color: rgb(0, 140, 255);
}

i{
  margin: 6px !important
}

.danger{
  color: red;
}
.success{
  color: #42b983;
}

.highlight{ 
  background: rgb(0, 140, 255);
}
</style>