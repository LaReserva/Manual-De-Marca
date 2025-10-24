# 💻 LA RESERVA - DESARROLLO WEB
## PARTE C-2: Layouts, Componentes y Estilos

**Versión:** 1.0  
**Fecha:** Octubre 2025  
**Tiempo de lectura:** 15 minutos

---

## 📑 CONTENIDO

1. Layouts Base
2. Componentes Globales
3. Responsive Design System
4. Utilidades de Estilo
5. Convenciones de Nomenclatura

---

## 1. LAYOUTS BASE

### 1.1 BaseLayout.astro

```css
---
// src/layouts/BaseLayout.astro
import '@/styles/global.css';

interface Props {
  title: string;
  description?: string;
  image?: string;
  noindex?: boolean;
}

const {
  title,
  description = 'Mixología exclusiva para eventos premium en Lima, Perú. Cócteles de autor y servicio excepcional.',
  image = '/images/og-image.jpg',
  noindex = false,
} = Astro.props;

const siteUrl = import.meta.env.PUBLIC_SITE_URL || 'https://lareserva.pe';
const canonicalURL = new URL(Astro.url.pathname, siteUrl);
---

<!doctype html>
<html lang="es" class="scroll-smooth">
  <head>
    <!-- Meta básico -->
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <link rel="icon" type="image/svg+xml" href="/favicon.svg" />
    <meta name="generator" content={Astro.generator} />
    
    <!-- SEO -->
    <title>{title} | La Reserva - Mixología Exclusiva</title>
    <meta name="description" content={description} />
    <link rel="canonical" href={canonicalURL} />
    {noindex && <meta name="robots" content="noindex, nofollow" />}
    
    <!-- Open Graph / Facebook -->
    <meta property="og:type" content="website" />
    <meta property="og:url" content={canonicalURL} />
    <meta property="og:title" content={title} />
    <meta property="og:description" content={description} />
    <meta property="og:image" content={new URL(image, siteUrl)} />
    
    <!-- Twitter -->
    <meta property="twitter:card" content="summary_large_image" />
    <meta property="twitter:url" content={canonicalURL} />
    <meta property="twitter:title" content={title} />
    <meta property="twitter:description" content={description} />
    <meta property="twitter:image" content={new URL(image, siteUrl)} />
    
    <!-- Fonts -->
    <link rel="preconnect" href="https://fonts.googleapis.com" />
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
    <link
      href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;500;600;700;900&family=Montserrat:wght@300;400;500;600;700&display=swap"
      rel="stylesheet"
    />
    
    <!-- Structured Data (JSON-LD) -->
    <script type="application/ld+json">
      {
        "@context": "https://schema.org",
        "@type": "LocalBusiness",
        "name": "La Reserva",
        "description": "Mixología exclusiva para eventos premium",
        "url": "https://lareserva.pe",
        "telephone": "+51999888777",
        "address": {
          "@type": "PostalAddress",
          "addressLocality": "Lima",
          "addressCountry": "PE"
        }
      }
    </script>
  </head>
  <body class="antialiased">
    <slot />
  </body>
</html>
```

### 1.2 PageLayout.astro

```astro
---
// src/layouts/PageLayout.astro
import BaseLayout from './BaseLayout.astro';
import Header from '@/components/layout/Header.astro';
import Footer from '@/components/layout/Footer.astro';

interface Props {
  title: string;
  description?: string;
  image?: string;
}

const { title, description, image } = Astro.props;
---

<BaseLayout title={title} description={description} image={image}>
  <Header />
  
  <main class="min-h-screen">
    <slot />
  </main>
  
  <Footer />
</BaseLayout>
```

### 1.3 AdminLayout.astro

