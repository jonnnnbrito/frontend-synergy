<template>
  <section id="about-us" class="about-section">
    <!-- Left Side: Sticky Background Image -->
    <div class="left-panel">
      <div class="background-image"></div>
      <div class="image-overlay"></div>
      <div class="left-content">
        <div class="company-badge">
          <q-chip style="background: #0A400C; color: #FEFAE0;">
            <q-icon name="verified" color="#FEFAE0" class="q-mr-sm" /> 
            35+ Years of Excellence
          </q-chip>
        </div>
        <h1 class="left-title">
          Building Tomorrow,<br>
          <span class="accent-text">Today</span>
        </h1>
      </div>
    </div>

    <!-- Right Side: Flowing Content -->
    <div class="right-panel">
      <div class="scrolling-content">
        
        <!-- Header Section -->
        <div class="content-section">
          <h2 class="section-heading">About Synergy</h2>
          <p class="section-text">
            For over three decades, we've been transforming visions into reality through 
            innovative construction solutions and unwavering commitment to excellence.
          </p>
        </div>

        <!-- Stats Cards -->
        <div class="content-section">
          <div class="stats-grid">
            <div class="stat-card">
              <div class="stat-number">200+</div>
              <div class="stat-label">Projects Completed</div>
            </div>
            <div class="stat-card">
              <div class="stat-number">98%</div>
              <div class="stat-label">Client Satisfaction</div>
            </div>
            <div class="stat-card">
              <div class="stat-number">35+</div>
              <div class="stat-label">Years Experience</div>
            </div>
            <div class="stat-card">
              <div class="stat-number">50+</div>
              <div class="stat-label">Team Members</div>
            </div>
          </div>
        </div>

        <!-- Mission & Vision -->
        <div class="content-section">
          <div class="mission-vision-grid">
            <div class="mv-card">
              <q-icon name="flag" class="mv-icon" />
              <h3 class="mv-title">Our Mission</h3>
              <p class="mv-text">
                To deliver exceptional construction services that exceed expectations 
                while building lasting relationships with our clients and communities.
              </p>
            </div>
            <div class="mv-card">
              <q-icon name="visibility" class="mv-icon" />
              <h3 class="mv-title">Our Vision</h3>
              <p class="mv-text">
                To be the leading construction partner, known for innovation, 
                quality craftsmanship, and sustainable building practices.
              </p>
            </div>
          </div>
        </div>

        <!-- Values Section -->
        <div class="content-section">
          <h2 class="section-heading">Our Core Values</h2>
          <div class="values-grid">
            <div class="value-item">
              <q-icon name="lightbulb" class="value-icon" />
              <h4 class="value-title">Innovation</h4>
              <p class="value-text">Embracing cutting-edge technology and creative solutions</p>
            </div>
            <div class="value-item">
              <q-icon name="handshake" class="value-icon" />
              <h4 class="value-title">Integrity</h4>
              <p class="value-text">Building trust through honest and transparent practices</p>
            </div>
            <div class="value-item">
              <q-icon name="star" class="value-icon" />
              <h4 class="value-title">Excellence</h4>
              <p class="value-text">Delivering outstanding quality in every project</p>
            </div>
            <div class="value-item">
              <q-icon name="group" class="value-icon" />
              <h4 class="value-title">Collaboration</h4>
              <p class="value-text">Working together to achieve extraordinary results</p>
            </div>
          </div>
        </div>

        <!-- Story Section -->
        <div class="content-section">
          <h2 class="section-heading">Our Journey</h2>
          <div class="story-content">
            <p class="story-text">
              Founded in 1989, Synergy Industrial Builders began as a small family business 
              with a simple mission: to build structures that stand the test of time while 
              fostering meaningful relationships with our clients.
            </p>
            <p class="story-text">
              Over the decades, we've grown from a local contractor to a trusted partner 
              for residential, commercial, and industrial projects across the region. 
              Our success is built on the foundation of skilled craftsmanship, innovative 
              solutions, and an unwavering commitment to quality.
            </p>
            <p class="story-text">
              Today, we continue to honor our founding principles while embracing new 
              technologies and sustainable practices that benefit our clients and communities.
            </p>
          </div>
          
          <!-- CTA Section -->
          <div class="cta-section">
            <q-btn
              size="lg"
              style="background: #0A400C; color: #FEFAE0;"
              label="Start Your Project"
              no-caps
              class="cta-btn"
              icon="construction"
            />
          </div>
        </div>

      </div>
    </div>
  </section>
