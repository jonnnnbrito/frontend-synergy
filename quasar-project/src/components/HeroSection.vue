<template>
  <section class="hero-section">
    <div class="hero-overlay"></div>
    <div class="hero-content">
      <div class="container q-pa-xl">
        <div class="row items-center">
          <div class="col-12 col-md-8 col-lg-6">
            <div class="hero-badge q-mb-lg">
              <q-chip color="orange" text-color="white" icon="verified" label="35+ Years of Engineering Expertise" />
            </div>
            <h1 class="hero-title text-white q-mb-md">
              Building Dreams,<br>
              <span class="text-orange">Creating Reality</span>
            </h1>
            <p class="hero-subtitle text-white q-mb-xl">
              Your trusted construction partner for residential, commercial, and industrial projects.
              We deliver quality craftsmanship with innovative solutions and reliable service.
            </p>
            <div class="hero-actions q-gutter-md">
              <q-btn
                size="lg"
                color="orange"
                label="Get Free Quote"
                no-caps
                class="q-px-xl hero-btn-primary"
                icon="calculate"
                @click="scrollToContact"
              />
              <q-btn
                size="lg"
                outline
                color="white"
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
                  <div class="stat-number text-orange">500+</div>
                  <div class="stat-label text-white">Projects Completed</div>
                </div>
                <div class="stat-item">
                  <div class="stat-number text-orange">98%</div>
                  <div class="stat-label text-white">Client Satisfaction</div>
                </div>
                <div class="stat-item">
                  <div class="stat-number text-orange">25+</div>
                  <div class="stat-label text-white">Years Experience</div>
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
  background: linear-gradient(
    135deg,
    rgba(10, 64, 12, 0.9) 0%,
    rgba(129, 144, 103, 0.8) 100%
  ),
  url('https://images.unsplash.com/photo-1541888946425-d81bb19240f5?q=80&w=2070&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D') center/cover;
  display: flex;
  align-items: center;
}

.hero-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: linear-gradient(
    135deg,
    rgba(10, 64, 12, 0.8) 0%,
    rgba(129, 144, 103, 0.6) 100%
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
}

.hero-subtitle {
  font-size: 1.2rem;
  line-height: 1.6;
  opacity: 0.9;
}

.hero-btn-primary {
  font-weight: 600;
  border-radius: 50px;
  text-transform: none;
  transition: all 0.3s ease;

  &:hover {
    transform: translateY(-2px);
    box-shadow: 0 8px 25px rgba(255, 102, 0, 0.3);
  }
}

.hero-btn-secondary {
  font-weight: 600;
  border-radius: 50px;
  text-transform: none;
  border: 2px solid white;

  &:hover {
    background: white;
    color: #0A400C;
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
    font-size: 2.5rem;
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
