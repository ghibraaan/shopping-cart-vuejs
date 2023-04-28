<template>
  <div class="col-xl-9">
    <h3>Daftar Produk</h3>
    <div class="card mt-3">
      <div class="table-responsive">
        <div class="card-body">
          <table class="table table-hover">
            <thead>
              <tr>
                <th scope="col">No</th>
                <th scope="col">Nama Produk</th>
                <th scope="col">Deskripsi</th>
                <th scope="col">Stock</th>
                <th scope="col">Harga</th>
                <th scope="col"></th>
              </tr>
            </thead>

            <tbody class="table-group-divider">
              <tr v-for="(item, i) in productList" :key="i">
                <th scope="row">{{ i + 1 }}</th>
                <td>{{ item.nama }}</td>
                <td>{{ item.desk }}</td>
                <td>{{ item.stock }}</td>
                <td>{{ item.harga }}</td>
                <td>
                  <button
                    class="btn btn-primary"
                    type="button"
                    @click="addToCart(item)"
                  >
                    Add to cart
                  </button>
                </td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>

    <cart-component
      :cart="cartList"
      @emit-tambah="tambahJumlah"
      @emit-kurangi="kurangiJumlah"
    />
  </div>
</template>

<script>
export default {
  emits: ["emit-cart", "emit-tambah", "emit-kurangi"],
  props: {
    productList: {
      type: Array,
      default: () => {
        return [];
      },
    },
  },
  data: function () {
    return {
      cartList: [],
    };
  },
  methods: {
    addToCart(item, i) {
      let newCart = {
        cartId: item.id,
        cartNama: item.nama,
        cartQty: 1,
        cartHarga: item.harga,
      };
      this.$emit("emit-cart", newCart, i);
      // this.cartList.push(newCart);
      let existingData = this.cartList.find(
        (item) => item.cartId === newCart.cartId
      );
      if (!existingData) {
        this.cartList.push(newCart);
        this.console.log("Data bisa diinput");
      } else {
        this.cartList.map((obj) => {
          if (obj.cartId === newCart.cartId) {
            obj.cartQty += 1;
            obj.cartHarga += barang.cartHarga;
          }
          return obj;
        });
      }
    },
    tambahJumlah(barang) {
      this.$emit("emit-tambah", barang);
      let existingData = this.cartList.find(
        (item) => item.cartId === barang.cartId
      );
      if (existingData.cartId === barang.cartId) {
        this.cartList.map((obj) => {
          if (obj.cartId === barang.cartId) {
            obj.cartQty += 1;
            obj.cartHarga += barang.cartHarga;
          }
        });
      }
    },
    kurangiJumlah(barang) {
      this.$emit("emit-kurangi", barang);
      let existingData = this.cartList.find(
        (item) => item.cartId === barang.cartId
      );
      if (existingData.cartId === barang.cartId) {
        this.cartList.map((obj) => {
          if (obj.cartId === barang.cartId) {
            obj.cartQty -= 1;
            obj.cartHarga -= barang.cartHarga;
          }
        });
      }
    },
  },
};
</script>

<style>
</style>