```astro
---
// src/layouts/AdminLayout.astro
import BaseLayout from './BaseLayout.astro';
import AdminSidebar from '@/components/admin/AdminSidebar.astro';
import AdminHeader from '@/components/admin/AdminHeader.astro';

interface Props {
  title: string;
}

const { title } = Astro.props;
---

<BaseLayout title={title} noindex={true}>
  <div class="flex h-screen bg-secondary-50">
    <!-- Sidebar -->
    <AdminSidebar />
    
    <!-- Main content area -->
    <div class="flex-1 flex flex-col overflow-hidden">
      <!-- Admin Header -->
      <AdminHeader />
      
      <!-- Main content -->
      <main class="flex-1 overflow-y-auto">
        <div class="container-custom py-8">
          <slot />
        </div>
      </main>
    </div>
  </div>
</BaseLayout>
```

---

## 2. COMPONENTES GLOBALES

### 2.1 Header.astro

```astro
---
// src/components/layout/Header.astro
import Navbar from './Navbar.astro';
import MobileMenu from './MobileMenu.astro';

const currentPath = Astro.url.pathname;
---

<header 
  id="main-header"
  class="fixed top-0 left-0 right-0 z-50 bg-white/95 backdrop-blur-sm shadow-sm transition-all duration-300"
>
  <div class="container-custom">
    <div class="flex items-center justify-between py-4">
      <!-- Logo -->
      <a href="/" class="flex items-center group">
        <img 
          src="/logo.svg" 
          alt="La Reserva" 
          class="h-12 w-auto transition-transform group-hover:scale-105" 
        />
      </a>
      
      <!-- Desktop Navigation -->
      <Navbar currentPath={currentPath} />
      
      <!-- CTA Button (Desktop) -->
      <a href="/cotizacion" class="hidden lg:block btn-primary">
        Cotizar Evento
      </a>
      
      <!-- Mobile Menu Button -->
      <button
        id="mobile-menu-btn"
        class="lg:hidden p-2 text-secondary-600 hover:text-primary-500 transition-colors"
        aria-label="Abrir menú"
      >
        <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
        </svg>
      </button>
    </div>
  </div>
  
  <!-- Mobile Menu -->
  <MobileMenu currentPath={currentPath} />
</header>

<!-- Spacer para header fixed -->
<div class="h-20"></div>

<script>
  // Mobile menu toggle
  const btn = document.getElementById('mobile-menu-btn');
  const menu = document.getElementById('mobile-menu');
  
  btn?.addEventListener('click', () => {
    menu?.classList.toggle('hidden');
  });
  
  // Header scroll effect
  let lastScroll = 0;
  const header = document.getElementById('main-header');
  
  window.addEventListener('scroll', () => {
    const currentScroll = window.pageYOffset;
    
    if (currentScroll > 100) {
      header?.classList.add('shadow-md');
    } else {
      header?.classList.remove('shadow-md');
    }
    
    lastScroll = currentScroll;
  });
</script>
```

### 2.2 Navbar.astro

```astro
---
// src/components/layout/Navbar.astro
interface Props {
  currentPath: string;
}

const { currentPath } = Astro.props;

const navLinks = [
  { name: 'Inicio', href: '/' },
  { name: 'Servicios', href: '/servicios' },
  { name: 'Paquetes', href: '/paquetes' },
  { name: 'Portafolio', href: '/portafolio' },
  { name: 'Nosotros', href: '/nosotros' },
  { name: 'Blog', href: '/blog' },
  { name: 'Contacto', href: '/contacto' },
];

function isActive(path: string) {
  if (path === '/') {
    return currentPath === '/';
  }
  return currentPath.startsWith(path);
}
---

<nav class="hidden lg:block">
  <ul class="flex items-center gap-8">
    {navLinks.map(link => (
      <li>
        <a 
          href={link.href}
          class={`
            font-medium transition-colors duration-200
            ${isActive(link.href) 
              ? 'text-primary-500' 
              : 'text-secondary-600 hover:text-primary-500'
            }
          `}
        >
          {link.name}
        </a>
      </li>
    ))}
  </ul>
</nav>
```

### 2.3 MobileMenu.astro

