<template  >
<div  class="bg-image d-flex justify-content-center align-items-center"
     style="
            background-image: url('https://images7.alphacoders.com/992/thumb-1920-992404.jpg');
            height: 100%
            
            
            
            " >
  <v-container >
    
    <center><h1 class="text-info">Product Page</h1></center>
    <v-container class="d-flex flex-wrap">
      <v-card
        class="mx-auto mb-5"
        max-width="400"
        v-for="(i, index) in productlist"
        :key="index"
      >
        <v-img class="white--text align-end" height="200px" :src="i.imageurl">
          <v-card-title>{{ i.name }}</v-card-title>
        </v-img>

        <v-card-subtitle class="pb-0 ">{{ i.rightText }}</v-card-subtitle>

        <v-card-text class="text--primary">
          <div>{{ i.leftText }}</div>
        </v-card-text>

        <v-card-actions>
          <v-btn  color="info" text :to="'/detail/' + i.name">detail</v-btn>
          <v-btn color="orange" text @click="selected(i)"> Add </v-btn>
         
        </v-card-actions>
      </v-card>
    </v-container>

    <table class="table table-striped table-hover">        
    
    </table>
    <v-container
      ><h4 class="text-danger fs-1">ยอดชำระเงิน  {{ total() }} บาท</h4></v-container
    >
    <v-container grid-list-xs class="success">
      <router-view :key="$route.path"></router-view>
    </v-container>
  </v-container>
  </div>
</template>

<script>
export default {
  data() {
    return {
        productlist: [
        {
         
          name: "nike air max (white&black)",
          imageurl:
            "https://static.nike.com/a/images/c_limit,w_592,f_auto/t_product_v1/19748bd0-5a80-4583-9c3f-e29a24044a58/%E0%B8%A3%E0%B8%AD%E0%B8%87%E0%B9%80%E0%B8%97%E0%B9%89%E0%B8%B2%E0%B8%81%E0%B8%AD%E0%B8%A5%E0%B9%8C%E0%B8%9F-air-max-270-g-Z6vCfs.png",
          rightText: "price : 199",
          leftText: "Size : EU 31-45",
          producturl: "https://www.nike.com/th/t/%E0%B8%A3%E0%B8%AD%E0%B8%87%E0%B9%80%E0%B8%97%E0%B9%89%E0%B8%B2%E0%B8%9C%E0%B8%B9%E0%B9%89-air-max-270-V4DfZQ/AH6789-001?cp=32538102380_search_%7cth%7cTH+-+Smart+Shopping+-+Brand%7cSmart+Shopping+-+Brand+-+All+Products%7cGOOGLE&gclid=CjwKCAiA6seQBhAfEiwAvPqu1z-YHWaZUDrFhiJFc0U3mG3VZzJid6LH10h1BbcRIUEqCXsLGEvPnBoCSjIQAvD_BwE&gclsrc=aw.ds/",
          ctaText: "Shop Now",
          active: false,
          price: 199,
        },

        {
         
          name: "CONVERSE CHUCK TAYLOR ALL STAR 70 GREY",
          imageurl:
            "https://www.shooos.com/media/catalog/product/cache/2/image/9df78eab33525d08d6e5fb8d27136e95/c/o/converse-chuck-taylor-all-star-70-grey-2.jpg",
          ctaText: "Shop Now",
          active: false,
          price: 93.60,
        },

        {
         
          name: "acis GEL-Kayano 23",
          imageurl:
            http://ustatic.priceza.com/img/productgroup/306698-1-l.jpg",
          rightText: "price : 25 * 4 =100",
          leftText: "",
          producturl: "https://www.priceza.com/p/asics-running-shoes-gel-kayano-23-70836312",

          ctaText: "Shop Now",
          active: false,
          price: 1,186,
        },

        {
         
          name: "PUMA Men's Axelion",
          imageurl:
            "data:image/jpeg;base64,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",
          rightText: "price : 199",
          leftText: "",
          producturl: "https://www.ubuy.co.th/th/product/1CGSCL1LE-puma-mens-axelion-ultra-shoes",
          ctaText: "Shop Now",
          active: false,
          price: 199,
        },
      ],
    };
  },
  methods: {
    selected: function (i) {
      i.active = !i.active;
    },
    total: function () {
      var sum = 0;
      this.productlist.forEach(function (i) {
        if (i.active) {
          sum += i.price;
        }
      });
      return sum;
    },
  },
 
};
</script>

<style>
h2 {
  color: white;
}
@keyframes gradient {
  0% {
    background-position: 0% 50%;
  }
  100% {
    background-position: 100% 0%;
  }
}
h1 {
  background: linear-gradient(80deg, #ebebeb, #020202);
  background-size: 50%;
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  animation: gradient 2s infinite;
}
.text-danger {
  background: linear-gradient(80deg, #ffffff, #000000);
  background-size: 50%;
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  animation: gradient 2s infinite;
}
.white{
  background: linear-gradient(80deg, #ffffff, #090c09);
  background-size: 50%;
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  animation: gradient 2s infinite;
}
</style>
