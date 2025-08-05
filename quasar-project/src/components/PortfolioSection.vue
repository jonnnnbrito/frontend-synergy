<template>
  <section id="portfolio" class="portfolio-section">
    <div class="portfolio-content">
      <div class="container">
        <!-- Section Header -->
        <div class="section-header">
          <h2 class="section-title">Our Portfolio</h2>
          <p class="section-subtitle">
            Explore our construction projects that showcase quality craftsmanship and innovative solutions
          </p>
        </div>

        <!-- Filter Controls -->
        <div class="filter-controls">
          <div class="filter-buttons">
            <button
              v-for="filter in filterOptions"
              :key="filter.value"
              :class="['filter-btn', { active: selectedFilter === filter.value }]"
              @click="selectedFilter = filter.value"
            >
              {{ filter.label }}
            </button>
          </div>
        </div>

        <!-- Interactive Map - Hidden until Leaflet is installed -->
        <!--
        <div class="map-container">
          <div id="portfolio-map" class="map" ref="mapContainer"></div>

          <div v-if="mapLoading" class="map-loading">
            <q-spinner-gears size="50px" color="primary" />
            <p>Loading project locations...</p>
          </div>

          <div class="map-info">
            <div class="info-card">
              <q-icon name="info" class="info-icon" />
              <span>Click markers to view project details</span>
            </div>
          </div>
        </div>
        -->

        <!-- Featured Projects Grid -->
        <div class="featured-projects">
          <h3 class="featured-title">Featured Projects</h3>
          <div class="projects-grid">
            <div
              v-for="project in filteredProjects.slice(0, 6)"
              :key="project.id"
              class="project-card"
              @click="focusProjectOnMap(project)"
            >
              <div class="project-image">
                <img :src="project.image" :alt="project.name" loading="lazy" />
                <div class="project-overlay">
                  <q-icon name="zoom_in" class="zoom-icon" />
                </div>
                <div class="project-type">{{ project.type }}</div>
              </div>
              <div class="project-info">
                <h4 class="project-name">{{ project.name }}</h4>
                <p class="project-location">
                  <q-icon name="place" />
                  {{ project.location }}
                </p>
                <div class="project-stats">
                  <span class="stat">
                    <q-icon name="straighten" />
                    {{ project.size }}
                  </span>
                  <span class="stat">
                    <q-icon name="schedule" />
                    {{ project.duration }}
                  </span>
                </div>
              </div>
            </div>
          </div>
        </div>

      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, computed, onMounted, nextTick } from 'vue'

const map = ref(null)
const selectedFilter = ref('all')

// Filter options
const filterOptions = [
  { label: 'All Projects', value: 'all' },
  { label: 'Residential', value: 'residential' },
  { label: 'Commercial', value: 'commercial' },
  { label: 'Industrial', value: 'industrial' }
]

// Sample project data
const projects = ref([
  {
    id: 1,
    name: 'Green Valley Residential Complex',
    type: 'residential',
    location: 'Green Valley, CA',
    lat: 34.0522,
    lng: -118.2437,
    image: 'https://images.unsplash.com/photo-1570129477492-45c003edd2be?w=600&h=400&fit=crop',
    size: '50,000 sq ft',
    duration: '18 months',
    year: '2023',
    description: 'Modern residential complex with sustainable design and energy-efficient features.'
  },
  {
    id: 2,
    name: 'Tech Hub Office Building',
    type: 'commercial',
    location: 'Downtown LA, CA',
    lat: 34.0622,
    lng: -118.2437,
    image: 'https://images.unsplash.com/photo-1486406146926-c627a92ad1ab?w=600&h=400&fit=crop',
    size: '75,000 sq ft',
    duration: '24 months',
    year: '2022',
    description: 'State-of-the-art office building with modern amenities and smart building technology.'
  },
  {
    id: 3,
    name: 'Manufacturing Facility',
    type: 'industrial',
    location: 'Industrial District, CA',
    lat: 34.0422,
    lng: -118.2637,
    image: 'https://images.unsplash.com/photo-1581094794329-c8112a89af12?w=600&h=400&fit=crop',
    size: '100,000 sq ft',
    duration: '30 months',
    year: '2021',
    description: 'Large-scale manufacturing facility with advanced automation and safety systems.'
  },
  {
    id: 4,
    name: 'Luxury Shopping Center',
    type: 'commercial',
    location: 'Beverly Hills, CA',
    lat: 34.0736,
    lng: -118.4004,
    image: 'https://images.unsplash.com/photo-1441986300917-64674bd600d8?w=600&h=400&fit=crop',
    size: '120,000 sq ft',
    duration: '36 months',
    year: '2023',
    description: 'Premium retail space with luxury finishes and modern architectural design.'
  },
  {
    id: 5,
    name: 'Suburban Housing Development',
    type: 'residential',
    location: 'Pasadena, CA',
    lat: 34.1478,
    lng: -118.1445,
    image: 'https://images.unsplash.com/photo-1564013799919-ab600027ffc6?w=600&h=400&fit=crop',
    size: '25 homes',
    duration: '24 months',
    year: '2022',
    description: 'Family-friendly neighborhood with parks, playgrounds, and community spaces.'
  },
  {
    id: 6,
    name: 'Corporate Headquarters',
    type: 'commercial',
    location: 'Santa Monica, CA',
    lat: 34.0195,
    lng: -118.4912,
    image: 'https://images.unsplash.com/photo-1497366216548-37526070297c?w=600&h=400&fit=crop',
    size: '90,000 sq ft',
    duration: '28 months',
    year: '2023',
    description: 'Modern corporate headquarters with sustainable design and wellness features.'
  }
])

