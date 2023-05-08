<template>
    <div>
      <form @submit.prevent="submitFormIATA">
        <label class="Enter-iata" for="iata-code">Enter IATA code:</label>
        <input type="text" id="iata-code" v-model="IATA_code">
        <button type="submit">Search</button>
      </form>
      <div class="ICAO-code" v-if="ICAO_code">
        <h3>ICAO code: {{ ICAO_code }} </h3>
      </div>
    </div>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    data() {
      return {
        IATA_code: '',
        ICAO_code: '',
      };
    },
    methods: {
      async submitFormIATA() {
    try {
      const response = await axios.get(`http://localhost:8090/airports/iata/${this.IATA_code}`);
      this.ICAO_code = response.data.ICAO_code;
    } catch (error) {
      console.error(error);
      // Display an error message to the user
      alert("An error occurred while fetching the ICAO code. IATA code example 'TLL'.");
    }
  },
    },
  };
  </script>
  
    <style scoped>
    header {
      line-height: 1.5;
      max-height: 100vh;
    }
    
    .logo {
      display: block;
      margin: 0 auto 2rem;
    }
    
    nav {
      width: 100%;
      font-size: 12px;
      text-align: center;
      margin-top: 2rem;
    }
    
    nav a.router-link-exact-active {
      color: var(--color-text);
    }
    
    nav a.router-link-exact-active:hover {
      background-color: transparent;
    }
    
    nav a {
      display: inline-block;
      padding: 0 1rem;
      border-left: 1px solid var(--color-border);
    }
    
    nav a:first-of-type {
      border: 0;
    }
    
    @media (min-width: 1024px) {
      header {
        display: flex;
        place-items: center;
        padding-right: calc(var(--section-gap) / 2);
      }
    
      .logo {
        margin: 0 2rem 0 0;
      }
    
      header .wrapper {
        display: flex;
        place-items: flex-start;
        flex-wrap: wrap;
      }
    
      nav {
        text-align: left;
        margin-left: -1rem;
        font-size: 1rem;
    
        padding: 1rem 0;
        margin-top: 1rem;
      }
  
    }
    </style>