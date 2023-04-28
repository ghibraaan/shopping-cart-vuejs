<template>
  <div class="container-fluid p-5">
    <div class="row justify-content-between">
      <product-list
        :productList="produk"
        @emit-cart="addToCart"
        @emit-tambah="tambahJumlah"
        @emit-kurangi="kurangiJumlah"
      />

      <input-component @emit-submit="addList" />
    </div>
  </div>
</template>

<script>
export default {
  data: function () {
    return {
      produk: [],
    };
  },
  methods: {
    addList(inputid, inputnama, inputdesk, inputstock, inputharga) {
      let newProduk = {
        id: inputid,
        nama: inputnama,
        desk: inputdesk,
        stock: inputstock,
        harga: inputharga,
      };
      this.produk.push(newProduk);
    },
    addToCart(newCart) {
      let idToUpdate = newCart.cartId;
      let existingData = this.produk.find((item) => item.id === newCart.cartId);
      if (existingData.stock > 1) {
        this.produk.map((obj) => {
          if (obj.id === idToUpdate) {
            obj.stock -= 1;
          }
          return obj;
        });
      } else if ((existingData.stock = 1)) {
        this.produk.map((obj) => {
          if (obj.id === idToUpdate) {
            obj.stock -= 1;
          }
          return obj;
        });
        let index = this.produk.findIndex((obj) => obj.id === idToUpdate);
        if (index > -1) {
          this.produk.splice(index, 1);
        }
      }
    },
    tambahJumlah(barang) {
      let existingData = this.produk.find((item) => item.id === barang.cartId);
      if (existingData.id === barang.cartId) {
        this.produk.map((obj) => {
          if (obj.cartid === barang.cartId) {
            obj.stock -= 1;
          }
        });
      }
    },
    kurangiJumlah(barang) {
      let existingData = this.produk.find((item) => item.id === barang.cartId);
      if (existingData.id === barang.cartId) {
        this.produk.map((obj) => {
          if (obj.cartid === barang.cartId) {
            obj.stock += 1;
          }
        });
      }
    },
  },
  mounted() {
    console.log("Component mounted.");
  },
};
</script>

<style>
</style>