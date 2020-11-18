# Coursework


<html>
    <head>
        <title>Available Lessons</title>
        <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
        <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css">
        <script src="lessons.js/lessons.js"></script>
    </head>

    <body>
        <div id="app">
            <header>
                <h1> {{ sitename }}</h1>
                <button @click='showCheckout'> 
                    {{cartItemCount}}      
                <span class ="fa fa-cart-plus"></span> Shopping cart </button>
            </header>
            <main>

                <div v-if='showLesson' >
                    <!--Using the for loop we are looping through the return of the sortedLesson computed property-->
                    <!--This will give us a list sorted by Price-->
                    <div v-for="lesson in sortedLessons">
                   
                        <img v-bind:src="lesson.image" style="width: 15%; height: 26%;">
                        <div style="display: inline-block" >
                        <h3>Subject: {{lesson.subject}}</h3>
				        <p>Location: {{lesson.location}}</p>
			        	<p>Price: {{lesson.price}}</p>
                        <p>Number of Spaces: {{lesson.numberOfSpaces}}</p>
                     
                        <!-- The button will display when 'Add to Cart is True -->                        
                        <!--When we click the Add To Cart are now passing the lesson and its id to the function as parameters-->
                         <button @click='addToCart(lesson)' class="btn" v-if='canAddToCart(lesson)'> Add to Cart </button>

                            <!-- This button will be disabled otherwise -->
                        <button disabled ='disabled'class="btn" v-else>Add to Cart</button>
                    </div>
CONTINUATION
           </div>  
            </div>
            <div v-else>
               
                <h2>Checkout</h2>
                <ul>
                <li v-for="cart"> {{lesson.subject}}</li>
            </ul>

                </div>
                <p>
                    <strong>Name:</strong>
                    <!-- This input field is bound to 'firstName' in the 'order' object -->
                    <input v-model.trim="order.name"/>
                </p>
                <p>
                    <strong>Phone:</strong>
                    <!-- This input field is bound to 'lastName' in the 'order' object -->
                    <input v-model.number='order.phone' type="number"/>
                </p>
                <h2>Order Information</h2>
                <p>Name:{{order.name}}</p>
                <p>Phone: {{order.phone}}</p>

                <button v-on:click="submitForm">Checkout</button>
            </div>
           
            </main>
        </div>
    </body>
    
         var webstore = new Vue({
            el: '#app',
            data: {
                showLesson: true,
                sitename: 'New Lessons',
                id: [1001, 1002, 1003, 1004, 1005, 1006, 1007, 1008, 1009, 1010],
                cart: [], // array to store items in shopping cart,
                location: '',
                availableInventory: 10,
                order: {
                    fullName: "",
                    phone: "",
                },
                lessons: lesson,
            },
	     methods:{
                addToCart: function (lesson) {
                    this.cart.push(lesson.id);
                },
             addToCheckOutCart(lesson){
                    this.addToCheckOutCart.push(lesson);
                },
                showCheckout: function(){
                    this.showLesson = this.showLesson ? false : true;
                },
		submitForm(){
                    alert('order has been placed')
                },
                //Remove canAddToCart from Computed to method since computed does not take parameters, 
                //We are now working with an array of objects and therefore need to pass the lesson
                //and its id to identify which lesson we are working with
                  canAddToCart: function(lesson){
                    return lesson.availableInventory > this.cartCount(lesson.id);
                },
