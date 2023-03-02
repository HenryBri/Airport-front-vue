<template>
  <div>
    <table-template
      caption="All airports"
      :items="airports"
      :showControlls="true"
      @show="($event) => (airportDetailId = $event.id)"
    >
      <template #additionalHeaders><th></th></template>
      <template #additionalColumns></template>
    </table-template>
  </div>
  <Teleport to="body">
    <!-- use the modal component, pass in the prop -->
    <modal :show="showModal" @close="showModal = false">
      <template #header>
        <h3>Airport details</h3>
      </template>
      <template #body>
        <b>Name: </b>{{ currentAirport.name }}<br />
        <b>Location: </b>{{ currentAirport.location }}<br />
        <b>IATA code: </b>{{ currentAirport.IATA_code }}<br />
        <b>ICAO code: </b>{{ currentAirport.ICAO_code }}<br />
        <b>Info: </b>{{ currentAirport.info }}<br />
      </template>
    </modal>
  </Teleport>
</template>

<script>
import Modal from "./components/Modal.vue";
import TableTemplate from "./components/Table.vue";

export default {
  components: {
    Modal,
    TableTemplate,
  },
  data() {
    return {
      airports: [],
      showModal: false,
      airportDetailId: 0,
      currentAirport: {
        id: 0,
        name: "",
        location: "",
        IATA_code: "",
        ICAO_code: "",
        info: "",
      },
    };
  },
  async created() {
    this.airports = await (
      await fetch("http://localhost:8090/airports")
    ).json();
  },
  watch: {
    async airportDetailId(newId) {
      this.currentAirport = await (
        await fetch(`http://localhost:8090/airports/id/${newId}`)
      ).json();
      this.showModal = true;
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
