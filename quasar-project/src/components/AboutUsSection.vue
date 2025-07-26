<template>
  <section id="about-us" class="about-section">
    <div class="about-overlay"></div>
    <div class="about-content">
      <div class="row justify-center">
        <div class="col-12 col-md-10 col-lg-8">
          <div class="text-center q-mb-xl">
            <h1 class="section-title">About Us</h1>
            <p class="section-subtitle">
              Learn more about our mission, values, and the team behind our success
            </p>
          </div>

          <div class="row q-col-gutter-xl">
            <div class="col-12 col-md-6">
              <q-card class="full-height brand-card">
                <q-card-section>
                  <div class="card-title">Our Mission</div>
                  <p class="card-text">
                    We are dedicated to creating innovative solutions that empower businesses 
                    to achieve their goals through cutting-edge technology and exceptional service.
                  </p>
                </q-card-section>
              </q-card>
            </div>

            <div class="col-12 col-md-6">
              <q-card class="full-height brand-card">
                <q-card-section>
                  <div class="card-title">Our Vision</div>
                  <p class="card-text">
                    To be the leading provider of transformative digital solutions that 
                    drive success and create lasting value for our clients and partners.
                  </p>
                </q-card-section>
              </q-card>
            </div>

            <div class="col-12">
              <q-card class="brand-card">
                <q-card-section>
                  <div class="card-title q-mb-md">Our Values</div>
                  <div class="row q-col-gutter-md">
                    <div class="col-12 col-sm-6 col-md-3">
                      <div class="text-center value-item">
                        <q-icon name="lightbulb" size="3rem" class="value-icon q-mb-sm" />
                        <div class="value-title">Innovation</div>
                        <p class="value-text">
                          Continuously pushing boundaries with creative solutions
                        </p>
                      </div>
                    </div>
                    <div class="col-12 col-sm-6 col-md-3">
                      <div class="text-center value-item">
                        <q-icon name="handshake" size="3rem" class="value-icon q-mb-sm" />
                        <div class="value-title">Integrity</div>
                        <p class="value-text">
                          Building trust through honest and transparent practices
                        </p>
                      </div>
                    </div>
                    <div class="col-12 col-sm-6 col-md-3">
                      <div class="text-center value-item">
                        <q-icon name="star" size="3rem" class="value-icon q-mb-sm" />
                        <div class="value-title">Excellence</div>
                        <p class="value-text">
                          Delivering outstanding quality in everything we do
                        </p>
                      </div>
                    </div>
                    <div class="col-12 col-sm-6 col-md-3">
                      <div class="text-center value-item">
                        <q-icon name="group" size="3rem" class="value-icon q-mb-sm" />
                        <div class="value-title">Collaboration</div>
                        <p class="value-text">
                          Working together to achieve shared success
                        </p>
                      </div>
                    </div>
                  </div>
                </q-card-section>
              </q-card>
            </div>

            <div class="col-12">
              <q-card class="brand-card">
                <q-card-section>
                  <div class="card-title q-mb-md">Our Story</div>
                  <p class="card-text q-mb-md">
                    Founded with a passion for technology and a commitment to excellence, 
                    our company has grown from a small startup to a trusted partner for 
                    businesses worldwide. We combine years of experience with fresh 
                    perspectives to deliver solutions that make a real difference.
                  </p>
                  <p class="card-text">
                    Our team of dedicated professionals brings together diverse skills 
                    and expertise, united by a shared vision of helping our clients 
                    succeed in an ever-evolving digital landscape.
                  </p>
                </q-card-section>
              </q-card>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
// About Us section component
</script>

<style lang="scss" scoped>
.about-section {
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
    background: linear-gradient(
      135deg,
      rgba(254, 250, 224, 0.95) 0%,
      rgba(245, 243, 232, 0.92) 25%,
      rgba(232, 230, 211, 0.90) 50%,
      rgba(212, 210, 191, 0.88) 75%,
      rgba(177, 171, 134, 0.85) 100%
    );
    z-index: 0;
  }
}

.about-content {
  position: relative;
  z-index: 2;
  width: 100%;
  padding: 80px 24px;
}

.section-title {
  font-size: 3rem;
  font-weight: 800;
  color: #0A400C;
  margin-bottom: 1rem;
}

.section-subtitle {
  font-size: 1.2rem;
  color: #819067;
  opacity: 0.9;
  line-height: 1.6;
}

.brand-card {
  border-radius: 20px;
  background: rgba(254, 250, 224, 0.9);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(177, 171, 134, 0.3);
  box-shadow: 0 8px 32px rgba(10, 64, 12, 0.1);
  transition: all 0.3s ease;

  &:hover {
    transform: translateY(-5px);
    box-shadow: 0 12px 40px rgba(10, 64, 12, 0.15);
  }
}

.card-title {
  font-size: 1.5rem;
  font-weight: 700;
  color: #0A400C;
  margin-bottom: 1rem;
}

.card-text {
  font-size: 1rem;
  color: #0A400C;
  opacity: 0.8;
  line-height: 1.6;
}

.value-item {
  padding: 1rem;
}

.value-icon {
  color: #0A400C;
  opacity: 0.8;
}

.value-title {
  font-size: 1.2rem;
  font-weight: 600;
  color: #0A400C;
  margin-bottom: 0.5rem;
}

.value-text {
  font-size: 0.9rem;
  color: #819067;
  opacity: 0.9;
  line-height: 1.5;
}

@media (max-width: 768px) {
  .about-content {
    padding: 60px 16px;
  }

  .section-title {
    font-size: 2.5rem;
  }

  .section-subtitle {
    font-size: 1rem;
  }

  .card-title {
    font-size: 1.3rem;
  }

  .value-title {
    font-size: 1.1rem;
  }

  .value-text {
    font-size: 0.85rem;
  }
}
</style>