<template>
  <div id="app" class="product-background">
    <!--------------main flex----------start--->
    <div class="product-background1"> 
      <!----display---image start------------>
      <div class="product-image">
      <img :src="image" />
        
      </div>
      <!-----display--------image end--------->

      <!-------product details------- start--->
      <div class="product-details"> 
        <div class="product-name"> 
          <h1> {{ product }}</h1>
        </div>

        <div> 
          <h2>Shipping: 0</h2>
        </div>

        <div> 
          <h2 v-if="inStock">In Stock</h2>
          <!-- <h2 v-else="inStock">Out of Stock</h2> -->

        </div>

        <div class="product-list-details">
          <h3>Details</h3>
        </div>
        <!----product list start-->
        <ul> 
          <li v-for="detail in productDetails" :key="detail">  
            {{ detail }}
          </li>
        </ul>
        <!----product list end-->


        <!----product color start-->
        <div class="socks-colors"> 

        </div>
        <!--  -->

        <div v-for="variant in variants" 
        :key="variant.variantsId"
        class="socks-colors"
        :style="{ backgroundColor: variant.variantsColor }"
        @mouseover="updateProduct(variant.variantsImage)"
>                                                                  <!----here we are style binding with a class which has been partially styled with no background colors in css-->
        >                                                          <!----background colors vue is able to identify the named colors in the data and apply it to the div's background -->
        >                                                          <!----also the variantsColors is now then connected to the variantImage in the same div with help of the mouseover event
                                                                    and the updateProduct function that took the variantImage variable as a parameter-->

         <!-- <p @mouseover="updateProduct(variant.variantsImage)"></p>  -->
         <!-- <p @mouseover="updateProduct(variant.variantsImage)">{{ variant.variantsColor }}</p>  -->
          
        </div>

        
        <!----product color end---->  

        <button class="btn" @click="addItems">add to cart</button>
      </div>

      <!-------product details------- end----->

      <div class="product-cart">
        <h4 > Cart({{ cart }})</h4>  
      </div>
     




    </div>
    <!--------------main flex------------end-->
  </div>
</template>

<script>

export default {
  name: 'App',
  components: { 
  },

  data() {
    return {
      product: "Abigail's Brand Of Socks",
      image: require('./assets/images/yellow-socks.jpg'), /*for images to appear in the html from data you have to require it*/ 
      inStock: true,                                  /*inStock: v-if="inStock" = will display instock if instock is true, ifInstock is false in data it will not display, */ 
      productDetails: ["80% Cotton", "20% Polyster", "Gender-Neutral"],
      variants: [
                 { variantsId: 2234,
                  variantsColor: "yellow",
                  variantsImage: require('./assets/images/yellow-socks.jpg')
                 
                 },
                 { variantsId: 2235,
                   variantsColor: "purple",
                   variantsImage: require('./assets/images/purple-socks.jpg')

                 

                 },
          
      ],

      cart: 0,

    }
  },

  methods: {
    addItems(){
      this.cart += 1;/**here we are targeting the cart data with the button in html, with this.cart with JS arimethics */
    },

    updateProduct(variantsImage){
      this.image = variantsImage;/**this.image means that we want the dummy image to be changed to the variantImage, the update function is giving a parameter because we want the image to be
                                 dynamic since they two images. the updateProduct function is then connected to the html element  */
    }


  }
}
</script>






<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Poppins:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&display=swap');

*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
 
}

.product-background{
  height: 100vh;
  width: 100%;
  background: rgb(184, 223, 235);
  font-family: 'Poppins';
}
.product-background1{
  display: flex;
  justify-content: space-between;
}

.product-image{
  padding: 6rem 7rem;
}

.product-image img{
  width: 32rem;
  height: 40rem;
  border-radius: 15px;
  cursor: pointer;
  object-fit: cover;
  object-position: 50% 50%;
}

.product-details{
  /* width: 50%; */
  padding-top: 7rem;
  text-align: justify;


}

.product-details h1{
  font-size: 2.5rem;
  margin-bottom: 3rem;
  text-align: center;
}

.product-details h2{
  margin-bottom: 2rem;
}

.product-list-details h3{

  font-size: 35px;


}



.socks-colors{
  height: 50px;
  width: 50px;
  cursor: pointer;
  /* background-color: yellow; */
  margin-top: 1rem;
}
/* .socks-colors1{
  height: 50px;
  width: 50px;
  cursor: pointer;
  background-color: purple;
  margin-top: 2rem;
} */
.btn{
  outline: none;
  background-color: aquamarine;
  padding: 1.1rem 0.9rem ;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-size: 20px;
  font-weight: bold;
  margin-top: 2rem;
}

ul{

  /* margin-bottom: 2rem; */
  margin-left: 2rem;

}

.product-cart{
  padding-top: 8rem;
  padding-right: 5rem;
  
}

.product-cart h4{
  padding: 3rem 1rem;
  font-size: 18px;
  text-align: center;
  background-color: aliceblue;
  border: 1px solid black;
  border-radius: 5px;
}


/* @media screen and (min-width: 480px) {

  .product-details h1 {
      font-size: 1.5rem;
      margin-bottom: 3rem;
    }
  .product-details {
      padding-top: 6rem;
    
    
    }
} */
</style>
