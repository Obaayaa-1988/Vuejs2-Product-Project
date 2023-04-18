<template>
<div class="container">
    <div class="review-flex" >
        <div class="form-width"> 

            <form @submit.prevent="submitReview"> 
                <h2>Review Form</h2>
    
                <p> 
                    <label for="name">Name:</label>
                    <input id="name" type="text" v-model="name">
                </p>
                <p> 
                    <label for="reviews">Reviews:</label>
                 <textarea id="review" v-model="review"></textarea>
    
                </p>
    
                <p> 
                    <label for="rating">Rating</label>
                    <select id="rating" v-model.number="rating"><!---v-model.number so a user can pick a number-->
                        <option>0</option> 
                        <option>5</option> 
                        <option>4</option> 
                        <option>3</option> 
                        <option>2</option> 
                        <option>1</option> 
                    </select>
                </p>
                <button type="submit" value="Submit" >submit</button>

            </form>
        </div>

        <div class="review-width"> 
            <h1>Reviews</h1> 
            <p class="length" v-if="!reviews.length">There are no reviews now</p>

             <div v-for="review in reviews" :key="review" class="review-card"> 
                <p>Name: {{ review.name }}</p>
                <p> Review: {{ review.review }}</p>
                <p>rating: {{ review.rating }}</p>

             </div>
        </div>
    </div>


</div>
</template>

<script>
export default {
    name: "ReviewPage",
    props: ["reviews"],

    data (){
        return{
            name: null,
            review: null,
            rating: null
        }
    },

    methods:{

        submitReview(){
            let productReview = { /**now we have to send the review to our parent component app.vue, in other words we cannot display the reviews, name and ratin on
                                    on our own, so to send this method and data we use custome events $emit to tranfer the data from child to parent component */
                name: this.name,
                review: this.review,
                rating: this.rating
            }

            
            this.$emit("review-submit", productReview)
            this.name = null,
            this.review = null,
            this.rating = null
        }
        
    }

}
</script>

<style scoped>
.container{
    width: 80%;
    margin: auto;
    
}

.review-flex{
    display: flex;
    justify-content: space-between;
}

.form-width{
    width: 50%;
}

form{
    max-width: 600px;
    height: 550px;
    background-color: rgb(113, 188, 231);
    padding-bottom: 4rem;
    border-radius: 20px;
}

form h2{
    text-align: center;
    padding-top: 2rem ;
}
label{
    display: block;
}

#name{
    width: 70%;
    padding: 1rem;
    margin-bottom: 2rem;
    /* margin-left: 3rem; */
}

#review{
    width: 70%;
    padding: 2rem;
    margin-bottom: 2rem;

}

#rating {
    width: 15%;
    padding: 1rem;
    margin-bottom: 2rem;
    /* margin-left: 3rem; */
}

p{
    padding-left: 3rem;
}

button{
    width: 70%;
    padding: 1rem;
    background-color: tomato;
    color: white;
    cursor: pointer;
    outline: none;
    border: none;
    border-radius: 5px;
    margin-left: 3rem;
    font-size: 1.5rem;

}
.review-width{
    width: 50%;
}

/* .review-width h1{
    text-align: center;
    font-size: 3rem;
} */

.review-card{
    background-color: white;
    width: 70%;
    height: 150px;
    border-radius: 10px;
    margin-bottom: 2rem;
}
.review-card p{
    font-size: 20px;
    margin-bottom: 1rem;
}

/* .length{
    text-align: center;
} */
</style>

<!-- <form
              class="flex justify-between items-center "
              action=""
              @submit.prevent=""
            >
              <input
                type="email"
                required
                placeholder="uniqueemailaddress@mail.walulel.com"
                class="w-[248px] h-6 pl-2 py-2 border-[2.5px]  border-[BCBCC0] outline-none rounded-l-[10px] font-normal  text-[11px]"
              >
              <button
                class="w-20 h-6 bg-[#FC5800] -ml-2 flex justify-around items-center rounded-r-[10px] text-[8px]"
              >
                <span class="font-semibold"> Subscribe </span>
                <span>
                  <svg
                    class="w-3 h-3"
                    viewBox="0 0 14 14"
                    fill="none"
                    xmlns="http://www.w3.org/2000/svg"
                  >
                    <path
                      d="M1 13L0.105573 12.5528C-0.0669502 12.8978 -0.0256149 13.3113 0.211795 13.6154C0.449204 13.9195 0.840344 14.0599 1.21693 13.9762L1 13ZM7 1L7.89443 0.552786C7.72504 0.214002 7.37877 0 7 0C6.62123 0 6.27496 0.214002 6.10557 0.552786L7 1ZM13 13L12.7831 13.9762C13.1597 14.0599 13.5508 13.9195 13.7882 13.6154C14.0256 13.3113 14.0669 12.8978 13.8944 12.5528L13 13ZM8 6.33333C8 5.78105 7.55228 5.33333 7 5.33333C6.44772 5.33333 6 5.78105 6 6.33333H8ZM1.89443 13.4472L7.89443 1.44721L6.10557 0.552786L0.105573 12.5528L1.89443 13.4472ZM6.10557 1.44721L12.1056 13.4472L13.8944 12.5528L7.89443 0.552786L6.10557 1.44721ZM13.2169 12.0238L7.21693 10.6905L6.78307 12.6429L12.7831 13.9762L13.2169 12.0238ZM6.78307 10.6905L0.78307 12.0238L1.21693 13.9762L7.21693 12.6429L6.78307 10.6905ZM8 11.6667V6.33333H6V11.6667H8Z"
                      fill="black"
                    />
                  </svg>
                </span>
              </button>
            </form> -->