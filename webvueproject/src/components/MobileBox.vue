
<template>
  <div>
    <nav class="navbar">
      <button class="hamburger" @click="toggleMenu">☰</button>
      <div :class="{ 'nav-filters': true, open: isMenuOpen }">
        <div class="filter-group">
          <span class="filter-title">Price:</span>
          <button :class="{ active: activePrice === 'low' }" @click="setPrice('low')">≤ 500 USD</button>
          <button :class="{ active: activePrice === 'high' }" @click="setPrice('high')">> 500 USD</button>
        </div>
        <div class="filter-group">
          <span class="filter-title">Year:</span>
          <button v-for="year in [2023, 2024, 2025]"
                  :key="year"
                  :class="{ active: activeYear === year }"
                  @click="setYear(year)">
            {{ year }}
          </button>
        </div>
      </div>
    </nav>

   
    <div class="mobile-group">
      <SingleMobile
        v-for="phone in filteredMobiles"
        :key="phone.id"
        :phone="phone"
      />
    </div>
  </div>
</template>

<script>
import SingleMobile from './SingleMobile.vue';

export default {
  name: 'MobileBox',
  components: { SingleMobile },
  props: {
    Mobiles: {
      type: Array,
      required: true
    }
  },
  data() {
    return {
      activePrice: 'low',
      activeYear: 2023,
      isMenuOpen: false
    };
  },
  computed: {
    filteredMobiles() {
      return this.Mobiles.filter(m => {
        const cost = parseFloat(m.Cost);
        const matchesPrice = this.activePrice === 'low' ? cost <= 500 : cost > 500;
        const matchesYear = parseInt(m.YearOfRelease) === this.activeYear;
        return matchesPrice && matchesYear;
      });
    }
  },
  methods: {
    toggleMenu() {
      this.isMenuOpen = !this.isMenuOpen;
    },
    setPrice(price) {
      this.activePrice = price;
      this.isMenuOpen = false;
    },
    setYear(year) {
      this.activeYear = year;
      this.isMenuOpen = false;
    }
  }
};
</script>

<style scoped>

.navbar {
  display: grid;
  grid-template-columns: auto 1fr;
  align-items: center;
  background-color: #2563eb;
  color: white;
  padding: 10px 20px;
}


.hamburger {
  display: none;
  font-size: 24px;
  background: none;
  border: none;
  color: white;
  cursor: pointer;
}


.nav-filters {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 10px;
  padding: 10px 0;
}

.filter-group {
  display: block;
  text-align: left;
  padding-left: 10px;
}

.filter-title {
  font-weight: bold;
  display: block;
  margin-bottom: 4px;
}

.filter-group button {
  display: inline-block;
  background-color: #3b82f6;
  color: white;
  padding: 6px 12px;
  margin-right: 6px;
  margin-bottom: 6px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.filter-group button.active {
  background-color: #1e40af;
}


@media (max-width: 600px) {
  .hamburger {
    display: inline-block;
  }

  .nav-filters {
    display: none;
    grid-template-columns: 1fr;
    background-color: #1e3a8a;
    width: 100%;
  }

  .nav-filters.open {
    display: grid;
  }

  .filter-group {
    margin-bottom: 10px;
  }

  .filter-group button {
    display: block;
    width: 100%;
    text-align: left;
  }
}


.mobile-group {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
  gap: 1.5em;
  margin-top: 2em;
}
</style>
