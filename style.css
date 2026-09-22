// ---------- Menú móvil ----------
const navToggle = document.getElementById('navToggle');
const siteNav = document.getElementById('siteNav');

if (navToggle && siteNav) {
  navToggle.addEventListener('click', () => {
    const isOpen = siteNav.classList.toggle('is-open');
    navToggle.classList.toggle('is-active', isOpen);
    navToggle.setAttribute('aria-expanded', String(isOpen));
  });

  siteNav.querySelectorAll('a').forEach((link) => {
    link.addEventListener('click', () => {
      siteNav.classList.remove('is-open');
      navToggle.classList.remove('is-active');
      navToggle.setAttribute('aria-expanded', 'false');
    });
  });
}

// ---------- Revelado al hacer scroll ----------
const revealEls = document.querySelectorAll('.reveal, .reveal-big');

if ('IntersectionObserver' in window && revealEls.length) {
  const revealObserver = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          entry.target.classList.add('in-view');
          revealObserver.unobserve(entry.target);
        }
      });
    },
    { threshold: 0.15, rootMargin: '0px 0px -8% 0px' }
  );
  revealEls.forEach((el) => revealObserver.observe(el));
} else {
  revealEls.forEach((el) => el.classList.add('in-view'));
}

// ---------- Barra de progreso, cabecera con sombra y parallax ----------
const progressBar = document.getElementById('progressBar');
const siteHeader = document.getElementById('siteHeader');
const parallaxEls = Array.from(document.querySelectorAll('[data-speed]'));
const reduceMotion = window.matchMedia('(prefers-reduced-motion: reduce)').matches;

let ticking = false;

function updateOnScroll() {
  const scrollY = window.scrollY || window.pageYOffset;

  // Barra de progreso
  if (progressBar) {
    const docHeight = document.documentElement.scrollHeight - window.innerHeight;
    const pct = docHeight > 0 ? (scrollY / docHeight) * 100 : 0;
    progressBar.style.width = pct + '%';
  }

  // Sombra de cabecera
  if (siteHeader) {
    siteHeader.classList.toggle('is-scrolled', scrollY > 12);
  }

  // Parallax de formas decorativas (relativo a su posición en pantalla,
  // para que no se desplacen sin control en secciones alejadas del inicio)
  if (!reduceMotion) {
    const viewportCenter = window.innerHeight / 2;
    parallaxEls.forEach((el) => {
      const speed = parseFloat(el.dataset.speed) || 0.15;
      const rect = el.getBoundingClientRect();
      const elCenter = rect.top + rect.height / 2;
      const offset = (viewportCenter - elCenter) * speed;
      el.style.transform = `translate3d(0, ${offset}px, 0)`;
    });
  }

  ticking = false;
}

window.addEventListener(
  'scroll',
  () => {
    if (!ticking) {
      requestAnimationFrame(updateOnScroll);
      ticking = true;
    }
  },
  { passive: true }
);

updateOnScroll();
