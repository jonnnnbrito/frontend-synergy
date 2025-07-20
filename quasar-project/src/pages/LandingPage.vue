<template>
  <q-page class="landing-page">
    <!-- Hero Section -->
    <section class="hero-section bg-gradient-to-r from-primary to-secondary text-white">
      <div class="container q-pa-xl">
        <div class="row items-center">
          <div class="col-12 col-md-6">
            <h1 class="text-h2 text-weight-bold q-mb-md">
              Welcome to Synergy
            </h1>
            <p class="text-h6 q-mb-xl opacity-90">
              Streamline your workflow, enhance collaboration, and achieve more together.
              The all-in-one platform for modern teams.
            </p>
            <div class="q-gutter-md">
              <q-btn
                size="lg"
                color="white"
                text-color="primary"
                label="Get Started"
                no-caps
                class="q-px-xl"
                @click="scrollToFeatures"
              />
              <q-btn
                size="lg"
                outline
                color="white"
                label="Learn More"
                no-caps
                class="q-px-xl"
                @click="scrollToAbout"
              />
            </div>
          </div>
          <div class="col-12 col-md-6 text-center">
            <q-img
              src="https://via.placeholder.com/500x400/1976D2/FFFFFF?text=Synergy+Dashboard"
              alt="Synergy Dashboard Preview"
              class="hero-image rounded-borders shadow-5"
              style="max-width: 500px"
            />
          </div>
        </div>
      </div>
    </section>

    <!-- Features Section -->
    <section id="features" class="features-section q-pa-xl">
      <div class="container">
        <div class="text-center q-mb-xl">
          <h2 class="text-h3 text-weight-bold q-mb-md">Powerful Features</h2>
          <p class="text-h6 text-grey-7">Everything you need to supercharge your productivity</p>
        </div>
        
        <div class="row q-gutter-lg">
          <div class="col-12 col-md-4" v-for="feature in features" :key="feature.id">
            <q-card class="feature-card full-height" flat bordered>
              <q-card-section class="text-center">
                <q-icon :name="feature.icon" size="64px" :color="feature.color" class="q-mb-md" />
                <h3 class="text-h5 text-weight-bold q-mb-sm">{{ feature.title }}</h3>
                <p class="text-body1 text-grey-7">{{ feature.description }}</p>
              </q-card-section>
            </q-card>
          </div>
        </div>
      </div>
    </section>

    <!-- About Section -->
    <section id="about" class="about-section bg-grey-1 q-pa-xl">
      <div class="container">
        <div class="row items-center">
          <div class="col-12 col-md-6">
            <q-img
              src="https://via.placeholder.com/400x300/F5F5F5/666666?text=Team+Collaboration"
              alt="Team Collaboration"
              class="rounded-borders"
            />
          </div>
          <div class="col-12 col-md-6 q-pl-xl">
            <h2 class="text-h3 text-weight-bold q-mb-md">Built for Modern Teams</h2>
            <p class="text-h6 q-mb-lg text-grey-7">
              Synergy brings together all the tools your team needs in one unified platform.
              From project management to real-time collaboration, we've got you covered.
            </p>
            <div class="q-gutter-sm">
              <div class="row items-center q-mb-sm" v-for="benefit in benefits" :key="benefit">
                <q-icon name="check_circle" color="positive" class="q-mr-sm" />
                <span class="text-body1">{{ benefit }}</span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- CTA Section -->
    <section class="cta-section bg-primary text-white q-pa-xl">
      <div class="container text-center">
        <h2 class="text-h3 text-weight-bold q-mb-md">Ready to Get Started?</h2>
        <p class="text-h6 q-mb-xl opacity-90">
          Join thousands of teams already using Synergy to achieve their goals.
        </p>
        <q-btn
          size="xl"
          color="white"
          text-color="primary"
          label="Start Your Free Trial"
          no-caps
          class="q-px-xl"
          @click="navigateToSignup"
        />
      </div>
    </section>

    <!-- Footer -->
    <footer class="bg-grey-9 text-white q-pa-lg">
      <div class="container">
        <div class="row">
          <div class="col-12 col-md-4">
            <h4 class="text-h5 text-weight-bold q-mb-md">Synergy</h4>
            <p class="text-body2 opacity-80">
              Empowering teams to achieve more through seamless collaboration and intelligent workflow management.
            </p>
          </div>
          <div class="col-12 col-md-2">
            <h5 class="text-h6 text-weight-bold q-mb-md">Product</h5>
            <div class="column q-gutter-xs">
              <a href="#" class="text-white opacity-80 text-decoration-none">Features</a>
              <a href="#" class="text-white opacity-80 text-decoration-none">Pricing</a>
              <a href="#" class="text-white opacity-80 text-decoration-none">Security</a>
            </div>
          </div>
          <div class="col-12 col-md-2">
            <h5 class="text-h6 text-weight-bold q-mb-md">Company</h5>
            <div class="column q-gutter-xs">
              <a href="#" class="text-white opacity-80 text-decoration-none">About</a>
              <a href="#" class="text-white opacity-80 text-decoration-none">Careers</a>
              <a href="#" class="text-white opacity-80 text-decoration-none">Contact</a>
            </div>
          </div>
          <div class="col-12 col-md-4">
            <h5 class="text-h6 text-weight-bold q-mb-md">Stay Updated</h5>
            <div class="row q-gutter-sm">
              <q-input
                v-model="email"
                placeholder="Enter your email"
                dark
                outlined
                dense
                class="col"
              />
              <q-btn color="primary" label="Subscribe" no-caps />
            </div>
          </div>
        </div>
        <q-separator class="q-my-lg" dark />
        <div class="text-center">
          <p class="text-body2 opacity-60">
            © 2025 Synergy. All rights reserved.
          </p>
        </div>
      </div>
    </footer>
  </q-page>
