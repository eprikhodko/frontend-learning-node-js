<template>
  <div>
    <main>
      <form class="flex gap-4">
        <input
          v-model="title"
          type="text"
          name="title"
          class="rounded-md border border-solid border-gray-300 p-2 text-gray-700"
        />

        <button
          type="button"
          @click="addProduct"
          class="bg-gray-300 px-8 rounded-md hover:bg-gray-400 font-bold text-1 text-letters-primary transition duration-[150ms]"
        >
          Add
        </button>
      </form>
    </main>
  </div>
</template>

<script setup lang="ts">
import { ref } from "vue";

const title = ref("");

const addProductToServer = async () => {
  // console.log({ title: title.value });
  try {
    const response = await fetch("http://localhost:3333/admin/add-product", {
      method: "POST",
      headers: { "Content-Type": "application/json" },
      /*
      The JSON.stringify() method converts a JavaScript value to a JSON string

      The JSON.stringify() method is used to convert a JavaScript object into a string in JSON format. This is necessary because the fetch() function, which is used to send the HTTP request, expects the body of the request to be a string.

      The JSON.stringify() method is often used when sending data to a server, or when storing data in a file. It is also commonly used when working with APIs, since many APIs expect data to be sent and received in JSON format.

      By using the JSON.stringify() method, the JavaScript object is converted into a string that can be included in the body of the HTTP request. This allows the server to easily parse the data and access the individual properties of the object.
      */
      body: JSON.stringify({ title: title.value }),
      /* 
      In an HTTP request, the body is the portion of the request message that carries the payload of the request. It is the part of the request that contains the data being sent to the server.

      The body of an HTTP request is optional and may not be present in all requests. For example, a GET request typically does not have a body, as it is used to retrieve data from the server rather than sending data to it. On the other hand, a POST request often includes a body, as it is used to send data to the server for processing or storage.

      The body of an HTTP request can contain various types of data, such as text, HTML, XML, JSON, or binary data. The type of data being sent in the body is usually indicated by the Content-Type header, which specifies the media type of the resource being sent.

      In this code, the body property of the object passed to the fetch() function is set to a JSON-formatted string that contains a single property called "title". This JSON object will be included in the body of the HTTP request and sent to the server for processing.
      */
    });
    console.log(response);
    /* 
    When you log the response object to the console using console.log(response), you will see a JavaScript object that represents the HTTP response received from the server.

    By logging the response object to the console, you can see the information contained in the HTTP response and use it to debug or analyze the request.
    */
  } catch (error) {
    console.error(error);
  }

  /* 
  Here is an example of what the HTTP POST request created by this function might look like:

  ################################

  POST /admin/add-product HTTP/1.1
  Host: localhost:3333
  Content-Type: application/json

  {"title":"My Product"}

  ###############################

  This request includes a POST method, a content type of "application/json", and a JSON object in the body of the request with a single property called "title" and a value of "My Product". The request is sent to the server at the specified URL, "http://localhost:3333/admin/add-product".

  The Content-Type header is used to indicate the media type of the resource being sent in the request body. The media type, also known as the MIME type, consists of two parts: a type and a subtype.

  The "application" part of the media type indicates that the resource is a binary file, a video, a sound, or some other type of application-specific data. The "json" part of the media type indicates that the resource is a JSON object.

  So, in the case of "application/json", the "application" part of the media type indicates that the resource is a JSON object that is intended for use by an application, rather than being displayed directly to the user.

  It is important to specify the correct media type in the Content-Type header, as this helps the server understand how to properly process the request. If the media type is not specified or is specified incorrectly, the server may not be able to properly interpret the request body and may return an error.

  In summary, the "application" part of the media type indicates that the resource is a JSON object that is intended for use by an application, and the "json" part indicates the specific type of data being sent in the request body.
  */
};

const addProduct = () => {
  const isOnlySpaces = (str: string) => {
    return /^\s*$/.test(str);
  };
  const isStringContainOnlySpaces = isOnlySpaces(title.value);
  if (isStringContainOnlySpaces) {
    title.value = "";
  }
  if (title.value !== "" && !isStringContainOnlySpaces) {
    addProductToServer();

    title.value = "";
  }
};
</script>
