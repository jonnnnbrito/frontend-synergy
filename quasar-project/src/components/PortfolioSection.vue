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
              @click.prevent="handleFilterClick(filter.value)"
            >
              {{ filter.label }}
            </button>
          </div>
        </div>

        <!-- Interactive Map -->
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

          <!-- Mobile Map Overlay -->
          <div v-if="!mapEnabled && isMobile" class="map-overlay" @click="enableMap">
            <div class="map-overlay-content">
              <q-icon name="touch_app" size="2rem" color="white" />
              <p>Tap to enable map</p>
            </div>
          </div>

          <!-- Mobile Map Disable Button -->
          <div v-if="mapEnabled && isMobile" class="map-disable-btn" @click="disableMap">
            <q-icon name="close" size="1.5rem" color="white" />
          </div>
        </div>

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
import { ref, computed, watch, onMounted, nextTick } from 'vue'
import 'leaflet/dist/leaflet.css'

const map = ref(null)
const mapContainer = ref(null)
const mapLoading = ref(true)
const mapEnabled = ref(false)
const isMobile = ref(false)
const selectedFilter = ref('all')
const pendingProject = ref(null)

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
    name: 'Boracay Beach Resort Complex',
    type: 'residential',
    location: 'Boracay, Aklan',
    lat: 11.9674,
    lng: 121.9248,
    image: 'https://images.unsplash.com/photo-1559827260-dc66d52bef19?w=600&h=400&fit=crop',
    size: '50,000 sq ft',
    duration: '18 months',
    year: '2023',
    description: 'Luxury beachfront resort complex with sustainable tropical design and ocean views.'
  },
  {
    id: 2,
    name: 'Makati Business Tower',
    type: 'commercial',
    location: 'Makati, Metro Manila',
    lat: 14.5547,
    lng: 121.0244,
    image: 'https://images.unsplash.com/photo-1582407947304-fd86f028f716?w=600&h=400&fit=crop',
    size: '75,000 sq ft',
    duration: '24 months',
    year: '2022',
    description: 'Modern high-rise office building in Manila\'s premier business district.'
  },
  {
    id: 3,
    name: 'Cebu Industrial Complex',
    type: 'industrial',
    location: 'Cebu City, Cebu',
    lat: 10.3157,
    lng: 123.8854,
    image: 'https://images.unsplash.com/photo-1504307651254-35680f356dfd?w=600&h=400&fit=crop',
    size: '100,000 sq ft',
    duration: '30 months',
    year: '2021',
    description: 'State-of-the-art manufacturing facility in the Queen City of the South.'
  },
  {
    id: 4,
    name: 'El Nido Eco Resort',
    type: 'commercial',
    location: 'El Nido, Palawan',
    lat: 11.1949,
    lng: 119.4013,
    image: 'https://images.unsplash.com/photo-1571896349842-33c89424de2d?w=600&h=400&fit=crop',
    size: '120,000 sq ft',
    duration: '36 months',
    year: '2023',
    description: 'Sustainable eco-tourism resort nestled in Palawan\'s pristine natural beauty.'
  },
  {
    id: 5,
    name: 'Bohol Heritage Village',
    type: 'residential',
    location: 'Bohol Island',
    lat: 9.8349,
    lng: 124.1436,
    image: 'https://images.unsplash.com/photo-1512100356356-de1b84283e18?w=600&h=400&fit=crop',
    size: '25 homes',
    duration: '24 months',
    year: '2022',
    description: 'Cultural heritage-inspired residential community near the famous Chocolate Hills.'
  },
  {
    id: 6,
    name: 'Davao Corporate Center',
    type: 'commercial',
    location: 'Davao City, Davao',
    lat: 7.0731,
    lng: 125.6128,
    image: 'https://images.unsplash.com/photo-1580587771525-78b9dba3b914?w=600&h=400&fit=crop',
    size: '90,000 sq ft',
    duration: '28 months',
    year: '2023',
    description: 'Modern corporate headquarters in the gateway to Mindanao.'
  }
])

// Computed filtered projects
const filteredProjects = computed(() => {
  if (selectedFilter.value === 'all') {
    return projects.value
  }
  return projects.value.filter(project => project.type === selectedFilter.value)
})

// Watch for filter changes and update map
watch(selectedFilter, () => {
  // Add small delay to prevent Brave's flash
  requestAnimationFrame(() => {
    if (window.updateMapMarkers) {
      window.updateMapMarkers()
    }
  })
})

