<template>
    <div>
      <form @submit.prevent="submitFormICAO">
        <label class="Enter-icao" for="icao-code">Enter ICAO code:</label>
        <input type="text" id="icao-code" v-model="ICAO_code">
        <button type="submit">Search</button>
      </form>
      <div class="IATA-code" v-if="IATA_code">
        <h3>IATA code: {{ IATA_code }} </h3>
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
      async submitFormICAO() {
    try {
      const response = await axios.get(`http://localhost:8090/airports/ICAO/${this.ICAO_code}`);
      this.IATA_code = response.data.IATA_code;
    } catch (error) {
      console.error(error);
      alert("An error occurred while fetching the IATA code. ICAO code example 'EETN'.");
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