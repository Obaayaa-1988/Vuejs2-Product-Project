<template>
<div class="container">
    <div>
        <form> 
        <h2>Review Form</h2>

            <p> 
                <label for="name">Name:</label>
                <input id="name" type="text" >
            </p>
            <p> 
                <label>Reviews:</label>
             <textarea id="review"></textarea>

            </p>

            <p> 
                <label>Rating</label>
                <select id="rating">
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


</div>
</template>

<script>
export default {
    name: "ReviewPage",

    data (){
        return{
            name: null,
            review: null,
            rating: null
        }
    }

}
</script>

<style scoped>
.container{
    width: 80%;
    margin: auto;
    
}

form{
    max-width: 600px;
    height: 550px;
    background-color: rgb(241, 237, 231);
    padding-bottom: 4rem;
    /* padding: 3rem; */
   

 
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
    font-size: 1rem;

}
</style>