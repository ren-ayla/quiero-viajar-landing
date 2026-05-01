<script setup>
/**
 * Estándar de la industria para assets dinámicos en Vite.
 * Usamos import.meta.url para asegurar compatibilidad en hosting.
 */
const mapUrl = new URL('./assets/background.webp', import.meta.url).href;
const logoComplete = new URL('./assets/sky.webp', import.meta.url).href;

const heroBgStyle = {
  backgroundImage: `url(${mapUrl})`
};

const currentYear = new Date().getFullYear();
</script>

<template>
  <!-- El wrapper ahora tiene el color de base para matar el halo -->
  <div class="main-wrapper min-vh-100 d-flex flex-column" id="inicio">
    
    <!-- Capas de fondo: Ahora con z-index positivo pero bajo -->
    <div class="map-background" :style="heroBgStyle"></div>
    <div class="orange-overlay"></div>

    <!-- Contenido Principal: Elevado para que nunca se pierda -->
    <main class="content-section flex-grow-1 d-flex align-items-center justify-content-center">
      <div class="container py-5 mt-4">
        <div class="row justify-content-center">
          <div class="col-11 col-sm-10 col-md-8 col-lg-6">
            <div class="stack-container text-center">
              
              <div class="logo-wrapper mb-4">
                 <img :src="logoComplete" alt="Logo Quiero Viajar" class="img-fluid main-logo-hero">
              </div>
              
              <div class="mb-4">
                <span class="status-badge px-3 py-2 px-md-4 fw-semibold">Sitio Web en Construcción</span>
              </div>

              <p class="branding-keywords text-white mb-4 mb-md-5 fw-normal">
                Viajes grupales | Eventos | Experiencias | Asesorías
              </p>

            </div>
          </div>
        </div>
      </div>
    </main>

    <footer class="footer-bg text-white pt-5 pb-4">
      <div class="container">
        <div class="row gy-4 align-items-center align-items-md-start">
          <div class="col-12 col-md-3 col-lg-2 text-center text-md-start">
            <img :src="logoComplete" alt="Logo Blanco" class="footer-logo-img img-fluid">
          </div>

          <div class="col-12 col-md-6 col-lg-4 text-center text-md-start">
            <h5 class="contacto-title mb-3 fw-bold">Contacto</h5>
            <ul class="list-unstyled mb-0 footer-list">
              <li class="mb-2">
                <a href="tel:+56967864980" class="text-white text-decoration-none">
                  <i class="fa-solid fa-phone me-2"></i>+569 6786 4980
                </a>
              </li>
              <li class="mb-2">
                  <i class="fa-solid fa-envelope me-2"></i>contacto@quieroviajar.cl
              </li>
              <li class="mb-2">
                  <i class="fa-solid fa-location-dot me-2"></i> Chile
              </li>
            </ul>
          </div>

          <div class="col-lg-3 d-none d-lg-block"></div>

          <div class="col-12 col-md-3 col-lg-3 text-center text-md-end">
            <a href="#inicio" class="up-link text-white text-decoration-none border-bottom border-white border-opacity-25 pb-1">
              Volver arriba
            </a>
          </div>

          <div class="col-12 text-center">
            <hr class="mt-4 opacity-10 border-white">
            <p class="small opacity-50 mb-0 fw-light">
              © {{ currentYear }} Quiero Viajar.
            </p>
          </div>
        </div>
      </div>
    </footer>
  </div>
</template>

<style scoped>
/* Estructura Base: El "Filtro" contra el halo */
.main-wrapper {
  /* Color base sólido que coincide con el inicio del degradado */
  background-color: #FF7B1A; 
  position: relative;
  /* Creamos un nuevo contexto de apilamiento para los hijos */
  z-index: 0; 
}

.map-background {
  position: fixed;
  inset: 0;
  background-size: cover;
  background-position: center;
  filter: blur(4px) brightness(0.45);
  /* z-index positivo pero bajo el contenido */
  z-index: 1; 
}

.orange-overlay {
  position: fixed;
  inset: 0;
  /* Bajamos el centro a 0.3 y el borde a 0.7 para que el mapa sea el protagonista */
  background: radial-gradient(
    circle, 
    rgba(255, 123, 26, 0.3) 0%, 
    rgba(255, 123, 26, 0.7) 100%
  );
  z-index: 2;
}

/* Contenido Principal: Siempre encima */
.content-section {
  position: relative;
  z-index: 10;
}

.main-logo-hero {
  width: 80%;
  max-width: 280px;
  height: auto;
  filter: drop-shadow(0 10px 15px rgba(0,0,0,0.3));
  -webkit-box-reflect: below -10px linear-gradient(transparent, rgba(255, 255, 255, 0.05));
}

.status-badge {
  color: white;
  letter-spacing: 2px;
  background: #43A4C5; 
  border-bottom: 3px solid #CC1047; 
  text-transform: uppercase;
  font-size: 1rem;
  display: inline-block;
}

.branding-keywords {
  font-size: 0.9rem;
  letter-spacing: 1px;
}

.contact-btn {
  background-color: #CC1047;
  color: white;
  padding: 0.8rem 2.5rem;
  border-radius: 50px;
  text-transform: uppercase;
  font-size: 0.85rem;
  display: inline-block;
  transition: all 0.3s ease;
}

.contact-btn:hover {
  transform: translateY(-3px);
  background-color: #e61250;
  box-shadow: 0 8px 20px rgba(204, 16, 71, 0.4);
}

.footer-bg {
  background-color: #001D29;
  position: relative;
  /* El footer debe estar por encima de los fondos fijos */
  z-index: 20; 
}

.contacto-title {
  font-size: 1rem;
  color: #FF7B1A; 
  letter-spacing: 1px;
}

.footer-logo-img { 
  max-width: 120px; 
  filter: brightness(0) invert(1); 
}

.footer-list i {
  color: #FF7B1A;
}

/* Media Queries */
@media (max-width: 767px) {
  .footer-logo-img { max-width: 100px; margin-bottom: 1rem; }
  .up-link { margin-top: 1rem; }
}

@media (max-width: 333px) {
  .main-logo-hero { max-width: 240px; }
  .status-badge { font-size: 0.7rem; }
}
</style>