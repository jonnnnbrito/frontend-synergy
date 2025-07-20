<template>
  <section class="hero-section">
    <div class="hero-overlay"></div>
    <div class="hero-content">
      <div class="container q-pa-xl">
        <div class="row items-center">
          <div class="col-12 col-md-8 col-lg-6">
            <div class="hero-badge q-mb-lg">
              <q-chip
                style="background: #0A400C; color: #FEFAE0;"
              >
                <q-icon name="verified" color="#FEFAE0" class="q-mr-md" /> 35+ Years of Engineering Expertise
              </q-chip>
            </div>
            <h1 class="hero-title q-mb-md">
              <span class="company-name">Synergy Industrial Builders:</span><br>
              <span class="tagline">Engineering Excellence, Delivering Results</span>
            </h1>
            <p class="hero-subtitle q-mb-xl">
              Your trusted construction partner for residential, commercial, and industrial projects.
              We deliver quality craftsmanship with innovative solutions and reliable service.
            </p>
            <div class="hero-actions q-gutter-md">
              <q-btn
                size="lg"
                style="background: #0A400C; color: #FEFAE0;"
                label="Get Free Quote"
                no-caps
                class="q-px-xl hero-btn-primary"
                icon="calculate"
                @click="scrollToContact"
              />
              <q-btn
                size="lg"
                outline
                style="border-color: #819067; color: #819067;"
                label="View Projects"
                no-caps
                class="q-px-xl hero-btn-secondary"
                icon="photo_library"
                @click="scrollToProjects"
              />
            </div>

            <!-- Stats Row -->
            <div class="stats-row q-mt-xl">
              <div class="row q-gutter-xl">
                <div class="stat-item">
                  <div class="stat-number" style="color: #0A400C;">200+</div>
                  <div class="stat-label" style="color: #819067;">Projects Completed</div>
                </div>
                <div class="stat-item">
                  <div class="stat-number" style="color: #0A400C;">98%</div>
                  <div class="stat-label" style="color: #819067;">Client Satisfaction</div>
                </div>
                <div class="stat-item">
                  <div class="stat-number" style="color: #0A400C;">35+</div>
                  <div class="stat-label" style="color: #819067;">Years Experience</div>
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
function scrollToProjects() {
  document.getElementById('services')?.scrollIntoView({ behavior: 'smooth' })
}

function scrollToContact() {
  console.log('Navigate to contact')
}
</script>

<style lang="scss" scoped>
.hero-section {
  min-height: 100vh;
  position: relative;
  display: flex;
  align-items: center;

  &::before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: url('https://images.unsplash.com/photo-1541888946425-d81bb19240f5?q=80&w=2070&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D') center/cover;
    filter: grayscale(100%);
    z-index: 0;
  }
}

.hero-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: linear-gradient(
    135deg,
    rgba(254, 250, 224, 0.9) 0%,
    rgba(245, 243, 232, 0.88) 25%,
    rgba(232, 230, 211, 0.87) 50%,
    rgba(212, 210, 191, 0.86) 75%,
    rgba(177, 171, 134, 0.85) 100%
  );
}

.hero-content {
  position: relative;
  z-index: 2;
  width: 100%;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
}

.hero-title {
  font-size: 3.5rem;
  line-height: 1.1;
  font-weight: 800;
  color: #0A400C;
}

.company-name {
  color: #0A400C;
  position: relative;
  white-space: nowrap;
  font-weight: 900;
}

.tagline {
  color: #819067;
  position: relative;
  font-weight: 600;
}

.hero-subtitle {
  font-size: 1.2rem;
  line-height: 1.6;
  color: #0A400C;
  opacity: 0.8;
}

.hero-btn-primary {
  font-weight: 600;
  border-radius: 50px;
  text-transform: none;
  transition: all 0.3s ease;
  box-shadow: 0 4px 15px rgba(10, 64, 12, 0.2);

  &:hover {
    transform: translateY(-2px);
    box-shadow: 0 8px 25px rgba(10, 64, 12, 0.3);
    background: #819067 !important;
    color: #FEFAE0 !important;
  }
}

.hero-btn-secondary {
  font-weight: 600;
  border-radius: 50px;
  text-transform: none;
  border: 2px solid #819067;
  background: transparent;

  &:hover {
    background: #819067 !important;
    color: #FEFAE0 !important;
    border-color: #819067 !important;
    transform: translateY(-2px);
    box-shadow: 0 8px 25px rgba(129, 144, 103, 0.3);
  }
}

.stats-row {
  .stat-item {
    text-align: left;
  }

  .stat-number {
    font-size: 2.5rem;
    font-weight: 800;
    line-height: 1;
  }

  .stat-label {
    font-size: 0.9rem;
    opacity: 0.8;
    margin-top: 4px;
  }
}

// Mobile Responsive
@media (max-width: 768px) {
  .hero-title {
    font-size: 2rem;
  }

  .hero-subtitle {
    font-size: 1rem;
  }

  .stats-row {
    .row {
      justify-content: center;
      text-align: center;
    }

    .stat-item {
      text-align: center;
      margin-bottom: 1rem;
    }
  }

  .hero-actions {
    .q-btn {
      width: 100%;
      margin-bottom: 10px;
    }
  }
}
</style>
