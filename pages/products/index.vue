<template>
  <main>
    <div class="container-fluid">
      <div class="row">
        <div class="col-sm-3"></div>
        <div class="col-sm-6">
          <div class="a-section">
            <div class="a-spacing-top-medium"></div>
            <h2 style="text-align: center">Add a new product</h2>
            <form action="">
              <div class="a-spacing-top-medium">
                <label for="">Category</label>
                <select class="a-select-option" v-model="categoryID">
                  <option
                    v-for="category in categories"
                    :value="category._id"
                    :key="category._id"
                  >
                    {{ category.type }}
                  </option>
                </select>
              </div>

              <div class="a-spacing-top-medium">
                <label for="">Owner</label>
                <select class="a-select-option" v-model="ownerID">
                  <option
                    v-for="owner in owners"
                    :value="owner._id"
                    :key="owner._id"
                  >
                    {{ owner.name }}
                  </option>
                </select>
              </div>

              <div class="a-spacing-top-medium">
                <label for="">Title</label>
                <input
                  type="text"
                  class="a-input-text"
                    v-model="title"
                  style="width: 100%"
                />
              </div>

              <div class="a-spacing-top-medium">
                <label for="">Price</label>
                <input
                  type="number"
                  class="a-input-text"
                  v-model="price"
                  style="width: 100%"
                />
              </div>

              <div class="a-spacing-top-medium">
                <label for="">Stock Quantity</label>
                <input
                  type="number"
                  class="a-input-text"
                  v-model="stockQuantity"
                  style="width: 100%"
                />
              </div>

              <div class="a-spacing-top-medium">
                <label for="">Description</label>
                <textarea
                  v-model="description"
                  rows="5"
                  placeholder="Provide details such as a product description"
                  style="width: 100%;resize:none"
                ></textarea>
              </div>

              <div class="a-spacing-top-medium">
                <label for="">Add Photo</label>
                <div class="a-row a-spacing-top-medium">
                  <label class="choosefile-button">
                    <i class="fal fa-plus"></i>
                    <input type="file" @change="onFileSelected"/>
                    <p style="margin-top: -70px">{{ fileName }}</p>
                  </label>
                </div>
              </div>
              <hr />
              <div class="a-spacing-top-large">
                <span class="a-button-register">
                  <span class="a-button-inner">
                    <span class="a-button-text" @click="onAddProduct">Add Product</span>
                  </span>
                </span>
              </div>
            </form>
          </div>
        </div>
        <div class="col-sm-3"></div>
      </div>
    </div>
  </main>
</template>

<script>
export default {
  async asyncData({ $axios }) {
    try {
      let categories = await $axios.$get("http://localhost:8080/api/categories");
      let owners = await $axios.$get("http://localhost:8080/api/owners");

      const [catResponse, ownerResponse] = await Promise.all([
        categories,
        owners,
      ]);

      console.log(catResponse, ownerResponse);

      return {
        categories: catResponse.categories,
        owners: ownerResponse.owners,
      };
    } catch (err) {
      console.log(err);
    }
  },
  data() {
    return {
      categoryID: null,
      ownerID: null,
      title: "",
      price: 0,
      description: "",
      selectedFile: null,
      fileName: "",
      stockQuantity: 1
    };
  },
  methods:  {
    onFileSelected(e) {
        this.selectedFile = e.target.files[0];
        this.fileName = e.target.files[0].name;
        console.log(this.selectedFile)
    },
    async onAddProduct() {
        let data = new FormData();
        data.append('title',this.title);
        data.append('price',this.price);
        data.append('description',this.description);
        data.append('stockQuantity',this.stockQuantity);
        data.append('ownerID',this.ownerID);
        data.append('categoryID',this.categoryID);
        data.append('photo',this.selectedFile, this.selectedFile.name);

        let result = await this.$axios.$post('http://localhost:8080/api/products', data);

        this.$router.push('/')
    }
  }
};
</script>

<style>
</style>