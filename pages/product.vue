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
                <select name="" class="a-select-option" id="">
                  <option v-for="category in categories" :value="category._id" :key="category._id">{{category.type}}</option>
                </select>
              </div>

              <div class="a-spacing-top-medium">
                <label for="">Owner</label>
                <select name="" class="a-select-option" id="">
                  <option v-for="owner in owners" :value="owner._id" :key="owner._id">{{owner.name}}</option>
                </select>
              </div>

              <div class="a-spacing-top-medium">
                <label for="">Title</label>
                <input
                  type="text"
                  class="a-input-text"
                  name=""
                  id=""
                  style="width: 100%"
                />
              </div>

              <div class="a-spacing-top-medium">
                <label for="">Price</label>
                <input
                  type="number"
                  class="a-input-text"
                  name=""
                  id=""
                  style="width: 100%"
                />
              </div>

              <div class="a-spacing-top-medium">
                <label for="">Description</label>
                <textarea
                  name=""
                  id=""
                  cols="30"
                  rows="10"
                  placeholder="Provide details such as a product description"
                  style="width: 100%"
                ></textarea>
              </div>

              <div class="a-spacing-top-medium">
                <label for="">Add Photo</label>
                <div class="a-row a-spacing-top-medium">
                  <label for="" class="choosefile-button">
                    <i class="fal fa-plus"></i>
                    <input type="file" />
                    <p style="margin-top: -70px">name</p>
                  </label>
                </div>
              </div>
              <hr />
              <div class="a-spacing-top-large">
                <span class="a-button-register">
                  <span class="a-button-inner">
                    <span class="a-button-text">Add Product</span>
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
      let categories = $axios.$get("http://localhost:3000/api/categories");
      let owners = $axios.$get("http://localhost:3000/api/owners");

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
};
</script>

<style>
</style>