```astro
---
// src/components/layout/MobileMenu.astro
interface Props {
  currentPath: string;
}

const { currentPath } = Astro.props;

const navLinks = [
  { name: 'Inicio', href: '/' },
  { name: 'Servicios', href: '/servicios' },
  { name: 'Paquetes', href: '/paquetes' },
  { name: 'Portafolio', href: '/portafolio' },
  { name: 'Nosotros', href: '/nosotros' },
  { name: 'Blog', href: '/blog' },
  { name: 'Contacto', href: '/contacto' },
];

function isActive(path: string) {
  if (path === '/') return currentPath === '/';
  return currentPath.startsWith(path);
}
---

<div 
  id="mobile-menu"
  class="hidden lg:hidden fixed inset-0 top-20 bg-white z-40"
>
  <nav class="container-custom py-8">
    <ul class="space-y-4">
      {navLinks.map(link => (
        <li>
          <a 
            href={link.href}
            class={`
              block py-3 px-4 rounded-lg font-medium transition-all
              ${isActive(link.href)
                ? 'bg-primary-50 text-primary-600'
                : 'text-secondary-600 hover:bg-secondary-50'
              }
            `}
          >
            {link.name}
          </a>
        </li>
      ))}
    </ul>
    
    <!-- CTA Button -->
    <div class="mt-8">
      <a href="/cotizacion" class="btn-primary w-full text-center">
        Cotizar Evento
      </a>
    </div>
  </nav>
</div>
```

### 2.4 Footer.astro

