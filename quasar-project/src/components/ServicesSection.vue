<template>
  <section id="services" class="services-section">
    <div class="container">
      <!-- Section Header -->
      <div class="section-header">
        <h2 class="section-title">Our Services</h2>
        <p class="section-subtitle">
          We can offer comprehensive construction solutions tailored to meet your
          residential, commercial, and industrial needs with expert craftsmanship.
        </p>
      </div>

      <!-- Services Multi-Card Display -->
      <div class="services-carousel">
        <div class="carousel-container">
          <div class="cards-container">
              <!-- Service 1: Design -->
              <div class="service-card design-card">
                <div class="card-background"></div>
                <div class="card-overlay"></div>
                <div class="card-content">
                  <div class="service-icon">
                    <q-icon name="architecture" />
                  </div>
                  <h3 class="service-title">Design and Planning Services</h3>
                  <p class="service-description">
                    Comprehensive architectural design and planning solutions for your construction projects.
                  </p>
                  <ul class="service-features">
                    <li><q-icon name="check_circle" />Architectural Design & 3D Modeling</li>
                    <li><q-icon name="check_circle" />Site Planning & Analysis</li>
                    <li><q-icon name="check_circle" />Permit Applications & Approvals</li>
                  </ul>
                </div>
              </div>

              <!-- Service 2: Construction -->
              <div class="service-card construction-card">
                <div class="card-background"></div>
                <div class="card-overlay"></div>
                <div class="card-content">
                  <div class="service-icon">
                    <q-icon name="construction" />
                  </div>
                  <h3 class="service-title">Construction and Building</h3>
                  <p class="service-description">
                    Professional construction services from foundation to completion with quality craftsmanship.
                  </p>
                  <ul class="service-features">
                    <li><q-icon name="check_circle" />New Construction Projects</li>
                    <li><q-icon name="check_circle" />Foundation & Structural Work</li>
                    <li><q-icon name="check_circle" />Quality Control & Inspections</li>
                  </ul>
                </div>
              </div>

              <!-- Service 3: Renovation -->
              <div class="service-card renovation-card">
                <div class="card-background"></div>
                <div class="card-overlay"></div>
                <div class="card-content">
                  <div class="service-icon">
                    <q-icon name="home_repair_service" />
                  </div>
                  <h3 class="service-title">Renovation and Remodeling</h3>
                  <p class="service-description">
                    Transform your existing spaces with professional renovation and remodeling services.
                  </p>
                  <ul class="service-features">
                    <li><q-icon name="check_circle" />Kitchen & Bathroom Remodeling</li>
                    <li><q-icon name="check_circle" />Home Additions & Extensions</li>
                    <li><q-icon name="check_circle" />Interior Renovations</li>
                  </ul>
                </div>
              </div>

              <!-- Service 4: Project Management -->
              <div class="service-card management-card">
                <div class="card-background"></div>
                <div class="card-overlay"></div>
                <div class="card-content">
                  <div class="service-icon">
                    <q-icon name="engineering" />
                  </div>
                  <h3 class="service-title">Project Management & Consulting</h3>
                  <p class="service-description">
                    Expert project management and consulting services to ensure successful project delivery.
                  </p>
                  <ul class="service-features">
                    <li><q-icon name="check_circle" />Project Planning & Scheduling</li>
                    <li><q-icon name="check_circle" />Budget Management & Cost Control</li>
                    <li><q-icon name="check_circle" />Quality Assurance Programs</li>
                  </ul>
                </div>
              </div>

              <!-- Service 5: Maintenance -->
              <div class="service-card maintenance-card">
                <div class="card-background"></div>
                <div class="card-overlay"></div>
                <div class="card-content">
                  <div class="service-icon">
                    <q-icon name="build" />
                  </div>
                  <h3 class="service-title">Maintenance & Support Services</h3>
                  <p class="service-description">
                    Comprehensive maintenance and support services to keep your facilities in optimal condition.
                  </p>
                  <ul class="service-features">
                    <li><q-icon name="check_circle" />Preventive Maintenance Programs</li>
                    <li><q-icon name="check_circle" />Emergency Repair Services</li>
                    <li><q-icon name="check_circle" />24/7 Emergency Response</li>
                  </ul>
                </div>
              </div>
            </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>



