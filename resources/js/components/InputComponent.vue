<template>
  <div class="col-xl-3">
    <h3>Input Data Produk</h3>
    <div class="mt-3">
      <div class="input-group mb-3">
        <input
          type="text"
          class="form-control"
          v-model="inputid"
          placeholder="ID Produk"
        />
      </div>
      <div class="input-group mb-3">
        <input
          type="text"
          class="form-control"
          v-model="inputnama"
          placeholder="Nama Produk"
        />
      </div>
      <div class="input-group mb-3">
        <input
          type="text"
          class="form-control"
          v-model="inputdesk"
          placeholder="Deskripsi"
        />
      </div>
      <div class="input-group mb-3">
        <input
          type="text"
          class="form-control"
          v-model.number="inputstock"
          placeholder="Jumlah Stok"
        />
      </div>
      <div class="input-group mb-3">
        <input
          type="text"
          class="form-control"
          v-model.number="inputharga"
          placeholder="Harga"
        />
      </div>
      <button class="btn btn-primary" @click="addList">Submit</button>
    </div>
  </div>
</template>

<script>
export default {
  emits: ["emit-submit"],
  data: function () {
    return {
      inputid: "",
      inputnama: "",
      inputdesk: "",
      inputstock: "",
      inputharga: "",
    };
  },
  methods: {
    addList() {
      this.$emit(
        "emit-submit",
        this.inputid,
        this.inputnama,
        this.inputdesk,
        this.inputstock,
        this.inputharga
      );
      this.reset();
    },
    reset() {
      this.inputid = "";
      this.inputnama = "";
      this.inputdesk = "";
      this.inputstock = "";
      this.inputharga = "";
    },
  },
};
</script>

<style>
</style>