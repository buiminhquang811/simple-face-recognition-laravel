<template>
  <div class="container">
    <br />
    <div class="row justify-content-center">
      <div
        class="col-md-6 offset-md-3"
        style="
          margin: auto;
          background: white;
          padding: 20px;
          box-shadow: 10px 10px 5px #888;
        "
      >
        <div class="panel-heading">
          <h2>Nhận diện khuôn mặt - Laravel</h2>
          <p style="font-style: italic">Bùi Minh Quang - 201920425</p>
        </div>
        <hr />
        <form
          ref="form"
          @submit.prevent="onSubmit"
          method="post"
          enctype="multipart/form-data"
        >
          <!-- Product name:
          <br />
          <input type="text" placeholder="Name" name="name" />
          <br />
          Description:
          <br />
          <input type="text" placeholder="description" name="description" />
          <br />
          Price:
          <br />
          <input type="number" placeholder="price" name="price" />

          <br />
          <br />
          Product photos (can attach more than one):
          <br /> -->
          <input type="file" name="photos[]" multiple class="form-control" />
          <br />
          <input
            type="submit"
            value="Analyse Image"
            style="border-radius: 0px"
            class="btn btn-lg btn-block btn-outline-success"
          />
        </form>
      </div>
      <!-- <div class="col-md-8">
        <div class="card card-default">
          <div class="card-header">Face</div>

          <div class="card-body">
            
          </div>
        </div>
      </div> -->
    </div>
    <div style="" v-for="(item, index) in items" :key="index">
      {{ item.name }}
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      items: [],
    };
  },
  mounted() {
    axios.get("/api/items").then((response) => {
      this.items = response.data();
    });
  },
  methods: {
    onSubmit() {
      var vm = this;
      var formdata = new FormData(vm.$refs.form);
      axios.post("api/items", formdata).then(function (response) {
        console.log(formdata);
        console.log(response.data);
      });
    },
  },
};
</script>
 <!-- <div v-for="image in item.item_image_colors">{{ image.color }},</div>
      <img
        style="height: 150px"
        v-for="img in item.item_images"
        :src="img.path"
        alt=""
      /> -->