</script>

<style lang="scss" scoped>
// Brand colors
$primary-green: #0A400C;
$sage-green: #819067;
$cream: #FEFAE0;
$light-cream: rgba(254, 250, 224, 0.9);

.services-section {
  padding: 100px 0;
  background: linear-gradient(to bottom, #f8f9fa, white);
  position: relative;
  overflow: hidden;

  &::before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: url('data:image/svg+xml,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 100 100"><defs><pattern id="grid" width="2" height="2" patternUnits="userSpaceOnUse"><path d="M 2 0 L 0 0 0 2" fill="none" stroke="rgba(10,64,12,0.12)" stroke-width="0.3"/></pattern></defs><rect width="100" height="100" fill="url(%23grid)"/></svg>');
    opacity: 0.5;
  }
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 2rem;
  position: relative;
  z-index: 2;
}

.section-header {
  text-align: center;
  margin-bottom: 4rem;

  .section-title {
    font-size: 3rem;
    font-weight: 800;
    color: $primary-green;
    margin-bottom: 1.5rem;
    text-shadow: 2px 2px 4px rgba(0,0,0,0.1);
  }

  .section-subtitle {
    font-size: 1.2rem;
    color: $sage-green;
    line-height: 1.6;
    max-width: 800px;
    margin: 0 auto;
  }
}

.services-carousel {
  position: relative;

  .carousel-container {
    border-radius: 0;
    overflow: visible;
    box-shadow: none;
    background: transparent;
    height: 650px;
    position: relative;
  }


  .cards-container {
    display: flex;
    gap: 2rem;
    width: 100%;
    height: 100%;
    padding: 0;
    overflow-x: auto;
    scroll-snap-type: x mandatory;
    scroll-behavior: smooth;

    // Desktop: Show all 5 cards
    @media (min-width: 1024px) {
      overflow: visible;
      scroll-snap-type: none;
      padding: 0;
      gap: 1.5rem;
      justify-content: center;
    }
  }

  .service-card {
    border-radius: 20px;
    box-shadow: 0 8px 25px rgba($primary-green, 0.15);
    border: none;
    transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
    position: relative;
    overflow: hidden;
    height: 100%;
    margin: 0;
    scroll-snap-align: center;

    // Desktop: Equal width cards showing all 5
    @media (min-width: 1024px) {
      flex: 1;
      min-width: 280px;
      max-width: 320px;
    }

    // Mobile: Cards with partial preview
    @media (max-width: 1023px) {
      min-width: 320px;
      flex-shrink: 0;
    }

    .card-background {
      position: absolute;
      top: 0;
      left: 0;
      right: 0;
      bottom: 0;
      background-size: cover;
      background-position: center;
      background-repeat: no-repeat;
      z-index: 1;
      transition: transform 0.4s ease;
    }

    .card-overlay {
      position: absolute;
      top: 0;
      left: 0;
      right: 0;
      bottom: 0;
      background: linear-gradient(
        135deg,
        rgba($primary-green, 0.85) 0%,
        rgba($sage-green, 0.8) 100%
      );
      z-index: 2;
      transition: opacity 0.3s ease;
    }

    .card-content {
      position: relative;
      z-index: 3;
      padding: 2rem;
      height: 100%;
      display: flex;
      flex-direction: column;
      justify-content: flex-start;
      text-align: center;
      color: white;
      gap: 1rem;
    }

    &:hover {
      transform: translateY(-5px);
      box-shadow: 0 15px 40px rgba($primary-green, 0.25);

      .card-background {
        transform: scale(1.05);
      }

      .card-overlay {
        opacity: 0.6;
      }

      .service-icon {
        transform: scale(1.1);
        color: $cream;
      }

    }

    .service-icon {
      font-size: 3.5rem;
      color: rgba(white, 0.9);
      margin-bottom: 0.5rem;
      transition: all 0.3s ease;
      text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
      flex-shrink: 0;
    }

    .service-title {
      font-size: 1.4rem;
      font-weight: 700;
      color: white;
      margin-bottom: 0.5rem;
      line-height: 1.3;
      transition: all 0.3s ease;
      text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
      flex-shrink: 0;
    }

    .service-description {
      font-size: 0.95rem;
      color: rgba(white, 0.9);
      line-height: 1.5;
      margin-bottom: 0.5rem;
      text-shadow: 1px 1px 2px rgba(0,0,0,0.3);
      flex-shrink: 0;
    }

    .service-features {
      list-style: none;
      padding: 0;
      margin: 0;
      text-align: left;

      li {
        display: flex;
        align-items: center;
        margin-bottom: 0.8rem;
        font-size: 0.95rem;
        color: rgba(white, 0.9);
        text-shadow: 1px 1px 2px rgba(0,0,0,0.3);

        .q-icon {
          color: $cream;
          margin-right: 0.8rem;
          font-size: 1.1rem;
          flex-shrink: 0;
        }
      }
    }

  }

  // Individual card backgrounds
  .design-card .card-background {
    background-image: url('https://images.unsplash.com/photo-1586864387967-d02ef85d93e8?w=800&h=600&fit=crop&crop=center');
  }

  .construction-card .card-background {
    background-image: url('https://images.unsplash.com/photo-1487958449943-2429e8be8625?w=800&h=600&fit=crop&crop=center');
  }

  .renovation-card .card-background {
    background-image: url('https://images.unsplash.com/photo-1581858726788-75bc0f6a952d?w=800&h=600&fit=crop&crop=center');
  }

  .management-card .card-background {
    background-image: url('https://images.unsplash.com/photo-1454165804606-c3d57bc86b40?w=800&h=600&fit=crop&crop=center');
  }

  .maintenance-card .card-background {
    background-image: url('https://images.unsplash.com/photo-1621905251189-08b45d6a269e?w=800&h=600&fit=crop&crop=center');
  }
}

