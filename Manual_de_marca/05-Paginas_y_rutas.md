# 💻 LA RESERVA - DESARROLLO WEB
## PARTE 5: Páginas Principales del Sitio

**Versión:** 1.0  
**Fecha:** Octubre 2025  
**Tiempo de lectura:** 30 minutos

---

## 📑 CONTENIDO

1. Estructura de Páginas
2. Página Home (index.astro)
3. Página Servicios
4. Página Paquetes
5. Página Portafolio
6. Página Nosotros
7. Página Contacto
8. Página Blog

---

## 1. ESTRUCTURA DE PÁGINAS

### 1.1 Mapa del Sitio

```css
lareserva.pe/
├── / (Home)
├── /servicios
├── /paquetes
├── /portafolio
├── /nosotros
├── /blog
│   ├── /blog (índice)
│   └── /blog/[slug] (post individual)
├── /contacto
├── /cotizacion
└── /admin/* (panel administrativo)
```

### 1.2 SEO por Página

| Página | Title | Meta Description |
|--------|-------|------------------|
| Home | La Reserva - Mixología Exclusiva en Lima | Bartending premium para eventos exclusivos en Lima, Perú. Cócteles de autor y servicio excepcional. |
| Servicios | Servicios de Bartending - La Reserva | Descubre nuestros servicios de bartending y mixología exclusiva para eventos en Lima. |
| Paquetes | Paquetes de Eventos - La Reserva | Paquetes completos de bartending para bodas, eventos corporativos y celebraciones en Lima. |
| Portafolio | Portafolio de Eventos - La Reserva | Galería de eventos realizados. Cócteles de autor y experiencias memorables en Lima. |
| Nosotros | Sobre Nosotros - La Reserva | Conoce al equipo de La Reserva. Expertos en mixología con más de 10 años de experiencia. |
| Contacto | Contacto - La Reserva | Contáctanos para tu próximo evento. WhatsApp, email y ubicación en Lima. |

---

## 2. PÁGINA HOME (index.astro)

### 2.1 Código Completo