</template>

<script setup>
// About Us split-screen section with sticky left panel
</script>

<style lang="scss" scoped>
// Brand Colors
$primary-green: #0A400C;
$sage-green: #819067;
$cream: #FEFAE0;
$beige: #B1AB86;
$light-cream: rgba(254, 250, 224, 0.9);
$border-color: rgba(177, 171, 134, 0.3);

// Main Layout
.about-section {
  display: flex;
  min-height: 100vh;
  position: relative;
}

// Left Panel - Sticky Background
.left-panel {
  width: 50%;
  position: sticky;
  top: 0;
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 10;

  .background-image {
    position: absolute;
    inset: 0;
    background: url('https://images.unsplash.com/photo-1504307651254-35680f356dfd?q=80&w=2076&auto=format&fit=crop&ixlib=rb-4.1.0&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D') center/cover;
    filter: grayscale(50%);
  }

  .image-overlay {
    position: absolute;
    inset: 0;
    background: linear-gradient(135deg, rgba($primary-green, 0.7), rgba($sage-green, 0.6), rgba($primary-green, 0.8));
  }

  .left-content {
    position: relative;
    z-index: 2;
    text-align: center;
    padding: 2rem;

    .company-badge {
      margin-bottom: 2rem;
    }

    .left-title {
      font-size: 3.5rem;
      font-weight: 800;
      color: $cream;
      line-height: 1.1;
      text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);

      .accent-text {
        color: $beige;
        text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.4);
      }
    }
  }
}

// Right Panel - Flowing Content
.right-panel {
  width: 50%;
  background: linear-gradient(135deg, 
    rgba(254, 250, 224, 0.95), 
    rgba(245, 243, 232, 0.92), 
    rgba(232, 230, 211, 0.90), 
    rgba(212, 210, 191, 0.88), 
    rgba(177, 171, 134, 0.85)
  );
  z-index: 1;

  .scrolling-content {
    padding: 3rem 2rem;

    .content-section {
      margin-bottom: 4rem;

      .section-heading {
        font-size: 2.5rem;
        font-weight: 700;
        color: $primary-green;
        margin-bottom: 1.5rem;
      }

      .section-text {
        font-size: 1.1rem;
        color: $primary-green;
        opacity: 0.8;
        line-height: 1.7;
      }
    }
  }
}

// Stats Grid
.stats-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 1.5rem;
  margin-top: 2rem;

  .stat-card {
    background: $light-cream;
    backdrop-filter: blur(10px);
    border: 1px solid $border-color;
    border-radius: 15px;
    padding: 2rem 1.5rem;
    text-align: center;
    transition: all 0.3s ease;

    &:hover {
      transform: translateY(-5px);
      box-shadow: 0 10px 30px rgba($primary-green, 0.15);
    }

    .stat-number {
      font-size: 2.5rem;
      font-weight: 800;
      color: $primary-green;
      line-height: 1;
    }

    .stat-label {
      font-size: 0.9rem;
      color: $sage-green;
      margin-top: 0.5rem;
      opacity: 0.9;
    }
  }
}