// Responsive Design
@media (max-width: 768px) {
  .services-section {
    padding: 60px 0;
  }

  .section-header {
    margin-bottom: 3rem;

    .section-title {
      font-size: 2.2rem;
    }

    .section-subtitle {
      font-size: 1.1rem;
      padding: 0 1rem;
    }
  }

  .services-carousel {
    .carousel-container {
      height: 580px;
    }

    .cards-container {
      padding: 0;
      gap: 1.5rem;
    }

    .service-card {
      min-width: 300px;
      border-radius: 15px;

      .card-content {
        padding: 1.8rem;
      }

      .service-icon {
        font-size: 3.2rem;
        margin-bottom: 1rem;
      }

      .service-title {
        font-size: 1.2rem;
        margin-bottom: 0.8rem;
      }

      .service-description {
        font-size: 0.9rem;
        margin-bottom: 1rem;
      }

      .service-features {
        margin-bottom: 0;

        li {
          font-size: 0.85rem;
          margin-bottom: 0.5rem;
        }
      }
    }
  }
}

@media (max-width: 480px) {
  .container {
    padding: 0 1rem;
  }

  .services-carousel {
    .carousel-container {
      height: 520px;
    }

    .cards-container {
      padding: 0;
      gap: 1rem;
    }

    .service-card {
      min-width: 290px;
      border-radius: 12px;

      .card-content {
        padding: 1.5rem;
      }

      .service-icon {
        font-size: 2.8rem;
        margin-bottom: 0.8rem;
      }

      .service-title {
        font-size: 1.1rem;
        margin-bottom: 0.6rem;
      }

      .service-description {
        font-size: 0.85rem;
        margin-bottom: 0.9rem;
      }

      .service-features {
        margin-bottom: 0;

        li {
          font-size: 0.8rem;
          margin-bottom: 0.4rem;
        }
      }

    }
  }
}
</style>
