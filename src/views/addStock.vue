<template>
  <div class="container page w-50 form-container">
    <form @submit.prevent="handleSubmit" style="padding: 30px 20px; width: 100%;">
      <div class="mb-3">
        <label>الرمز</label>
        <input
          v-model="symbol"
          placeholder="ادخل رمز الشركة"
          type="text"
          class="form-control"
          required
        />
      </div>
      <div class="mb-3">
        <label>اسم الشركة</label>
        <input
          v-model="company"
          placeholder="ادخل اسم الشركة"
          type="text"
          class="form-control"
          required
        />
      </div>
      <div class="mb-3">
        <label>عدد الاسهم</label>
        <input placeholder="ادخل عدد اسهم الشركة" v-model="count" type="text" class="form-control" required />
      </div>
      <div class="mb-3 form-check">
        <label>سعر السهم</label>
        <input placeholder="ادخل سعر السهم" v-model="price" type="text" class="form-control" required />
      </div>
      <div class="mb-3 form-check">
        <label>تكلفة السهم</label>
        <input placeholder="ادخل سعر تكلفة السهم" v-model="cost" type="text" class="form-control" required />
      </div>
      <button type="submit" class="btn btn-primary">Submit</button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      symbol: "",
      company: "",
      count: "",
      price: "",
      cost: "",
    };
  },

  methods: {
    handleSubmit() {
      let stockInfo = {
        symbol: this.symbol,
        company: this.company,
        count: this.count,
        price: this.price,
        cost: this.cost,
      };
      fetch("http://localhost:3000/stocks", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(stockInfo),
      }).then(() => {
        this.$router.push("/");
      });
    },
  },
};
</script>

<style scoped>


.form-control {
  border: none;
  border-bottom: 1px #ddd solid;
  box-shadow: none;
  background: none;
}

.form-control:focus {
  box-shadow: none;
}

.form-container{
  margin-top: 100px;
  background-color: rgb(253, 253, 253);
  border: 1px solid #ddd;
  box-shadow: 1px 10px 13px #ddd;
  
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
