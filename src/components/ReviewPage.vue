<template>
<div class="container">
    <div class="review-flex" >
        <div class="form-width"> 

            <form @submit.prevent="onSubmit"> 
                <h2>Review Form</h2>
    
                <p> 
                    <label for="name">Name:</label>
                    <input id="name" type="text" v-model="name">
                </p>
                <p> 
                    <label>Reviews:</label>
                 <textarea id="review" v-model="review"></textarea>
    
                </p>
    
                <p> 
                    <label>Rating</label>
                    <select id="rating" v-model.number="rating"><!---v-model.number so a user can pick a number-->
                        <option>0</option> 
                        <option>5</option> 
                        <option>4</option> 
                        <option>3</option> 
                        <option>2</option> 
                        <option>1</option> 
                    </select>
                </p>
    
    
                <button>submit</button>
    
    
    
            </form>
        </div>

        <div class="review-width"> 
            <h2>Reviews</h2>
            <div class="review-card" v-for="review in reviews" :key="review"> 
                <p>Name: {{ review.name }}</p>
                <p> Review: {{ review.reviews }}</p>
                <p>rating: {{ review.rating }}</p>

            </div>
        </div>
    </div>


</div>
</template>

<script>
export default {
    name: "ReviewPage",

    data (){
        return{
            name: null,
            reviews: null,
            rating: null
        }
    },

    methods:{
        onSubmit(){
            let productReview = { /**now we have to send the review to our parent component app.vue, in other words we cannot display the reviews, name and ratin on
                                    on our own, so to send this method and data we use custome events $emit to tranfer the data from child to parent component */
                name: this.name,
                reviews: this.reviews,
                rating: this.rating
            }

            this.$emit("review-submitted", productReview)
            this.name = null,
            this.reviews = null,
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
</style>