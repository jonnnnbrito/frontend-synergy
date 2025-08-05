<template>
  <q-page>
    <!-- Portfolio Header Section -->
    <section class="portfolio-header">
      <div class="header-content">
        <h1 class="page-title">Our Portfolio</h1>
        <p class="page-subtitle">
          Explore our construction projects across the region. Click on any marker to see project details.
        </p>
        
        <!-- Filter Controls -->
        <div class="filter-controls">
          <q-btn-toggle
            v-model="selectedFilter"
            toggle-color="primary"
            color="white"
            text-color="primary"
            :options="filterOptions"
            class="filter-toggle"
          />
        </div>
      </div>
    </section>

    <!-- Interactive Map Section -->
    <section class="map-section">
      <div class="map-container">
        <div id="portfolio-map" class="map"></div>
        
        <!-- Map Loading State -->
        <div v-if="mapLoading" class="map-loading">
          <q-spinner-gears size="50px" color="primary" />
          <p>Loading project locations...</p>
        </div>
      </div>
    </section>

    <!-- Projects Grid Section -->
    <section class="projects-grid-section">
      <div class="container">
        <h2 class="section-heading">Featured Projects</h2>
        <div class="projects-grid">
          <div 
            v-for="project in filteredProjects" 
            :key="project.id"
            class="project-card"
            @click="focusProjectOnMap(project)"
          >
            <div class="project-image">
              <img :src="project.image" :alt="project.name" />
              <div class="project-type-badge">{{ project.type }}</div>
            </div>
            <div class="project-info">
              <h3 class="project-name">{{ project.name }}</h3>
              <p class="project-location">{{ project.location }}</p>
              <div class="project-stats">
                <div class="stat">
                  <q-icon name="straighten" />
                  <span>{{ project.size }}</span>
                </div>
                <div class="stat">
                  <q-icon name="schedule" />
                  <span>{{ project.duration }}</span>
                </div>
                <div class="stat">
                  <q-icon name="calendar_today" />
                  <span>{{ project.year }}</span>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
  </q-page>
</template>

<script setup>
import { ref, onMounted, computed, nextTick } from 'vue'

// Reactive data
const map = ref(null)
const mapLoading = ref(true)
const selectedFilter = ref('all')

// Filter options
const filterOptions = [
  { label: 'All Projects', value: 'all' },
  { label: 'Residential', value: 'residential' },
  { label: 'Commercial', value: 'commercial' },
  { label: 'Industrial', value: 'industrial' }
]

// Sample project data (replace with your actual data)
const projects = ref([
  {
    id: 1,
    name: 'Green Valley Residential Complex',
    type: 'residential',
    location: 'Green Valley, CA',
    lat: 34.0522,
    lng: -118.2437,
    image: 'https://images.unsplash.com/photo-1570129477492-45c003edd2be?w=800',
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
    lat: 34.0522,
    lng: -118.2437,
    image: 'https://images.unsplash.com/photo-1486406146926-c627a92ad1ab?w=800',
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
    lat: 34.0322,
    lng: -118.2637,
    image: 'https://images.unsplash.com/photo-1581094794329-c8112a89af12?w=800',
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
    image: 'https://images.unsplash.com/photo-1441986300917-64674bd600d8?w=800',
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
    image: 'https://images.unsplash.com/photo-1564013799919-ab600027ffc6?w=800',
    size: '25 homes',
    duration: '24 months',
    year: '2022',
    description: 'Family-friendly neighborhood with parks, playgrounds, and community spaces.'
  }
])

// Computed filtered projects
const filteredProjects = computed(() => {
  if (selectedFilter.value === 'all') {
    return projects.value
  }
  return projects.value.filter(project => project.type === selectedFilter.value)
})

// Map initialization
const initializeMap = async () => {
  try {
    // Note: You'll need to run `npm install leaflet` first
    // Then uncomment this code:
    
    /*
    const L = await import('leaflet')
    
    // Initialize map
    map.value = L.map('portfolio-map').setView([34.0522, -118.2437], 10)
    
    // Add tile layer
    L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
      attribution: '© OpenStreetMap contributors'
    }).addTo(map.value)
    
    // Custom marker icons
    const getMarkerIcon = (type) => {
      const colors = {
        residential: '#4CAF50',
        commercial: '#2196F3', 
        industrial: '#FF9800'
      }
      
      return L.divIcon({
        className: 'custom-marker',
        html: `<div class="marker-pin" style="background-color: ${colors[type]}">
                 <i class="material-icons">${getMarkerIcon(type)}</i>
               </div>`,
        iconSize: [30, 30],
        iconAnchor: [15, 30]
      })
    }
    
    // Add project markers
    projects.value.forEach(project => {
      const marker = L.marker([project.lat, project.lng], {
        icon: getMarkerIcon(project.type)
      }).addTo(map.value)
      
      // Create popup content
      const popupContent = `
        <div class="map-popup">
          <img src="${project.image}" alt="${project.name}" class="popup-image">
          <h3>${project.name}</h3>
          <p class="popup-location">${project.location}</p>
          <p class="popup-description">${project.description}</p>
          <div class="popup-stats">
            <span><strong>Size:</strong> ${project.size}</span>
            <span><strong>Duration:</strong> ${project.duration}</span>
            <span><strong>Year:</strong> ${project.year}</span>
          </div>
        </div>
      `
      
      marker.bindPopup(popupContent)
    })
    */
    
    mapLoading.value = false
  } catch (error) {
    console.error('Error initializing map:', error)
    mapLoading.value = false
  }
}