// Map initialization
const initializeMap = async () => {
  try {
    const L = await import('leaflet')

    if (!mapContainer.value) return

    // Fix for default markers
    delete L.Icon.Default.prototype._getIconUrl
    L.Icon.Default.mergeOptions({
      iconRetinaUrl: 'https://cdnjs.cloudflare.com/ajax/libs/leaflet/1.7.1/images/marker-icon-2x.png',
      iconUrl: 'https://cdnjs.cloudflare.com/ajax/libs/leaflet/1.7.1/images/marker-icon.png',
      shadowUrl: 'https://cdnjs.cloudflare.com/ajax/libs/leaflet/1.7.1/images/marker-shadow.png',
    })

    map.value = L.map(mapContainer.value).setView([12.8797, 121.7740], 6)

    L.tileLayer('https://{s}.basemaps.cartocdn.com/rastertiles/voyager/{z}/{x}/{y}{r}.png', {
      attribution: '© OpenStreetMap contributors © CARTO',
      maxZoom: 18
    }).addTo(map.value)

    const markerColors = {
      residential: '#4CAF50',
      commercial: '#2196F3',
      industrial: '#FF9800'
    }

    // Create marker layer group for easy management
    const markerLayer = L.layerGroup().addTo(map.value)
    
    const updateMapMarkers = () => {
      markerLayer.clearLayers()
      window.projectMarkers = {}
      
      filteredProjects.value.forEach(project => {
        const marker = L.circleMarker([project.lat, project.lng], {
          radius: 8,
          fillColor: markerColors[project.type],
          color: '#fff',
          weight: 2,
          opacity: 1,
          fillOpacity: 0.8
        }).addTo(markerLayer)

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
          maxWidth: window.innerWidth <= 768 ? 200 : 250,
          className: 'custom-popup'
        })

        // Store marker reference for project card clicks
        window.projectMarkers[project.id] = marker
      })
    }

    // Initial markers
    updateMapMarkers()
    
    // Watch for filter changes and update markers
    window.updateMapMarkers = updateMapMarkers

    mapLoading.value = false

    // Check if mobile and disable map interaction
    isMobile.value = window.innerWidth <= 768
    if (isMobile.value) {
      map.value.dragging.disable()
      map.value.touchZoom.disable()
      map.value.doubleClickZoom.disable()
      map.value.scrollWheelZoom.disable()
      mapEnabled.value = false
    } else {
      // Desktop: Enable all map interactions
      mapEnabled.value = true
      map.value.dragging.enable()
      map.value.touchZoom.enable()
      map.value.doubleClickZoom.enable()
      map.value.scrollWheelZoom.enable()
    }

  } catch (error) {
    console.error('Error initializing map:', error)
    mapLoading.value = false
  }
}

// Enable map interaction on mobile
const enableMap = () => {
  if (map.value && isMobile.value) {
    mapEnabled.value = true
    map.value.dragging.enable()
    map.value.touchZoom.enable()
    map.value.doubleClickZoom.enable()
    map.value.scrollWheelZoom.enable()
    
    // Continue with pending project interaction if exists
    if (pendingProject.value && window.projectMarkers && window.projectMarkers[pendingProject.value.id]) {
      setTimeout(() => {
        map.value.setView([pendingProject.value.lat, pendingProject.value.lng], 12, { animate: true })
        setTimeout(() => {
          window.projectMarkers[pendingProject.value.id].openPopup()
          pendingProject.value = null // Clear pending project
        }, 500)
      }, 300)
    }
  }
}

// Disable map interaction on mobile
const disableMap = () => {
  if (map.value && isMobile.value) {
    mapEnabled.value = false
    map.value.dragging.disable()
    map.value.touchZoom.disable()
    map.value.doubleClickZoom.disable()
    map.value.scrollWheelZoom.disable()
  }
}

// Handle filter clicks for Brave browser compatibility
const handleFilterClick = (filterValue) => {
  // Prevent any default behavior that might cause flash
  if (selectedFilter.value !== filterValue) {
    selectedFilter.value = filterValue
  }
}