```css
---
// src/pages/index.astro
import PageLayout from '@/layouts/PageLayout.astro';
import { Hero } from '@/components/sections/Hero';
import ServiceCard from '@/components/sections/ServiceCard.astro';
import { TestimonialsSlider } from '@/components/sections/TestimonialsSlider';
import Button from '@/components/ui/Button.astro';
import Card from '@/components/ui/Card.astro';
import { supabase } from '@/lib/supabase';
import { formatCurrency } from '@/utils/formatters';

// Obtener datos
const { data: services } = await supabase
  .from('services')
  .select('*')
  .eq('active', true)
  .order('order_index')
  .limit(4);

const { data: packages } = await supabase
  .from('packages')
  .select('*')
  .eq('active', true)
  .order('order_index');

const { data: testimonials } = await supabase
  .from('testimonials')
  .select('*')
  .eq('approved', true)
  .eq('featured', true)
  .limit(5);

const { data: portfolioImages } = await supabase
  .from('event_images')
  .select('*, event:events(event_type, status)')
  .eq('events.status', 'completed')
  .order('created_at', { ascending: false })
  .limit(6);
---

<PageLayout 
  title="Inicio"
  description="Bartending premium para eventos exclusivos en Lima, Perú. Cócteles de autor, servicio excepcional y experiencias memorables."
>
  <!-- Hero Section -->
  <Hero
    client:load
    title="Mixología Exclusiva para Momentos Únicos"
    subtitle="Transformamos tu celebración en una experiencia memorable con cócteles de autor y servicio excepcional"
    backgroundImage="/images/hero-cocktail-dark.jpg"
  />

  <!-- Servicios Section -->
  <section class="section">
    <div class="container-custom">
      <div class="text-center mb-16">
        <h2 class="text-4xl md:text-5xl font-display font-bold mb-4">
          Nuestros Servicios
        </h2>
        <p class="text-xl text-secondary-400 max-w-3xl mx-auto">
          Soluciones personalizadas de bartending y mixología para cada tipo de evento
        </p>
      </div>

      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-8 mb-12">
        {services?.map(service => (
          <ServiceCard service={service} />
        ))}
      </div>

      <div class="text-center">
        <Button variant="primary" href="/servicios" size="lg">
          Ver Todos los Servicios
        </Button>
      </div>
    </div>
  </section>

  <!-- Por Qué Elegirnos Section -->
  <section class="section bg-secondary-600 text-white">
    <div class="container-custom">
      <div class="text-center mb-16">
        <h2 class="text-4xl md:text-5xl font-display font-bold mb-4">
          ¿Por Qué Elegir La Reserva?
        </h2>
        <p class="text-xl text-secondary-200 max-w-3xl mx-auto">
          Excelencia, experiencia y atención personalizada en cada detalle
        </p>
      </div>

      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
        <!-- Feature 1 -->
        <div class="text-center">
          <div class="w-16 h-16 mx-auto mb-4 bg-primary-500 rounded-full flex items-center justify-center">
            <svg class="w-8 h-8 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7" />
            </svg>
          </div>
          <h3 class="text-xl font-semibold mb-2">Experiencia Comprobada</h3>
          <p class="text-secondary-200">
            Más de 10 años creando experiencias memorables en eventos exclusivos
          </p>
        </div>

        <!-- Feature 2 -->
        <div class="text-center">
          <div class="w-16 h-16 mx-auto mb-4 bg-primary-500 rounded-full flex items-center justify-center">
            <svg class="w-8 h-8 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 6V4m0 2a2 2 0 100 4m0-4a2 2 0 110 4m-6 8a2 2 0 100-4m0 4a2 2 0 110-4m0 4v2m0-6V4m6 6v10m6-2a2 2 0 100-4m0 4a2 2 0 110-4m0 4v2m0-6V4" />
            </svg>
          </div>
          <h3 class="text-xl font-semibold mb-2">Servicio Personalizado</h3>
          <p class="text-secondary-200">
            Cada evento es único. Diseñamos la experiencia perfecta para ti
          </p>
        </div>

        <!-- Feature 3 -->
        <div class="text-center">
          <div class="w-16 h-16 mx-auto mb-4 bg-primary-500 rounded-full flex items-center justify-center">
            <svg class="w-8 h-8 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z" />
            </svg>
          </div>
          <h3 class="text-xl font-semibold mb-2">Ingredientes Premium</h3>
          <p class="text-secondary-200">
            Solo utilizamos ingredientes de la más alta calidad en cada cóctel
          </p>
        </div>
      </div>
    </div>
  </section>

  <!-- Paquetes Section -->
  <section class="section">
    <div class="container-custom">
      <div class="text-center mb-16">
        <h2 class="text-4xl md:text-5xl font-display font-bold mb-4">
          Paquetes Especiales
        </h2>
        <p class="text-xl text-secondary-400 max-w-3xl mx-auto">
          Soluciones completas diseñadas para diferentes tipos de eventos
        </p>
      </div>

      <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
        {packages?.map(pkg => (
          <Card 
            hover 
            padding="none" 
            class={pkg.popular ? 'ring-2 ring-primary-500' : ''}
          >
            {pkg.popular && (
              <div class="bg-primary-500 text-white text-center py-2 font-semibold text-sm">
                MÁS POPULAR
              </div>
            )}
            
            <div class="p-8">
              <h3 class="text-2xl font-display font-bold mb-2">{pkg.name}</h3>
              <p class="text-secondary-400 mb-6">{pkg.description}</p>
              
              <div class="mb-6">
                <span class="text-4xl font-bold text-primary-500">
                  {formatCurrency(pkg.price)}
                </span>
                <p class="text-sm text-secondary-400 mt-1">
                  Para {pkg.guest_range} invitados
                </p>
              </div>

              <ul class="space-y-3 mb-8">
                {pkg.features.map(feature => (
                  <li class="flex items-start gap-2">
                    <svg class="w-5 h-5 text-primary-500 flex-shrink-0 mt-0.5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7" />
                    </svg>
                    <span class="text-sm">{feature}</span>
                  </li>
                ))}
              </ul>

              <Button 
                variant={pkg.popular ? 'primary' : 'secondary'} 
                href="/cotizacion"
                fullWidth
              >
                Solicitar Cotización
              </Button>
            </div>
          </Card>
        ))}
      </div>

      <div class="text-center mt-12">
        <Button variant="outline" href="/paquetes" size="lg">
          Ver Todos los Paquetes
        </Button>
      </div>
    </div>
  </section>

  <!-- Portfolio Preview -->
  <section class="section bg-secondary-50">
    <div class="container-custom">
      <div class="text-center mb-16">
        <h2 class="text-4xl md:text-5xl font-display font-bold mb-4">
          Nuestro Trabajo
        </h2>
        <p class="text-xl text-secondary-400 max-w-3xl mx-auto">
          Eventos realizados que hablan por sí solos
        </p>
      </div>

      <div class="grid grid-cols-2 md:grid-cols-3 gap-4">
        {portfolioImages?.slice(0, 6).map(img => (
          <div class="relative aspect-square overflow-hidden rounded-lg group">
            <img 
              src={img.image_url} 
              alt={img.caption || 'Evento La Reserva'}
              class="w-full h-full object-cover transition-transform duration-300 group-hover:scale-110"
            />
            <div class="absolute inset-0 bg-black/40 opacity-0 group-hover:opacity-100 transition-opacity duration-300 flex items-center justify-center">
              <span class="text-white font-semibold">
                {img.event?.event_type}
              </span>
            </div>
          </div>
        ))}
      </div>

      <div class="text-center mt-12">
        <Button variant="primary" href="/portafolio" size="lg">
          Ver Portafolio Completo
        </Button>
      </div>
    </div>
  </section>

  <!-- Testimonials Section -->
  {testimonials && testimonials.length > 0 && (
    <section class="section">
      <div class="container-custom">
        <div class="text-center mb-16">
          <h2 class="text-4xl md:text-5xl font-display font-bold mb-4">
            Lo Que Dicen Nuestros Clientes
          </h2>
          <p class="text-xl text-secondary-400 max-w-3xl mx-auto">
            Testimonios reales de eventos inolvidables
          </p>
        </div>

        <TestimonialsSlider client:load testimonials={testimonials} />
      </div>
    </section>
  )}

  <!-- CTA Final Section -->
  <section class="section bg-gradient-to-r from-primary-500 to-accent-500 text-white">
    <div class="container-custom text-center">
      <h2 class="text-4xl md:text-5xl font-display font-bold mb-6">
        ¿Listo para Crear Tu Evento Perfecto?
      </h2>
      <p class="text-xl mb-8 max-w-2xl mx-auto">
        Solicita una cotización personalizada y transforma tu celebración en una experiencia memorable
      </p>
      <div class="flex flex-col sm:flex-row gap-4 justify-center">
        <Button variant="outline" href="/cotizacion" size="lg">
          Solicitar Cotización
        </Button>
        <a 
          href="https://wa.me/51999888777?text=Hola!%20Me%20gustaría%20obtener%20más%20información"
          target="_blank"
          rel="noopener noreferrer"
          class="btn btn-secondary inline-flex items-center gap-2 bg-white text-secondary-600 hover:bg-secondary-50"
        >
          <svg class="w-6 h-6" fill="currentColor" viewBox="0 0 24 24">
            <path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 00-3.48-8.413Z"/>
          </svg>
          WhatsApp
        </a>
      </div>
    </div>
  </section>
</PageLayout>
```

