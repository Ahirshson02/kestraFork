<template>
    <div class="container">
        <h2>Congratulations, <br> You found the hidden secret!</h2>
        <p>Enjoy :)</p>
        <div class="button-container">
            <button @click="getCat">
                Get Cat
            </button>
            <button @click="getDog">
                Get Dog
            </button>
        </div>
        <div v-if="imgUrl" class="image-container">
            <img :src="imgUrl" alt="Pet Image">
        </div>
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
                    method: "GET",
                    headers: headers,
                    redirect: "follow"
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
                catch (error) {
                    console.error("Error fetching cat data:", error);
                }
            },
            async getDog() {
                const headers = new Headers({
                    "Content-Type": "application/json",
                    "x-api-key": "DEMO-API-KEY"
                });

                var requestOptions = {
                    method: "GET",
                    headers: headers,
                    redirect: "follow"
                };
                try {
                    //Fetches dog image from API
                    const response = await fetch("https://api.thedogapi.com/v1/images/search?size=med&mime_types=jpg&format=json&has_breeds=true&order=RANDOM&page=0&limit=1", requestOptions)
                    const data = await response.json();
                    const dog = data[0];
                    this.imgUrl = dog.url;
                }
                catch (error) {
                    console.error("Error fetching dog data:", error);
                }
            },
        },
    };
</script>

<style scoped>
/* Center the container */
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  min-height: 100vh;
  /* Takes up full height of viewport */
  text-align: center;
}

/* Style for the buttons */
.button-container {
  display: flex;
  gap: 15px;
  margin-bottom: 20px;
}

button {
  background-color: #2C0059;
  color: white;
  border: none;
  padding: 12px 24px;
  font-size: 18px;
  cursor: pointer;
  border-radius: 8px;
  transition: background 0.3s;
}

button:hover {
  background-color: #5302a3;
}

/* Style for the image */
img {
  max-width: 300px;
  border-radius: 10px;
  margin-top: 20px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  border: 10px solid white;
}
</style>