```astro
---
// src/components/layout/Footer.astro
const currentYear = new Date().getFullYear();

const socialLinks = [
  { name: 'Instagram', icon: 'instagram', url: 'https://instagram.com/lareservabar' },
  { name: 'Facebook', icon: 'facebook', url: 'https://facebook.com/lareservabar' },
  { name: 'WhatsApp', icon: 'message-circle', url: 'https://wa.me/51999888777' },
];

const quickLinks = [
  { name: 'Servicios', url: '/servicios' },
  { name: 'Paquetes', url: '/paquetes' },
  { name: 'Portafolio', url: '/portafolio' },
  { name: 'Blog', url: '/blog' },
  { name: 'Contacto', url: '/contacto' },
];

const legalLinks = [
  { name: 'Privacidad', url: '/privacidad' },
  { name: 'Términos', url: '/terminos' },
];
---

<footer class="bg-secondary-600 text-white">
  <!-- Main footer -->
  <div class="container-custom py-12">
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-8">
      <!-- Columna 1: Sobre nosotros -->
      <div>
        <h3 class="font-display text-primary-500 text-xl mb-4">La Reserva</h3>
        <p class="text-secondary-200 text-sm leading-relaxed mb-4">
          Mixología exclusiva para eventos premium en Lima, Perú.
        </p>
        <div class="flex gap-3">
          {socialLinks.map(social => (
            <a
              href={social.url}
              target="_blank"
              rel="noopener noreferrer"
              class="p-2 bg-secondary-500 hover:bg-primary-500 rounded-full transition-colors"
              aria-label={social.name}
            >
              <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24">
                <!-- Iconos inline simples para evitar dependencias -->
                {social.icon === 'instagram' && (
                  <path d="M12 2.163c3.204 0 3.584.012 4.85.07 3.252.148 4.771 1.691 4.919 4.919.058 1.265.069 1.645.069 4.849 0 3.205-.012 3.584-.069 4.849-.149 3.225-1.664 4.771-4.919 4.919-1.266.058-1.644.07-4.85.07-3.204 0-3.584-.012-4.849-.07-3.26-.149-4.771-1.699-4.919-4.92-.058-1.265-.07-1.644-.07-4.849 0-3.204.013-3.583.07-4.849.149-3.227 1.664-4.771 4.919-4.919 1.266-.057 1.645-.069 4.849-.069zm0-2.163c-3.259 0-3.667.014-4.947.072-4.358.2-6.78 2.618-6.98 6.98-.059 1.281-.073 1.689-.073 4.948 0 3.259.014 3.668.072 4.948.2 4.358 2.618 6.78 6.98 6.98 1.281.058 1.689.072 4.948.072 3.259 0 3.668-.014 4.948-.072 4.354-.2 6.782-2.618 6.979-6.98.059-1.28.073-1.689.073-4.948 0-3.259-.014-3.667-.072-4.947-.196-4.354-2.617-6.78-6.979-6.98-1.281-.059-1.69-.073-4.949-.073zm0 5.838c-3.403 0-6.162 2.759-6.162 6.162s2.759 6.163 6.162 6.163 6.162-2.759 6.162-6.163c0-3.403-2.759-6.162-6.162-6.162zm0 10.162c-2.209 0-4-1.79-4-4 0-2.209 1.791-4 4-4s4 1.791 4 4c0 2.21-1.791 4-4 4zm6.406-11.845c-.796 0-1.441.645-1.441 1.44s.645 1.44 1.441 1.44c.795 0 1.439-.645 1.439-1.44s-.644-1.44-1.439-1.44z"/>
                )}
                {social.icon === 'facebook' && (
                  <path d="M24 12.073c0-6.627-5.373-12-12-12s-12 5.373-12 12c0 5.99 4.388 10.954 10.125 11.854v-8.385H7.078v-3.47h3.047V9.43c0-3.007 1.792-4.669 4.533-4.669 1.312 0 2.686.235 2.686.235v2.953H15.83c-1.491 0-1.956.925-1.956 1.874v2.25h3.328l-.532 3.47h-2.796v8.385C19.612 23.027 24 18.062 24 12.073z"/>
                )}
                {social.icon === 'message-circle' && (
                  <path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 00-3.48-8.413Z"/>
                )}
              </svg>
            </a>
          ))}
        </div>
      </div>
      
      <!-- Columna 2: Links rápidos -->
      <div>
        <h4 class="font-semibold text-lg mb-4">Enlaces</h4>
        <ul class="space-y-2">
          {quickLinks.map(link => (
            <li>
              <a
                href={link.url}
                class="text-secondary-200 hover:text-primary-500 transition-colors text-sm"
              >
                {link.name}
              </a>
            </li>
          ))}
        </ul>
      </div>
      
      <!-- Columna 3: Contacto -->
      <div>
        <h4 class="font-semibold text-lg mb-4">Contacto</h4>
        <ul class="space-y-3 text-secondary-200 text-sm">
          <li class="flex items-start gap-2">
            <svg class="w-5 h-5 mt-0.5 flex-shrink-0" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 5a2 2 0 012-2h3.28a1 1 0 01.948.684l1.498 4.493a1 1 0 01-.502 1.21l-2.257 1.13a11.042 11.042 0 005.516 5.516l1.13-2.257a1 1 0 011.21-.502l4.493 1.498a1 1 0 01.684.949V19a2 2 0 01-2 2h-1C9.716 21 3 14.284 3 6V5z" />
            </svg>
            <a href="tel:+51999888777" class="hover:text-primary-500">+51 999 888 777</a>
          </li>
          <li class="flex items-start gap-2">
            <svg class="w-5 h-5 mt-0.5 flex-shrink-0" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z" />
            </svg>
            <a href="mailto:contacto@lareserva.pe" class="hover:text-primary-500">contacto@lareserva.pe</a>
          </li>
          <li class="flex items-start gap-2">
            <svg class="w-5 h-5 mt-0.5 flex-shrink-0" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z" />
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 11a3 3 0 11-6 0 3 3 0 016 0z" />
            </svg>
            <span>Lima, Perú</span>
          </li>
        </ul>
      </div>
      
      <!-- Columna 4: Horarios -->
      <div>
        <h4 class="font-semibold text-lg mb-4">Horarios</h4>
        <ul class="space-y-2 text-secondary-200 text-sm">
          <li>Lunes - Viernes: 9:00 AM - 5:00 PM</li>
          <li>Sábado: 9:00 AM - 1:00 PM</li>
          <li>Domingo: Cerrado</li>
        </ul>
      </div>
    </div>
  </div>
  
  <!-- Bottom bar -->
  <div class="border-t border-secondary-500">
    <div class="container-custom py-6">
      <div class="flex flex-col md:flex-row justify-between items-center gap-4 text-sm text-secondary-300">
        <p>© {currentYear} La Reserva. Todos los derechos reservados.</p>
        <div class="flex gap-4">
          {legalLinks.map(link => (
            <a href={link.url} class="hover:text-primary-500 transition-colors">
              {link.name}
            </a>
          ))}
        </div>
      </div>
    </div>
  </div>
</footer>
```

