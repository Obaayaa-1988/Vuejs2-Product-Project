<template>
<div class="container">
    <div>
        <h2>Review Form</h2>
        <form> 
            <p> 
                <label for="name">Name:</label>
                <input id="name" type="text" ><br>
            </p>
            <p> 
                <label>Reviews</label>
             <textarea id="review"></textarea>

            </p>

            <p> 
                <label>Reviews</label>
                <select id="rating">
                    <option>5</option> 
                    <option>4</option> 
                    <option>3</option> 
                    <option>2</option> 
                    <option>1</option> 
                </select>
            </p>



        </form>
    </div>


</div>
</template>

<script>
export default {
    name: "ReviewPage"

}
</script>

<style scoped>
.container{
    width: 80%;
    margin: auto;
}
</style>