<template>

    <section class="hero">
      <h1 class="hero-title">
        Discover Premium <span>Cape Town</span> Rentals
      </h1>
      <p class="hero-text">
          Browse luxury apartments, beachfront villas and
          exclusive short-term stays across Cape Town.
      </p>

      <button>Explore Properties</button>
      
    </section>

  <Header :count="activeProperties.length"
          :favourites="favouriteCount"
          />

  <div class="controls">

    <input
    type="text"
    v-model="search"
    placeholder="Search properties..."
    >

    <select v-model="sortOrder">
      <option value="low">Price Low → High</option>
      <option value="high">Price High → Low</option>
    </select>

  </div>

  <div class="grid">
    <PropertyCard
    v-for="property in filteredProperties"
    :key="property.id"
    :property="property"
    @toggle-favourite="toggleFavourite"
    />

  </div>

  <footer class="footer">
    <h3>Homes & Beyond</h3>
    <p>Premium Short-Term Rentals in Cape Town</p>
  </footer>

</template>

<script>
import Header from "./components/Header.vue"
import PropertyCard from "./components/PropertyCard.vue";
import properties from "./data/properties"

export default {
  components: {
    Header,
    PropertyCard
  },

  data() {
    return {
      properties,
      search: "",
      sortOrder: "low"
    }
  },

  computed: {

    filteredProperties() {
      let filtered = this.properties.filter(property=>

        property.title
          .toLowerCase()
          .includes(this.search.toLowerCase())

        ||

        property.location
          .toLowerCase()
          .includes(this.search.toLowerCase())

       )

      if (this.sortOrder === "low") {
        filtered.sort((a,b) => a.price - b.price)
      }else {
        filtered.sort((a,b) => b.price - a.price)
      }

      return filtered

    },

    activeProperties() {
      return this.properties.filter(
        property => property.available
      )
    }
  },

  methods: {
    toggleFavourite(id) {
      const property = this.properties.find(
        p => p.id === id
      )

      property.favourite =
        !property?.favourite

      localStorage.setItem(
        "properties",
        JSON.stringify(this.properties)
      )
    }
  },

  mounted() {

    const saved =
    localStorage.getItem("properties")

    if(saved) {
      this.properties = JSON.parse(saved)
    }
  },

  favouriteCount() {
    return this.properties.filter(
      property => property.favourite
    ).length
  }

}
</script>