// Computed filtered projects
const filteredProjects = computed(() => {
  if (selectedFilter.value === 'all') {
    return projects.value
  }
  return projects.value.filter(project => project.type === selectedFilter.value)
})

// Map initialization - currently disabled until Leaflet is installed
const initializeMap = async () => {
  // Map functionality will be enabled after installing Leaflet
  // Run: npm install leaflet
  // Then uncomment the map container in template and this initialization code

  /*
  try {
    const L = await import('leaflet')

    if (!mapContainer.value) return

    map.value = L.map(mapContainer.value).setView([34.0522, -118.2437], 9)

    L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
      attribution: '© OpenStreetMap contributors',
      maxZoom: 18
    }).addTo(map.value)

    const markerColors = {
      residential: '#4CAF50',
      commercial: '#2196F3',
      industrial: '#FF9800'
    }

    projects.value.forEach(project => {
      const marker = L.circleMarker([project.lat, project.lng], {
        radius: 8,
        fillColor: markerColors[project.type],
        color: '#fff',
        weight: 2,
        opacity: 1,
        fillOpacity: 0.8
      }).addTo(map.value)

      const popupContent = `
        <div class="map-popup">
          <img src="${project.image}" alt="${project.name}" class="popup-image">
          <h4>${project.name}</h4>
          <p class="popup-location"><strong>Location:</strong> ${project.location}</p>
          <p class="popup-type"><strong>Type:</strong> ${project.type}</p>
          <p class="popup-size"><strong>Size:</strong> ${project.size}</p>
          <p class="popup-year"><strong>Year:</strong> ${project.year}</p>
        </div>
      `

      marker.bindPopup(popupContent, {
        maxWidth: 250,
        className: 'custom-popup'
      })
    })

    mapLoading.value = false
  } catch (error) {
    console.error('Error initializing map:', error)
    mapLoading.value = false
  }
  */
}

// Focus project on map
const focusProjectOnMap = (project) => {
  if (map.value) {
    map.value.setView([project.lat, project.lng], 15)
    // Find and open the popup for this project
  }
}


// Component lifecycle
onMounted(async () => {
  await nextTick()
  initializeMap()
})
</script>

<style lang="scss" scoped>
// Brand Colors
$primary-green: #0A400C;
$sage-green: #819067;
$cream: #FEFAE0;
$light-cream: rgba(254, 250, 224, 0.9);
$border-color: rgba(177, 171, 134, 0.3);

.portfolio-section {
  min-height: 100vh;
  background: linear-gradient(135deg,
    rgba(254, 250, 224, 0.95) 0%,
    rgba(245, 243, 232, 0.92) 25%,
    rgba(232, 230, 211, 0.90) 50%,
    rgba(212, 210, 191, 0.88) 75%,
    rgba(177, 171, 134, 0.85) 100%
  );
  padding: 5rem 0;

  .portfolio-content {
    .container {
      max-width: 1200px;
      margin: 0 auto;
      padding: 0 2rem;
    }
  }
}

// Section Header
.section-header {
  text-align: center;
  margin-bottom: 3rem;

  .section-title {
    font-size: 3rem;
    font-weight: 800;
    color: $primary-green;
    margin-bottom: 1rem;
  }

  .section-subtitle {
    font-size: 1.2rem;
    color: $sage-green;
    max-width: 600px;
    margin: 0 auto;
    line-height: 1.6;
  }
}

// Filter Controls
.filter-controls {
  display: flex;
  justify-content: center;
  margin-bottom: 3rem;

  .filter-buttons {
    display: flex;
    background: white;
    border-radius: 25px;
    padding: 4px;
    box-shadow: 0 4px 15px rgba($primary-green, 0.1);

    .filter-btn {
      padding: 0.75rem 1.5rem;
      border: none;
      background: transparent;
      color: $sage-green;
      border-radius: 20px;
      cursor: pointer;
      transition: all 0.3s ease;
      font-weight: 500;

      &:hover {
        background: rgba($sage-green, 0.1);
      }

      &.active {
        background: $primary-green;
        color: white;
      }
    }
  }
}