---

## 3. PÁGINA SERVICIOS

```css
---
// src/pages/servicios.astro
import PageLayout from '@/layouts/PageLayout.astro';
import ServiceCard from '@/components/sections/ServiceCard.astro';
import Button from '@/components/ui/Button.astro';
import { supabase } from '@/lib/supabase';

const { data: services } = await supabase
  .from('services')
  .select('*')
  .eq('active', true)
  .order('order_index');
---

<PageLayout 
  title="Servicios"
  description="Descubre nuestros servicios de bartending y mixología exclusiva para eventos en Lima. Cócteles de autor y experiencia profesional."
>
  <!-- Hero -->
  <section class="section bg-gradient-to-br from-secondary-600 to-secondary-700 text-white">
    <div class="container-custom text-center">
      <h1 class="text-5xl md:text-6xl font-display font-bold mb-6">
        Nuestros Servicios
      </h1>
      <p class="text-xl max-w-3xl mx-auto">
        Soluciones personalizadas de bartending y mixología para cada tipo de evento
      </p>
    </div>
  </section>

  <!-- Servicios Grid -->
  <section class="section">
    <div class="container-custom">
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
        {services?.map(service => (
          <ServiceCard service={service} />
        ))}
      </div>
    </div>
  </section>

  <!-- CTA -->
  <section class="section bg-primary-50">
    <div class="container-custom text-center">
      <h2 class="text-3xl font-display font-bold mb-4">
        ¿Necesitas un Servicio Personalizado?
      </h2>
      <p class="text-lg text-secondary-400 mb-8">
        Contáctanos para crear una propuesta a tu medida
      </p>
      <Button variant="primary" href="/cotizacion" size="lg">
        Solicitar Cotización
      </Button>
    </div>
  </section>
</PageLayout>
```

