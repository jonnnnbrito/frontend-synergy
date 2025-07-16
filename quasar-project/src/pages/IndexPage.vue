<template>
  <q-page>
    <!-- Hero Section -->
    <section id="home" class="hero-section bg-primary text-white">
      <div class="container q-py-xl">
        <div class="row items-center">
          <div class="col-md-6 col-12">
            <h1 class="text-h2 text-weight-bold q-mb-md">
              Welcome to Synergy
            </h1>
            <p class="text-h6 q-mb-lg">
              We create innovative solutions that drive your business forward
            </p>
            <div class="q-gutter-md">
              <q-btn 
                size="lg" 
                color="white" 
                text-color="primary" 
                label="Get Started"
                @click="scrollToSection('contact')"
              />
              <q-btn 
                size="lg" 
                outline 
                color="white" 
                label="Learn More"
                @click="scrollToSection('about')"
              />
            </div>
          </div>
          <div class="col-md-6 col-12 text-center">
            <q-img
              src="~assets/quasar-logo-vertical.svg"
              style="width: 300px; height: 300px"
              class="q-mt-md"
            />
          </div>
        </div>
      </div>
    </section>

    <!-- About Section -->
    <section id="about" class="q-py-xl">
      <div class="container">
        <div class="text-center q-mb-xl">
          <h2 class="text-h3 text-weight-bold q-mb-md">About Us</h2>
          <p class="text-h6 text-grey-7">
            Discover what makes us unique
          </p>
        </div>
        
        <div class="row q-col-gutter-lg">
          <div class="col-md-4 col-12">
            <q-card class="full-height">
              <q-card-section class="text-center">
                <q-icon name="lightbulb" size="3rem" color="primary" />
                <h3 class="text-h5 q-mt-md">Innovation</h3>
                <p>We bring fresh ideas and cutting-edge solutions to every project</p>
              </q-card-section>
            </q-card>
          </div>
          
          <div class="col-md-4 col-12">
            <q-card class="full-height">
              <q-card-section class="text-center">
                <q-icon name="speed" size="3rem" color="primary" />
                <h3 class="text-h5 q-mt-md">Efficiency</h3>
                <p>Fast delivery without compromising on quality and attention to detail</p>
              </q-card-section>
            </q-card>
          </div>
          
          <div class="col-md-4 col-12">
            <q-card class="full-height">
              <q-card-section class="text-center">
                <q-icon name="support" size="3rem" color="primary" />
                <h3 class="text-h5 q-mt-md">Support</h3>
                <p>24/7 customer support to ensure your success every step of the way</p>
              </q-card-section>
            </q-card>
          </div>
        </div>
      </div>
    </section>

    <!-- Services Section -->
    <section id="services" class="bg-grey-1 q-py-xl">
      <div class="container">
        <div class="text-center q-mb-xl">
          <h2 class="text-h3 text-weight-bold q-mb-md">Our Services</h2>
          <p class="text-h6 text-grey-7">
            Comprehensive solutions for your business needs
          </p>
        </div>
        
        <div class="row q-col-gutter-lg">
          <div class="col-md-6 col-12" v-for="service in services" :key="service.title">
            <q-card class="full-height">
              <q-card-section>
                <div class="row items-center q-mb-md">
                  <q-icon :name="service.icon" size="2rem" color="primary" class="q-mr-md" />
                  <h3 class="text-h5">{{ service.title }}</h3>
                </div>
                <p>{{ service.description }}</p>
              </q-card-section>
              <q-card-actions>
                <q-btn flat color="primary" label="Learn More" />
              </q-card-actions>
            </q-card>
          </div>
        </div>
      </div>
    </section>

    <!-- Team Section -->
    <section id="team" class="q-py-xl">
      <div class="container">
        <div class="text-center q-mb-xl">
          <h2 class="text-h3 text-weight-bold q-mb-md">Our Team</h2>
          <p class="text-h6 text-grey-7">
            Meet the talented people behind our success
          </p>
        </div>
        
        <div class="row q-col-gutter-lg">
          <div class="col-md-4 col-12" v-for="member in team" :key="member.name">
            <q-card class="text-center">
              <q-card-section>
                <q-avatar size="100px" class="q-mb-md">
                  <img :src="member.avatar" :alt="member.name">
                </q-avatar>
                <h3 class="text-h5">{{ member.name }}</h3>
                <p class="text-subtitle1 text-primary">{{ member.role }}</p>
                <p class="text-grey-7">{{ member.bio }}</p>
              </q-card-section>
            </q-card>
          </div>
        </div>
      </div>
    </section>

    <!-- Contact Section -->
    <section id="contact" class="bg-grey-1 q-py-xl">
      <div class="container">
        <div class="text-center q-mb-xl">
          <h2 class="text-h3 text-weight-bold q-mb-md">Get In Touch</h2>
          <p class="text-h6 text-grey-7">
            Ready to start your project? Let's talk!
          </p>
        </div>
        
        <div class="row q-col-gutter-lg">
          <div class="col-md-6 col-12">
            <q-card>
              <q-card-section>
                <h3 class="text-h5 q-mb-md">Contact Information</h3>
                
                <div class="q-mb-md">
                  <div class="row items-center q-mb-sm">
                    <q-icon name="phone" class="q-mr-sm" />
                    <span>+1 (555) 123-4567</span>
                  </div>
                  <div class="row items-center q-mb-sm">
                    <q-icon name="email" class="q-mr-sm" />
                    <span>hello@synergy.com</span>
                  </div>
                  <div class="row items-center q-mb-sm">
                    <q-icon name="location_on" class="q-mr-sm" />
                    <span>123 Business Street, City, State 12345</span>
                  </div>
                </div>
              </q-card-section>
            </q-card>
          </div>
          
          <div class="col-md-6 col-12">
            <q-card>
              <q-card-section>
                <h3 class="text-h5 q-mb-md">Send Message</h3>
                <q-form @submit="submitForm">
                  <q-input
                    v-model="form.name"
                    label="Your Name"
                    filled
                    class="q-mb-md"
                    required
                  />
                  <q-input
                    v-model="form.email"
                    label="Your Email"
                    type="email"
                    filled
                    class="q-mb-md"
                    required
                  />
                  <q-input
                    v-model="form.message"
                    label="Message"
                    type="textarea"
                    filled
                    rows="4"
                    class="q-mb-md"
                    required
                  />
                  <q-btn 
                    type="submit" 
                    color="primary" 
                    label="Send Message"
                    class="full-width"
                  />
                </q-form>
              </q-card-section>
            </q-card>
          </div>
        </div>
      </div>
    </section>
  </q-page>