---

## 3. RESPONSIVE DESIGN SYSTEM

### 3.1 Breakpoints de Tailwind

```javascript
// Breakpoints por defecto de Tailwind (ya configurados)
sm: '640px',   // Tablet pequeña
md: '768px',   // Tablet
lg: '1024px',  // Desktop
xl: '1280px',  // Desktop grande
2xl: '1536px', // Desktop extra grande
```

### 3.2 Mobile-First Approach

Siempre empezar diseñando para móvil, luego agregar estilos para pantallas más grandes:

```astro
<!-- ✅ CORRECTO: Mobile-first -->
<div class="
  text-sm          /* Mobile (por defecto) */
  md:text-base     /* Tablet y más grandes */
  lg:text-lg       /* Desktop y más grandes */
  xl:text-xl       /* Desktop grande y más grandes */
">
  Texto responsive
</div>

<!-- ❌ INCORRECTO: Desktop-first -->
<div class="
  text-xl          /* Aplica a TODOS los tamaños */
  lg:text-lg       /* Reduce en desktop (contradictorio) */
  md:text-base
  sm:text-sm
">
  Mal enfoque
</div>
```

### 3.3 Grid Responsive

```astro
<!-- Grid de 1, 2, 3, 4 columnas según tamaño -->
<div class="
  grid 
  grid-cols-1      /* Mobile: 1 columna */
  sm:grid-cols-2   /* Tablet pequeña: 2 columnas */
  md:grid-cols-2   /* Tablet: 2 columnas */
  lg:grid-cols-3   /* Desktop: 3 columnas */
  xl:grid-cols-4   /* Desktop grande: 4 columnas */
  gap-6            /* Espaciado entre elementos */
">
  <div>Card 1</div>
  <div>Card 2</div>
  <div>Card 3</div>
  <div>Card 4</div>
</div>
```

### 3.4 Flex Responsive

```astro
<!-- Stack vertical en mobile, horizontal en tablet+ -->
<div class="
  flex 
  flex-col         /* Mobile: vertical */
  md:flex-row      /* Tablet+: horizontal */
  gap-4
  items-center
">
  <button class="btn-primary">Botón 1</button>
  <button class="btn-secondary">Botón 2</button>
</div>
```

### 3.5 Padding/Margin Responsive

```astro
<section class="
  py-8             /* Mobile: padding vertical pequeño */
  md:py-16         /* Tablet: padding medio */
  lg:py-24         /* Desktop: padding grande */
">
  <div class="
    px-4           /* Mobile: padding horizontal */
    md:px-6        /* Tablet: más padding */
    lg:px-8        /* Desktop: aún más padding */
  ">
    Contenido
  </div>
</section>
```

### 3.6 Mostrar/Ocultar según tamaño

```astro
<!-- Mostrar solo en mobile -->
<div class="block md:hidden">
  Contenido solo mobile
</div>

<!-- Ocultar en mobile, mostrar en tablet+ -->
<div class="hidden md:block">
  Contenido tablet y desktop
</div>

<!-- Mostrar solo en desktop -->
<div class="hidden lg:block">
  Contenido solo desktop
</div>
```