</template>

<script setup>
import { ref } from 'vue'

const email = ref('')

const features = [
  {
    id: 1,
    title: 'Project Management',
    description: 'Organize tasks, set deadlines, and track progress with intuitive project boards.',
    icon: 'assignment',
    color: 'primary'
  },
  {
    id: 2,
    title: 'Team Collaboration',
    description: 'Real-time chat, file sharing, and collaborative workspaces for seamless teamwork.',
    icon: 'groups',
    color: 'secondary'
  },
  {
    id: 3,
    title: 'Analytics & Insights',
    description: 'Powerful reporting tools to understand team performance and optimize workflows.',
    icon: 'analytics',
    color: 'accent'
  },
  {
    id: 4,
    title: 'Integrations',
    description: 'Connect with your favorite tools and streamline your existing workflow.',
    icon: 'extension',
    color: 'positive'
  },
  {
    id: 5,
    title: 'Security',
    description: 'Enterprise-grade security with role-based access control and data encryption.',
    icon: 'security',
    color: 'warning'
  },
  {
    id: 6,
    title: 'Mobile Ready',
    description: 'Access your workspace from anywhere with our responsive mobile-first design.',
    icon: 'phone_android',
    color: 'info'
  }
]

const benefits = [
  'Increase team productivity by 40%',
  'Reduce project delivery time',
  'Improve communication and transparency',
  'Scale with your growing business',
  '99.9% uptime guarantee'
]

function scrollToFeatures() {
  document.getElementById('features')?.scrollIntoView({ behavior: 'smooth' })
}

function scrollToAbout() {
  document.getElementById('about')?.scrollIntoView({ behavior: 'smooth' })
}

function navigateToSignup() {
  // Navigate to signup page
  console.log('Navigate to signup')
}
</script>

<style lang="scss" scoped>
.landing-page {
  .hero-section {
    min-height: 100vh;
    display: flex;
    align-items: center;
    background: linear-gradient(135deg, var(--q-primary) 0%, var(--q-secondary) 100%);
  }

  .hero-image {
    transition: transform 0.3s ease;
    
    &:hover {
      transform: scale(1.05);
    }
  }

  .feature-card {
    transition: all 0.3s ease;
    
    &:hover {
      transform: translateY(-4px);
      box-shadow: 0 8px 24px rgba(0, 0, 0, 0.12);
    }
  }

  .container {
    max-width: 1200px;
    margin: 0 auto;
  }

  .bg-gradient-to-r {
    background: linear-gradient(135deg, var(--q-primary) 0%, var(--q-secondary) 100%);
  }
}

@media (max-width: 768px) {
  .hero-section {
    min-height: auto;
    padding: 2rem 0;
    
    .row {
      flex-direction: column-reverse;
    }
    
    .hero-image {
      margin-bottom: 2rem;
    }
  }
  
  .about-section .q-pl-xl {
    padding-left: 0 !important;
    margin-top: 2rem;
  }
}
</style>