// Map Container
.map-container {
  position: relative;
  height: 60vh;
  min-height: 400px;
  margin-bottom: 4rem;
  border-radius: 15px;
  overflow: hidden;
  box-shadow: 0 8px 25px rgba($primary-green, 0.15);

  .map {
    width: 100%;
    height: 100%;
  }

  .map-loading {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    text-align: center;
    color: $sage-green;

    p {
      margin-top: 1rem;
      font-size: 1.1rem;
    }
  }

  .map-info {
    position: absolute;
    top: 1rem;
    left: 1rem;
    z-index: 1000;

    .info-card {
      background: white;
      padding: 0.75rem 1rem;
      border-radius: 8px;
      box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
      display: flex;
      align-items: center;
      gap: 0.5rem;
      font-size: 0.9rem;
      color: $sage-green;

      .info-icon {
        color: $primary-green;
      }
    }
  }
}

// Featured Projects
.featured-projects {
  .featured-title {
    font-size: 2rem;
    font-weight: 700;
    color: $primary-green;
    text-align: center;
    margin-bottom: 2rem;
  }

  .projects-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 2rem;
    margin-bottom: 3rem;
  }
}

// Project Cards
.project-card {
  background: white;
  border-radius: 15px;
  overflow: hidden;
  box-shadow: 0 8px 25px rgba($primary-green, 0.1);
  transition: all 0.3s ease;
  cursor: pointer;

  &:hover {
    transform: translateY(-5px);
    box-shadow: 0 15px 40px rgba($primary-green, 0.2);

    .project-overlay {
      opacity: 1;
    }

    .project-image img {
      transform: scale(1.05);
    }
  }

  .project-image {
    position: relative;
    height: 200px;
    overflow: hidden;

    img {
      width: 100%;
      height: 100%;
      object-fit: cover;
      transition: transform 0.3s ease;
    }

    .project-overlay {
      position: absolute;
      top: 0;
      left: 0;
      right: 0;
      bottom: 0;
      background: rgba($primary-green, 0.8);
      display: flex;
      align-items: center;
      justify-content: center;
      opacity: 0;
      transition: opacity 0.3s ease;

      .zoom-icon {
        color: white;
        font-size: 2rem;
      }
    }

    .project-type {
      position: absolute;
      top: 1rem;
      right: 1rem;
      background: $primary-green;
      color: white;
      padding: 0.4rem 0.8rem;
      border-radius: 15px;
      font-size: 0.75rem;
      font-weight: 600;
      text-transform: capitalize;
    }
  }

  .project-info {
    padding: 1.5rem;

    .project-name {
      font-size: 1.1rem;
      font-weight: 700;
      color: $primary-green;
      margin-bottom: 0.5rem;
    }

    .project-location {
      display: flex;
      align-items: center;
      gap: 0.3rem;
      color: $sage-green;
      font-size: 0.9rem;
      margin-bottom: 1rem;
    }

    .project-stats {
      display: flex;
      gap: 1rem;

      .stat {
        display: flex;
        align-items: center;
        gap: 0.3rem;
        color: $sage-green;
        font-size: 0.8rem;

        .q-icon {
          font-size: 0.9rem;
        }
      }
    }
  }
}


// Mobile Responsive
@media (max-width: 768px) {
  .portfolio-section {
    padding: 3rem 0;

    .portfolio-content .container {
      padding: 0 1rem;
    }
  }

  .section-header {
    .section-title {
      font-size: 2.5rem;
    }

    .section-subtitle {
      font-size: 1rem;
    }
  }

  .filter-controls .filter-buttons {
    flex-wrap: wrap;
    justify-content: center;

    .filter-btn {
      padding: 0.6rem 1.2rem;
      font-size: 0.9rem;
    }
  }

  .map-container {
    height: 50vh;
    min-height: 300px;
    margin-bottom: 3rem;
  }

  .featured-projects {
    .featured-title {
      font-size: 1.8rem;
    }

    .projects-grid {
      grid-template-columns: 1fr;
      gap: 1.5rem;
    }
  }

  .project-card .project-image {
    height: 180px;
  }
}
</style>

<style>
/* Global Leaflet popup styles */
.custom-popup .leaflet-popup-content-wrapper {
  border-radius: 8px;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
}

.map-popup {
  font-family: 'Roboto', sans-serif;
}

.map-popup .popup-image {
  width: 100%;
  height: 120px;
  object-fit: cover;
  border-radius: 6px;
  margin-bottom: 8px;
}

.map-popup h4 {
  margin: 0 0 8px 0;
  color: #0A400C;
  font-size: 1rem;
}

.map-popup p {
  margin: 4px 0;
  font-size: 0.85rem;
  color: #555;
}
</style>