// Focus project on map
const focusProjectOnMap = (project) => {
  if (map.value && window.projectMarkers && window.projectMarkers[project.id]) {
    // Check if mobile (screen width <= 768px)
    const isMobileScreen = window.innerWidth <= 768
    
    // On mobile: Navigate to portfolio section first, then map interaction
    if (isMobileScreen) {
      const portfolioElement = document.getElementById('portfolio')
      if (portfolioElement) {
        portfolioElement.scrollIntoView({ behavior: 'smooth', block: 'start' })
        
        // After scrolling, provide visual feedback
        setTimeout(() => {
          if (!mapEnabled.value) {
            // Store the project for later interaction
            pendingProject.value = project
            
            // Show visual feedback - highlight the overlay
            const overlay = document.querySelector('.map-overlay')
            if (overlay) {
              overlay.style.animation = 'pulse 2s ease-in-out 3 times'
              overlay.style.background = 'rgba(129, 144, 103, 0.85)' // Slightly more visible
              
              // Reset after animation
              setTimeout(() => {
                overlay.style.animation = ''
                overlay.style.background = 'rgba(129, 144, 103, 0.7)'
              }, 6000)
            }
          } else {
            // Map already enabled, proceed normally
            map.value.setView([project.lat, project.lng], 12, { animate: true })
            setTimeout(() => {
              window.projectMarkers[project.id].openPopup()
            }, 500)
          }
        }, 800) // Wait for scroll to finish
      }
    } else {
      // Desktop: Navigate to portfolio section first, then map interaction
      const portfolioElement = document.getElementById('portfolio')
      if (portfolioElement) {
        portfolioElement.scrollIntoView({ behavior: 'smooth', block: 'start' })
        
        // After scrolling, zoom and show popup
        setTimeout(() => {
          map.value.setView([project.lat, project.lng], 12, { animate: true })
          setTimeout(() => {
            window.projectMarkers[project.id].openPopup()
          }, 500)
        }, 800) // Wait for scroll to finish
      }
    }
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
      outline: none !important;
      -webkit-tap-highlight-color: transparent;
      user-select: none;

      &:focus {
        outline: none !important;
        box-shadow: none !important;
      }

      &:active {
        outline: none !important;
        box-shadow: none !important;
      }

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
    right: 1rem;
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
    transition: opacity 0.3s ease;
  }
}

// Project Cards
.project-card {
  background: white;
  border-radius: 15px;
  overflow: hidden;
  box-shadow: 0 8px 25px rgba($primary-green, 0.1);
  transition: all 0.3s ease, opacity 0.3s ease;
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
    height: 40vh;
    min-height: 250px;
    margin-bottom: 2rem;
    border-radius: 10px;
  }

  .map-info {
    display: none;
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

  .project-card {
    .project-image {
      height: 200px;
    }

    .project-info {
      padding: 1rem;

      .project-name {
        font-size: 1rem;
        line-height: 1.3;
      }

      .project-stats {
        flex-direction: column;
        gap: 0.5rem;
        
        .stat {
          font-size: 0.85rem;
        }
      }
    }
  }

  // Add swipe functionality for mobile
  .projects-grid {
    overflow-x: auto;
    scroll-snap-type: x mandatory;
    display: flex;
    gap: 1rem;
    padding-bottom: 1rem;

    .project-card {
      min-width: 280px;
      scroll-snap-align: start;
      flex-shrink: 0;
    }
  }

  // Mobile Map Overlay
  .map-overlay {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: rgba($sage-green, 0.7);
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    border-radius: 0;
    z-index: 1001;

    .map-overlay-content {
      text-align: center;
      color: white;

      p {
        margin-top: 0.5rem;
        font-size: 1rem;
        font-weight: 500;
      }
    }
  }

  // Mobile Map Disable Button
  .map-disable-btn {
    position: absolute;
    top: 1rem;
    right: 1rem;
    background: rgba($primary-green, 0.9);
    border-radius: 50%;
    width: 40px;
    height: 40px;
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    z-index: 1002;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.2);

    &:hover {
      background: $primary-green;
    }
  }
}

// Extra small screens - better filter button layout
@media (max-width: 476px) {
  .portfolio-section {
    padding: 3rem 0;

    .portfolio-content .container {
      padding: 0 1rem;
    }
  }

  .filter-controls {
    margin-bottom: 2rem;

    .filter-buttons {
      padding: 3px;
      border-radius: 18px;
      transform: scale(0.85);

      .filter-btn {
        padding: 0.5rem 0.9rem;
        font-size: 0.75rem;
        border-radius: 15px;
      }
    }
  }

  .section-header {
    margin-bottom: 2rem;

    .section-title {
      font-size: 2rem;
    }

    .section-subtitle {
      font-size: 1rem;
      padding: 0 1rem;
    }
  }

  .map-container {
    height: 35vh;
    min-height: 200px;
    margin-bottom: 1.5rem;
  }

  .featured-projects {
    .featured-title {
      font-size: 1.5rem;
      margin-bottom: 1.5rem;
    }

    .projects-grid {
      gap: 0.8rem;
      padding-bottom: 0.5rem;

      .project-card {
        min-width: 260px;
      }
    }
  }
}

// Pulse animation for map overlay
@keyframes pulse {
  0% { transform: scale(1); opacity: 0.7; }
  50% { transform: scale(1.02); opacity: 0.9; }
  100% { transform: scale(1); opacity: 0.7; }
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

/* Mobile popup scaling */
@media (max-width: 768px) {
  .map-popup .popup-image {
    height: 80px;
  }

  .map-popup h4 {
    font-size: 0.9rem;
  }

  .map-popup p {
    font-size: 0.75rem;
    margin: 2px 0;
  }
}
</style>