// Mission & Vision
.mission-vision-grid {
  display: grid;
  gap: 2rem;
  margin-top: 2rem;

  .mv-card {
    background: $light-cream;
    backdrop-filter: blur(10px);
    border: 1px solid $border-color;
    border-radius: 15px;
    padding: 2rem;
    transition: all 0.3s ease;

    &:hover {
      transform: translateX(10px);
      box-shadow: 0 8px 25px rgba($primary-green, 0.15);
    }

    .mv-icon {
      font-size: 2.5rem;
      color: $primary-green;
      margin-bottom: 1rem;
    }

    .mv-title {
      font-size: 1.5rem;
      font-weight: 600;
      color: $primary-green;
      margin-bottom: 1rem;
    }

    .mv-text {
      font-size: 1rem;
      color: $sage-green;
      line-height: 1.6;
    }
  }
}

// Values Grid
.values-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 1.5rem;
  margin-top: 2rem;

  .value-item {
    text-align: center;
    padding: 1.5rem;

    .value-icon {
      font-size: 2.5rem;
      color: $primary-green;
      margin-bottom: 1rem;
      opacity: 0.8;
    }

    .value-title {
      font-size: 1.2rem;
      font-weight: 600;
      color: $primary-green;
      margin-bottom: 0.8rem;
    }

    .value-text {
      font-size: 0.9rem;
      color: $sage-green;
      line-height: 1.5;
    }
  }
}

// Story & CTA
.story-content {
  margin-top: 2rem;

  .story-text {
    font-size: 1rem;
    color: $primary-green;
    opacity: 0.8;
    line-height: 1.7;
    margin-bottom: 1.5rem;
  }
}

.cta-section {
  margin-top: 3rem;
  text-align: center;

  .cta-btn {
    font-weight: 600;
    border-radius: 50px;
    padding: 12px 30px;
    transition: all 0.3s ease;
    box-shadow: 0 4px 15px rgba($primary-green, 0.2);

    &:hover {
      transform: translateY(-2px);
      box-shadow: 0 8px 25px rgba($primary-green, 0.3);
      background: $sage-green !important;
    }
  }
}

// Mobile Responsive
@media (max-width: 768px) {
  .about-section {
    flex-direction: column;
  }

  .left-panel,
  .right-panel {
    width: 100%;
  }

  .left-panel {
    height: 45vh;
    min-height: 350px;

    .left-content .left-title {
      font-size: 2rem;
      line-height: 1.2;
    }
  }

  .right-panel .scrolling-content {
    padding: 1.5rem 1rem;
    margin-top: 1rem;

    .content-section {
      margin-bottom: 2.5rem;

      .section-heading {
        font-size: 1.6rem;
        margin-bottom: 1rem;
        line-height: 1.3;
      }

      .section-text {
        font-size: 0.9rem;
        line-height: 1.6;
        margin-bottom: 1.5rem;
      }
    }
  }

  .stats-grid,
  .values-grid {
    grid-template-columns: 1fr;
    gap: 1rem;
  }

  .stat-card {
    padding: 1.2rem 1rem;
    margin-bottom: 0.5rem;

    .stat-number {
      font-size: 1.8rem;
    }

    .stat-label {
      font-size: 0.8rem;
      margin-top: 0.3rem;
    }
  }

  .mv-card {
    padding: 1.2rem;
    margin-bottom: 1rem;

    &:hover {
      transform: translateY(-2px);
    }

    .mv-title {
      font-size: 1.2rem;
      margin-bottom: 0.8rem;
    }

    .mv-text {
      font-size: 0.9rem;
      line-height: 1.5;
    }
  }

  .value-item {
    padding: 1rem 0.5rem;

    .value-title {
      font-size: 1rem;
      margin-bottom: 0.5rem;
    }

    .value-text {
      font-size: 0.85rem;
      line-height: 1.4;
    }
  }

  .story-content .story-text {
    font-size: 0.9rem;
    line-height: 1.6;
    margin-bottom: 1.2rem;
  }

  .cta-section .cta-btn {
    padding: 10px 24px;
    font-size: 0.9rem;
  }
}
</style>