</template>

<script setup>
import { ref } from 'vue'
import { useQuasar } from 'quasar'

const $q = useQuasar()

const form = ref({
  name: '',
  email: '',
  message: ''
})

const services = [
  {
    title: 'Web Development',
    icon: 'web',
    description: 'Modern, responsive websites and web applications built with the latest technologies.'
  },
  {
    title: 'Mobile Apps',
    icon: 'phone_android',
    description: 'Native and cross-platform mobile applications for iOS and Android.'
  },
  {
    title: 'UI/UX Design',
    icon: 'design_services',
    description: 'Beautiful, user-friendly interfaces that enhance user experience.'
  },
  {
    title: 'Consulting',
    icon: 'psychology',
    description: 'Strategic technology consulting to help your business grow and succeed.'
  }
]

const team = [
  {
    name: 'John Doe',
    role: 'CEO & Founder',
    bio: 'Passionate about technology and innovation with 10+ years of experience.',
    avatar: 'https://cdn.quasar.dev/img/avatar2.jpg'
  },
  {
    name: 'Jane Smith',
    role: 'CTO',
    bio: 'Technical leader with expertise in full-stack development and architecture.',
    avatar: 'https://cdn.quasar.dev/img/avatar3.jpg'
  },
  {
    name: 'Mike Johnson',
    role: 'Lead Designer',
    bio: 'Creative designer focused on user experience and modern design principles.',
    avatar: 'https://cdn.quasar.dev/img/avatar.jpg'
  }
]

function scrollToSection(section) {
  const element = document.getElementById(section)
  if (element) {
    element.scrollIntoView({ behavior: 'smooth' })
  }
}

function submitForm() {
  $q.notify({
    message: 'Message sent successfully!',
    color: 'positive',
    position: 'top'
  })
  
  form.value = {
    name: '',
    email: '',
    message: ''
  }
}
</script>

<style scoped>
.hero-section {
  min-height: 100vh;
  display: flex;
  align-items: center;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;
}

section {
  scroll-margin-top: 70px;
}
</style>
