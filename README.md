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
