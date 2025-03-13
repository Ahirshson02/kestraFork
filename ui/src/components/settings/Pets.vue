<template>
    <div>
      <button @click="getCat">Get Cat</button> <!-- Button that returns cat image-->
      <button @click="getDog">Get Dog</button> <!-- Button that returns dog image-->
      <img v-if="imgUrl" :src="imgUrl" alt="Pet Image" style="max-width: 200px;" />
      <!--Image tag to display fetched image-->
    </div>
  </template>
 
  <script>
  export default {
    // Components initial state
    data() {
      return {
        imgUrl: null, //stores the URL of the fetched image
      };
    },
 
    //Methods section
    methods: {
        //Method to fetch cat image
      async getCat() {
 
        //Defines header for API request
 
        const headers = new Headers({
          "Content-Type": "application/json",
          "x-api-key": "DEMO-API-KEY"
        });
        //Define request options for API pull
        var requestOptions = {
          method: 'GET',
          headers: headers,
          redirect: 'follow'
        };
        try {
            //Fetches cat image from API
          const response = await fetch("https://api.thecatapi.com/v1/images/search?size=med&mime_types=jpg&format=json&has_breeds=true&order=RANDOM&page=0&limit=1", requestOptions)
          const data = await response.json();
          const cat = data[0];
          console.log(cat.url);
          console.log("test");
          this.imgUrl = cat.url;
        }
        catch(error) {
          console.error('Error fetching cat data:', error);
        }
      },
      async getDog() {
        const headers = new Headers({
          "Content-Type": "application/json",
          "x-api-key": "DEMO-API-KEY"
        });
 
        var requestOptions = {
          method: 'GET',
          headers: headers,
          redirect: 'follow'
        };
        try {
            //Fetches dog image from API
          const response = await fetch("https://api.thedogapi.com/v1/images/search?size=med&mime_types=jpg&format=json&has_breeds=true&order=RANDOM&page=0&limit=1", requestOptions)
          const data = await response.json();
          const dog = data[0];
          this.imgUrl = dog.url;
        }
        catch(error) {
          console.error('Error fetching dog data:', error);
        }
      },
    },
  };
  </script>