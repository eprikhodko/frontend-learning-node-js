<template>
  <main>
    <h1 class="text-2xl font-semibold">My Products</h1>
    <p>List of all the products...</p>

    <ul>
      <li v-for="product in products" :key="product.title">
        {{ product.title }}
      </li>
    </ul>
  </main>
</template>

<script setup lang="ts">
import { onMounted, ref } from "vue";

interface Product {
  title: string;
}

const products = ref<Product[]>([]);

const getProducts = async () => {
  try {
    const response = await fetch("http://localhost:3333/");
    const data = await response.json();
    /* 
    The response.json() method is used to parse the body of an HTTP response as JSON.

    When you make an HTTP request using the fetch() function, the response you receive is a Response object that contains the data returned by the server. The body of the response is not automatically parsed as JSON, so you need to use the response.json() method to parse it manually.

    The body of a raw HTTP response is a string that represents the data returned by the server. The format of the data in the body of the response depends on the server and the type of data it is returning.

    For example, if the server is returning JSON data, the body of the response will be a string that contains the JSON data. If the server is returning HTML, the body of the response will be a string that contains the HTML code.

    You cannot use the body of the response "straight away" because it is a string, and you may need to parse it to a different data type depending on the format of the data.

    For example, if the server is returning JSON data, you will need to parse the body of the response as JSON in order to access the data as a JavaScript object. You can use the JSON.parse() function to parse the body of the response as JSON:

    const response = await fetch('/api/products')
    const data = JSON.parse(response.body)

    Alternatively, you can use the response.json() method, which is a convenience method provided by the fetch() function that automatically parses the body of the response as JSON:

    const response = await fetch('/api/products')
    const data = await response.json()

    Parsing the body of the response as JSON converts the string representation of the data to a JavaScript object. This makes it easier to access and manipulate the data in your code.
    */
    products.value = data;
    console.log(products.value);
  } catch (error) {
    console.log(error);
  }
};

/* 
Using onMounted(getProducts()) is incorrect because it will immediately execute the getProducts() function and pass the returned value (which is a Promise) to onMounted() as an argument.

The onMounted() hook in Vue 3 expects a function with no return value as its argument. This function will be executed when the component is mounted. If you want to use onMounted to fetch data from an API, you can create a function that makes an HTTP request and returns a Promise, but you should not execute the function when you pass it to onMounted().

In this example, the getProducts() function is passed as an argument to the onMounted() hook, but it is not executed. Instead, it will be executed when the component is mounted. The data it fetches will be stored in the products ref.

The onMounted() hook is called after the component has been mounted to the DOM, which means that the component's template has already been rendered, and any children components have also been mounted. This is the appropriate hook to use if you want to fetch data from the server as soon as the component is ready to display it.

#################################
In the context of a Vue 3 component, "mounted to the DOM" means that the component's template has been rendered and inserted into the document object model (DOM).

The DOM is a tree-like structure that represents the HTML of a webpage. When a Vue 3 component is "mounted to the DOM", it means that the component's template has been rendered and inserted into the DOM as an HTML element.

For example, if you have a Vue 3 component with the following template:

<template>
  <div>
    <h1>Hello, World!</h1>
  </div>
</template>
When the component is mounted to the DOM, the template will be rendered as an HTML element, like this:

<div>
  <h1>Hello, World!</h1>
</div>
The onMounted() hook in Vue 3 is called after the component has been mounted to the DOM, which means that the component's template has already been rendered and inserted into the DOM.

########################
In the context of a Vue 3 component, "rendered" means that the component's template has been processed and converted into HTML elements that can be inserted into the DOM.

A template in Vue 3 is a declarative way of specifying the structure of the HTML elements that make up a component. When a component's template is "rendered", it means that the template has been processed and converted into actual HTML elements that can be inserted into the DOM.

For example, if you have a Vue 3 component with the following template:

<template>
  <div>
    <h1>Hello, World!</h1>
  </div>
</template>
When the component's template is rendered, it will be converted into the following HTML elements:

<div>
  <h1>Hello, World!</h1>
</div>
The process of rendering a component's template is typically handled by the Vue 3 runtime. When a component is mounted to the DOM, the template is automatically rendered and the resulting HTML elements are inserted into the DOM.

###############################
When you use the onMounted() hook to execute the fetchData() function in a Vue 3 component, the fetchData() function will be executed after the component has been mounted to the DOM.

The fetchData() function makes an HTTP request to the server to retrieve data. When the data is returned from the server, it is stored in the products ref.

In the template of the component, the products ref is used to display a list of products:

<template>
  <div>
    <ul>
      <li v-for="product in products" :key="product.title">{{ product.title }}</li>
    </ul>
  </div>
</template>
The v-for directive in the template is used to loop over the products array and render a list of li elements for each product.

When the fetchData() function is executed, it retrieves the data from the server and stores it in the products ref. This updates the products array and triggers a re-render of the component's template. The v-for directive in the template will loop over the updated products array and render the new list of products.

So, to answer your question: when you use onMounted(fetchData), the fetchData() function is executed after the component has been mounted to the DOM, and the data it retrieves is used to update the component's template and re-render the list of products.
*/
onMounted(getProducts);
</script>
