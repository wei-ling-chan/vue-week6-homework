<template>
  <h1>產品列表</h1>
  <div class="container">
      <div class="row row-cols-1 row-cols-lg-4 g-3" ><!--row決定內層的數量，row-cols-1為手機內層數量，row-cols-lg-4為電腦內層數量，g-3為卡片之間的距離-->
        <!-- 內層不定義寬度 -->
        <div class="col" v-for="product in products" :key="product.id">
          <div class="card h-100"> <!--卡片高度100-->
            <img :src="product.imageUrl" class="card-img-top" alt="...">
            <div class="card-body">
              <h5 class="card-title">{{product.title}}</h5>
              <p class="card-text">{{product.description}}</p>
              <router-link :to="`/product/${product.id}`" class="btn btn-primary">Go somewhere</router-link>
            </div>
          </div>
        </div>
      </div>
    </div>
</template>
<script>
export default {
  data () {
    return {
      products: []
    }
  },
  methods: {
    getProducts () {
      // console.log(process.env.VUE_APP_API, process.env.VUE_APP_PATH)
      this.$http(`${process.env.VUE_APP_API}api/${process.env.VUE_APP_PATH}/products/all`)
        .then(res => {
          // console.log(res)
          this.products = res.data.products
        })
    }
  },
  mounted () {
    this.getProducts()
  }
}
</script>