---

## 4. UTILIDADES DE ESTILO

### 4.1 Función cn() - Merge de clases

```typescript
// src/utils/utils.ts
import { type ClassValue, clsx } from 'clsx';
import { twMerge } from 'tailwind-merge';

/**
 * Combina clases de Tailwind sin conflictos
 * @example cn('px-4', 'px-6') → 'px-6' (última tiene prioridad)
 */
export function cn(...inputs: ClassValue[]) {
  return twMerge(clsx(inputs));
}
```

**Uso en componentes:**

```tsx
// Componente React
import { cn } from '@/utils/utils';

interface ButtonProps {
  variant?: 'primary' | 'secondary';
  size?: 'sm' | 'md' | 'lg';
  className?: string;
  children: React.ReactNode;
}

export function Button({ variant = 'primary', size = 'md', className, children }: ButtonProps) {
  return (
    <button
      className={cn(
        // Estilos base
        'btn font-semibold rounded-full transition-all',
        // Variantes
        variant === 'primary' && 'btn-primary',
        variant === 'secondary' && 'btn-secondary',
        // Tamaños
        size === 'sm' && 'px-4 py-2 text-sm',
        size === 'md' && 'px-6 py-3 text-base',
        size === 'lg' && 'px-8 py-4 text-lg',
        // Clases custom del padre
        className
      )}
    >
      {children}
    </button>
  );
}
```

### 4.2 Clases Utility en global.css

Recordatorio de las clases ya definidas en `src/styles/global.css`:

```css
/* Secciones de página */
.section {
  @apply py-16 md:py-24 lg:py-32;
}

/* Container personalizado */
.container-custom {
  @apply container mx-auto px-4 md:px-6 lg:px-8 max-w-7xl;
}

/* Botones */
.btn {
  @apply inline-flex items-center justify-center px-6 py-3 
         font-semibold rounded-full transition-all duration-200 
         uppercase tracking-wider text-sm md:text-base 
         disabled:opacity-50 disabled:cursor-not-allowed;
}

.btn-primary {
  @apply btn bg-gradient-to-r from-primary-500 to-accent-500 
         text-secondary-600 hover:from-primary-600 hover:to-accent-600 
         shadow-lg hover:shadow-xl;
}

.btn-secondary {
  @apply btn bg-transparent border-2 border-primary-500 
         text-primary-500 hover:bg-primary-500 hover:text-secondary-600;
}

/* Cards */
.card {
  @apply bg-white rounded-lg shadow-md hover:shadow-xl 
         transition-shadow duration-300 overflow-hidden;
}

/* Forms */
.input {
  @apply w-full px-4 py-3 border border-secondary-200 
         rounded-lg focus:outline-none focus:ring-2 
         focus:ring-primary-500 focus:border-transparent 
         transition-all duration-200;
}

.label {
  @apply block text-sm font-semibold text-secondary-600 mb-2;
}

/* Text utilities */
.text-gradient {
  @apply bg-gradient-to-r from-primary-500 to-accent-500 
         bg-clip-text text-transparent;
}
```

---

## 5. CONVENCIONES DE NOMENCLATURA

### 5.1 Archivos y Carpetas

```css
✅ RECOMENDADO:
ComponentName.astro          # PascalCase para componentes
page-name.astro              # kebab-case para páginas
utils.ts                     # camelCase para utilidades
ServiceCard.tsx              # PascalCase para React components

❌ EVITAR:
component_name.astro         # snake_case
COMPONENT.astro              # UPPERCASE
component name.astro         # espacios
```

### 5.2 Componentes

```astro
---
// ✅ CORRECTO: PascalCase
import Button from '@/components/ui/Button.astro';
import ServiceCard from '@/components/sections/ServiceCard.astro';
import QuoteForm from '@/components/forms/QuoteForm.tsx';
---

<Button>Click</Button>
<ServiceCard />
<QuoteForm />
```

### 5.3 Variables y Funciones