---

## 4. PÁGINA PORTAFOLIO (Simplificado)

```css
---
// src/pages/portafolio.astro
import PageLayout from '@/layouts/PageLayout.astro';
import { supabase } from '@/lib/supabase';

const { data: images } = await supabase
  .from('event_images')
  .select('*, event:events(event_type, event_date, status)')
  .eq('events.status', 'completed')
  .order('created_at', { ascending: false });
---

<PageLayout title="Portafolio" description="Galería de eventos realizados por La Reserva en Lima.">
  <section class="section">
    <div class="container-custom">
      <h1 class="text-center mb-12">Nuestro Portafolio</h1>
      
      <div class="grid grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-4">
        {images?.map(img => (
          <div class="relative aspect-square overflow-hidden rounded-lg group">
            <img 
              src={img.image_url} 
              alt={img.caption || 'Evento'}
              class="w-full h-full object-cover group-hover:scale-110 transition-transform duration-300"
            />
            <div class="absolute inset-0 bg-black/50 opacity-0 group-hover:opacity-100 transition-opacity flex items-center justify-center">
              <span class="text-white font-semibold">
                {img.event?.event_type}
              </span>
            </div>
          </div>
        ))}
      </div>
    </div>
  </section>
</PageLayout>
```

---

## 5. PÁGINA NOSOTROS

```css
---
// src/pages/nosotros.astro
import PageLayout from '@/layouts/PageLayout.astro';
import Card from '@/components/ui/Card.astro';
---

<PageLayout title="Nosotros" description="Conoce al equipo de La Reserva. Expertos en mixología con más de 10 años de experiencia.">
  <section class="section">
    <div class="container-custom max-w-4xl">
      <h1 class="text-center mb-8">Sobre La Reserva</h1>
      
      <div class="prose prose-lg mx-auto mb-16">
        <p class="lead">
          Somos especialistas en crear experiencias memorables a través de la mixología artesanal. 
          Con más de 10 años de experiencia, hemos transformado cientos de eventos en Lima.
        </p>
        
        <h2>Nuestra Historia</h2>
        <p>
          La Reserva nació de la pasión por la mixología y el deseo de elevar la experiencia de 
          eventos en Lima. Cada cóctel que preparamos es una obra de arte, cada servicio es una 
          experiencia única.
        </p>

        <h2>Nuestra Misión</h2>
        <p>
          Crear experiencias únicas a través de la mixología artesanal, elevando cada evento con 
          cócteles de autor y un servicio excepcional.
        </p>

        <h2>Nuestra Visión</h2>
        <p>
          Ser la empresa de bartending referente en eventos exclusivos en Lima, reconocida por 
          nuestra excelencia, innovación y atención personalizada.
        </p>
      </div>

      <div class="grid grid-cols-1 md:grid-cols-4 gap-6 mb-16">
        <Card class="text-center">
          <div class="text-4xl font-bold text-primary-500 mb-2">+10</div>
          <p class="text-sm">Años de Experiencia</p>
        </Card>
        <Card class="text-center">
          <div class="text-4xl font-bold text-primary-500 mb-2">+200</div>
          <p class="text-sm">Eventos Realizados</p>
        </Card>
        <Card class="text-center">
          <div class="text-4xl font-bold text-primary-500 mb-2">100%</div>
          <p class="text-sm">Clientes Satisfechos</p>
        </Card>
        <Card class="text-center">
          <div class="text-4xl font-bold text-primary-500 mb-2">5★</div>
          <p class="text-sm">Calificación Promedio</p>
        </Card>
      </div>
    </div>
  </section>
</PageLayout>
```