// Focus project on map
const focusProjectOnMap = (project) => {
  if (map.value) {
    map.value.setView([project.lat, project.lng], 15)
    // Trigger popup for the project
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

// Portfolio Header
.portfolio-header {
  background: linear-gradient(135deg, $light-cream, rgba(245, 243, 232, 0.95));
  padding: 4rem 2rem 2rem;
  text-align: center;

  .header-content {
    max-width: 800px;
    margin: 0 auto;

    .page-title {
      font-size: 3rem;
      font-weight: 800;
      color: $primary-green;
      margin-bottom: 1rem;
    }

    .page-subtitle {
      font-size: 1.2rem;
      color: $sage-green;
      margin-bottom: 2rem;
      line-height: 1.6;
    }

    .filter-controls {
      display: flex;
      justify-content: center;

      .filter-toggle {
        border-radius: 25px;
        overflow: hidden;
        box-shadow: 0 4px 15px rgba($primary-green, 0.15);
      }
    }
  }
}

// Map Section
.map-section {
  height: 60vh;
  min-height: 500px;
  position: relative;

  .map-container {
    height: 100%;
    position: relative;

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
  }
}

// Projects Grid
.projects-grid-section {
  padding: 4rem 2rem;
  background: linear-gradient(135deg, $cream, rgba(245, 243, 232, 0.5));

  .container {
    max-width: 1200px;
    margin: 0 auto;

    .section-heading {
      font-size: 2.5rem;
      font-weight: 700;
      color: $primary-green;
      text-align: center;
      margin-bottom: 3rem;
    }

    .projects-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
      gap: 2rem;
    }
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
    box-shadow: 0 15px 40px rgba($primary-green, 0.15);
  }

  .project-image {
    position: relative;
    height: 250px;
    overflow: hidden;

    img {
      width: 100%;
      height: 100%;
      object-fit: cover;
      transition: transform 0.3s ease;
    }

    &:hover img {
      transform: scale(1.05);
    }

    .project-type-badge {
      position: absolute;
      top: 1rem;
      right: 1rem;
      background: $primary-green;
      color: white;
      padding: 0.5rem 1rem;
      border-radius: 20px;
      font-size: 0.8rem;
      font-weight: 600;
      text-transform: capitalize;
    }
  }

  .project-info {
    padding: 1.5rem;

    .project-name {
      font-size: 1.3rem;
      font-weight: 700;
      color: $primary-green;
      margin-bottom: 0.5rem;
    }

    .project-location {
      color: $sage-green;
      margin-bottom: 1rem;
      font-size: 0.9rem;
    }

    .project-stats {
      display: flex;
      gap: 1rem;
      flex-wrap: wrap;

      .stat {
        display: flex;
        align-items: center;
        gap: 0.3rem;
        color: $sage-green;
        font-size: 0.85rem;

        .q-icon {
          font-size: 1rem;
        }
      }
    }
  }
}

// Mobile Responsive
@media (max-width: 768px) {
  .portfolio-header {
    padding: 2rem 1rem;

    .header-content .page-title {
      font-size: 2.5rem;
    }
  }

  .map-section {
    height: 50vh;
    min-height: 400px;
  }

  .projects-grid-section {
    padding: 2rem 1rem;

    .container .projects-grid {
      grid-template-columns: 1fr;
      gap: 1.5rem;
    }
  }

  .project-card .project-image {
    height: 200px;
  }
}
</style>

<style>
/* Global Leaflet styles (will be uncommented after installing Leaflet) */
/*
@import 'leaflet/dist/leaflet.css';

.custom-marker .marker-pin {
  width: 30px;
  height: 30px;
  border-radius: 50% 50% 50% 0;
  position: relative;
  transform: rotate(-45deg);
  display: flex;
  align-items: center;
  justify-content: center;
  border: 2px solid white;
  box-shadow: 0 2px 8px rgba(0,0,0,0.3);
}

.custom-marker .marker-pin i {
  transform: rotate(45deg);
  color: white;
  font-size: 16px;
}

.map-popup {
  max-width: 300px;
}

.map-popup .popup-image {
  width: 100%;
  height: 150px;
  object-fit: cover;
  border-radius: 8px;
  margin-bottom: 10px;
}

.map-popup h3 {
  margin: 0 0 5px 0;
  color: #0A400C;
}

.map-popup .popup-location {
  color: #819067;
  font-size: 0.9rem;
  margin-bottom: 10px;
}

.map-popup .popup-description {
  font-size: 0.85rem;
  line-height: 1.4;
  margin-bottom: 10px;
}

.map-popup .popup-stats {
  display: flex;
  flex-direction: column;
  gap: 5px;
  font-size: 0.8rem;
  color: #819067;
}
*/
</style>