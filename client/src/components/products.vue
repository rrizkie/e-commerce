<template>
  <div class="container">
    <div class="card"  v-for="product in products" :key="product.id">
          <div class="card-content">
            <div class="top-bar">
              <span>
              Rp. {{ new Number(product.price).toLocaleString("id-ID") }}
              </span>
              <span class="float-right lnr lnr-heart"></span>
            </div>
            <div class="img">
              <img
                :src="product.image_url"
              />
            </div>
          </div>
          <div class="card-description">
            <div class="title">
              {{product.name}}
            </div>
            <div class="cart">
              <span class="lnr lnr-cart"></span>
            </div>
          </div>
          <div class="card-footer">
            <div class="span" @click.prevent="addCart(product.id)">
              <i class="fas fa-cart-plus"></i>
              Stock : {{product.stock}}
            </div>
          </div>
        </div>
  </div>
</template>

<script>
export default {
  name: 'Products',
  computed: {
    products () {
      return this.$store.state.products
    }
  },
  methods: {
    fetchData () {
      return this.$store.dispatch('fetchProducts')
    },
    addCart (productId) {
      if(!localStorage.getItem('access_token')){
        this.$router.push('/login')
      }else{
        return this.$store.dispatch('addCart', productId)
      }
    }
  },
  created () {
    this.fetchData()
  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
html,
body {
  font-family: "Kanit", sans-serif;
  min-height: 100vh;
  min-width: 100vw;
  background: #fcfcfc;
}
.header {
  z-index: 99999;
  width: 100%;
  height: 70px;
  background: white;
  position: fixed;
  top: 0;
  left: 0;
  box-shadow: 0px 2px 40px 0px rgba(0, 0, 0, 0.091);
  display: flex;
  justify-content: center;
  align-items: center;
  color: #cacaca;
  font-weight: 100;
  text-transform: uppercase;
  letter-spacing: 0.3em;
}
.body {
  height: 100vh;
  width: 100%;
  padding-top: 50px;
}
.container {
  padding-top: 20px;
  min-height: 100vh;
  display: grid;
  grid-auto-rows: 400px;
  grid-gap: 30px;
  grid-template-columns: repeat(3, minmax(200px, 300px));
  justify-content: center;
  align-items: stretch;
  @media screen and (max-width: 720px) {
    grid-template-columns: 1fr;
    margin: 50px 30px;
  }
}

.card {
  position: relative;
  padding: 10px;
  background: white;
  display: grid;
  grid-template-rows: 8fr 1fr 1fr;
  box-shadow: 0px 15px 20px 0px rgba(0, 0, 0, 0.057);
  transition: 0.2s ease-in;

  .card-content {
    .top-bar {
      width: calc(100% - 40px);
      position: absolute;
      top: 0;
      left: 0;
      padding: 20px;
      .float-right {
        float: right;
      }
    }
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100%;
    .img {
      width: 100%;
      justify-content: bottom;
      align-content: bottom;
      text-align: center;
      img {
        max-width: 100%;
        max-height: 220px;
      }
    }
  }
  .card-description {
    padding: 10px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    font-weight: 400;
    font-size: 14px;
    letter-spacing: 0.1em;
    width: calc(100%-20px);
    .title {
      text-transform: uppercase;
      text-align: left;
    }
    .cart {
      float: right;
      cursor: pointer;
    }
  }
  .card-footer {
    text-transform: uppercase;
    padding: 0.3em;
    border-top: 0.5px solid #ececec;
    letter-spacing: 0.1em;
    font-size: 11px;
    color: white;
    justify-items: left;
    align-items: center;
    display: flex;
    .span {
      margin: 5px;
      width: auto;
      background: black;
      padding: 6px 9px;
      border-radius: 2px;
      font-weight: 100;
      cursor: pointer;
      &:hover {
        background: #aaaaaa;
      }
    }
  }
  &:hover {
    transition: 0.2s ease-in;
    transform: translateY(-10px);
    box-shadow: 0px 45px 60px 0px rgba(0, 0, 0, 0.087);
  }
}
</style>