---

## 6. PÁGINA CONTACTO

```css
---
// src/pages/contacto.astro
import PageLayout from '@/layouts/PageLayout.astro';
import { ContactForm } from '@/components/forms/ContactForm';
import Card from '@/components/ui/Card.astro';
import { CONTACT_INFO, BUSINESS_HOURS } from '@/utils/constants';
---

<PageLayout title="Contacto" description="Contáctanos para tu próximo evento. WhatsApp, email y ubicación en Lima.">
  <section class="section">
    <div class="container-custom">
      <h1 class="text-center mb-12">Contáctanos</h1>

      <div class="grid grid-cols-1 lg:grid-cols-2 gap-12 max-w-6xl mx-auto">
        <!-- Formulario -->
        <Card>
          <h2 class="text-2xl font-display font-bold mb-6">Envíanos un Mensaje</h2>
          <ContactForm client:load />
        </Card>

        <!-- Info de Contacto -->
        <div class="space-y-6">
          <Card>
            <h3 class="text-xl font-semibold mb-4">Información de Contacto</h3>
            <ul class="space-y-4">
              <li class="flex items-start gap-3">
                <svg class="w-6 h-6 text-primary-500 flex-shrink-0" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 5a2 2 0 012-2h3.28a1 1 0 01.948.684l1.498 4.493a1 1 0 01-.502 1.21l-2.257 1.13a11.042 11.042 0 005.516 5.516l1.13-2.257a1 1 0 011.21-.502l4.493 1.498a1 1 0 01.684.949V19a2 2 0 01-2 2h-1C9.716 21 3 14.284 3 6V5z" />
                </svg>
                <div>
                  <p class="font-semibold">Teléfono / WhatsApp</p>
                  <a href={`tel:${CONTACT_INFO.phone}`} class="text-primary-500 hover:underline">
                    {CONTACT_INFO.phoneFormatted}
                  </a>
                </div>
              </li>

              <li class="flex items-start gap-3">
                <svg class="w-6 h-6 text-primary-500 flex-shrink-0" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z" />
                </svg>
                <div>
                  <p class="font-semibold">Email</p>
                  <a href={`mailto:${CONTACT_INFO.email}`} class="text-primary-500 hover:underline">
                    {CONTACT_INFO.email}
                  </a>
                </div>
              </li>

              <li class="flex items-start gap-3">
                <svg class="w-6 h-6 text-primary-500 flex-shrink-0" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17.657 16.657L13.414 20.9a1.998 1.998 0 01-2.827 0l-4.244-4.243a8 8 0 1111.314 0z" />
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 11a3 3 0 11-6 0 3 3 0 016 0z" />
                </svg>
                <div>
                  <p class="font-semibold">Ubicación</p>
                  <p class="text-secondary-400">{CONTACT_INFO.address}</p>
                </div>
              </li>
            </ul>
          </Card>

          <Card>
            <h3 class="text-xl font-semibold mb-4">Horarios de Atención</h3>
            <ul class="space-y-2 text-sm">
              <li>{BUSINESS_HOURS.weekdays}</li>
              <li>{BUSINESS_HOURS.saturday}</li>
              <li>{BUSINESS_HOURS.sunday}</li>
            </ul>
          </Card>

          <Card class="bg-primary-50 border-2 border-primary-500">
            <p class="text-center font-semibold">
              ⚡ {BUSINESS_HOURS.responseTime}
            </p>
          </Card>
        </div>
      </div>
    </div>
  </section>
</PageLayout>
```

---


**© 2025 La Reserva. Documentación técnica completa del proyecto.**