<template>
  <h3 class="mt-5">Shopping Cart</h3>
  <div class="card mt-3">
    <div class="table-responsive">
      <div class="card-body">
        <table class="table table-hover">
          <thead>
            <tr>
              <th scope="col">No</th>
              <th scope="col">Nama Produk</th>
              <th scope="col">Jumlah</th>
              <th scope="col">Harga</th>
              <th scope="col"></th>
            </tr>
          </thead>

          <tbody class="table-group-divider">
            <tr v-for="(barang, i) in cart" :key="i">
              <th scope="row">{{ i + 1 }}</th>
              <td>{{ barang.cartNama }}</td>
              <td>
                <span
                  ><button
                    class="btn btn-primary mr-3"
                    @click="kurangiJumlah(barang)"
                  >
                    -
                  </button></span
                >
                {{ barang.cartQty }}
                <span
                  ><button
                    class="btn btn-primary ml-3"
                    @click="tambahJumlah(barang)"
                  >
                    +
                  </button></span
                >
              </td>
              <td>{{ barang.cartHarga }}</td>
              <td>
                <button class="btn btn-danger">Delete</button>
              </td>
            </tr>
            <tr>
              <th scope="row" colspan="3">Total</th>
              <th scope="row">
                {{ totalHarga }}
              </th>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  emits: ["emit-kurangi", "emit-tambah"],
  props: {
    cart: {
      type: Array,
      default: () => {
        return [];
      },
    },
  },
  methods: {
    tambahJumlah(barang) {
      this.$emit("emit-tambah", barang);
    },
    kurangiJumlah(barang) {
      this.$emit("emit-kurangi", barang);
    },
  },
  computed: {
    totalHarga() {
      return this.cart.reduce(
        (accumulator, currentValue) => accumulator + currentValue.cartHarga,
        0
      );
    },
    // harga(barang) {
    //   return barang.cartHarga * barang.cartQty;
    // },
  },
};
</script>

<style>
</style>