```typescript
// ✅ camelCase para variables y funciones
const userName = 'Juan';
const eventDate = new Date();
const isActive = true;

function getEventById(id: string) { }
async function fetchQuotes() { }
const handleSubmit = () => { };
```

### 5.4 Constantes

```typescript
// ✅ UPPER_SNAKE_CASE para constantes globales
const MAX_GUESTS = 500;
const MIN_GUESTS = 25;
const DEFAULT_EVENT_DURATION = 5;
const API_BASE_URL = 'https://api.lareserva.pe';
```

### 5.5 Tipos e Interfaces

```typescript
// ✅ PascalCase para tipos e interfaces
interface Event {
  id: string;
  name: string;
}

interface QuoteFormData {
  email: string;
  phone: string;
}

type EventStatus = 'pending' | 'confirmed' | 'completed';
type UserRole = 'admin' | 'super_admin';
```

### 5.6 Clases CSS

```css
/* ✅ kebab-case para clases custom */
.hero-section { }
.card-title { }
.btn-primary { }
.service-card { }

/* BEM (opcional, no muy común con Tailwind) */
.card { }
.card__title { }
.card__body { }
.card--highlighted { }
```

### 5.7 Nombres de Props

```typescript
// ✅ camelCase para props
interface ButtonProps {
  variant?: string;
  onClick?: () => void;
  isDisabled?: boolean;
  className?: string;
}

// ❌ Evitar
interface ButtonProps {
  Variant?: string;        // PascalCase
  on_click?: () => void;   // snake_case
  'is-disabled'?: boolean; // kebab-case
}
```

---

## ✅ CHECKLIST COMPLETO - 02C

Antes de continuar con el siguiente archivo (02D), verifica:

### Estructura:
- [ ] Todas las carpetas creadas según la estructura
- [ ] Layouts base implementados (BaseLayout, PageLayout, AdminLayout)
- [ ] Header y Footer implementados
- [ ] Navbar responsive funcional

### Estilos:
- [ ] Tailwind configurado con paleta de La Reserva
- [ ] global.css con clases utility
- [ ] Sistema responsive mobile-first implementado
- [ ] Función cn() creada en utils

### Convenciones:
- [ ] Nombres de archivos consistentes (PascalCase, kebab-case)
- [ ] Variables y funciones en camelCase
- [ ] Constantes en UPPER_SNAKE_CASE
- [ ] Tipos e interfaces en PascalCase

### Testing:
- [ ] Servidor de desarrollo corriendo (`pnpm dev`)
- [ ] Página de inicio muestra header y footer
- [ ] Menú móvil funciona correctamente
- [ ] Responsive design funciona en diferentes tamaños
- [ ] No hay errores de TypeScript

---

## 📚 RECURSOS ADICIONALES

### Comandos útiles durante desarrollo:

```bash
# Iniciar servidor de desarrollo
pnpm dev

# Verificar tipos TypeScript
pnpm type-check

# Formatear código
pnpm format

# Build para producción
pnpm build

# Preview del build
pnpm preview
```

### Extensiones de VS Code recomendadas:

1. **Astro** - Syntax highlighting y autocompletado
2. **Tailwind CSS IntelliSense** - Autocompletado de clases
3. **Prettier** - Formateo automático
4. **ESLint** - Detección de errores

### Links útiles:

- **Astro Docs:** https://docs.astro.build
- **Tailwind Docs:** https://tailwindcss.com/docs
- **React Docs:** https://react.dev
- **TypeScript Handbook:** https://www.typescriptlang.org/docs

---

## 🔄 PRÓXIMOS PASOS

Has completado la configuración de estructura y estilos. Ahora continúa con:

**→ Archivo 02D: Utilidades y Mejores Prácticas**
- Funciones de utilidad completas
- Constantes del proyecto
- Validadores con Zod
- Mejores prácticas de código

---

**© 2025 La Reserva. Documentación técnica del proyecto.**