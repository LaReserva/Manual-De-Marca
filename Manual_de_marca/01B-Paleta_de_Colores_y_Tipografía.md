# 🎨 LA RESERVA - MANUAL DE IDENTIDAD DE MARCA
## PARTE 2: Paleta de Colores y Tipografía

**Versión:** 1.0  
**Fecha:** Octubre 2025  
**Empresa:** La Reserva - Mixología Exclusiva

---

## 📑 CONTENIDO DE ESTE ARCHIVO

4. [Paleta de Colores](#4-paleta-de-colores)
5. [Tipografía](#5-tipografía)

---

# 4. PALETA DE COLORES

## 🎨 Filosofía de Color

La paleta de colores de La Reserva está diseñada para transmitir:
- **Elegancia y sofisticación** a través del negro profundo
- **Lujo y exclusividad** con el dorado elegante
- **Claridad y pureza** mediante el blanco limpio

Esta combinación clásica evoca **prestigio, tradición y calidad premium**, perfecta para eventos exclusivos y experiencias memorables.

---

## 🎨 Colores Primarios

### **1. Negro Profundo**

```css
HEX: #1A1A1A
RGB: 26, 26, 26
CMYK: 0, 0, 0, 90
Pantone: Black 6 C
RAL: 9005 (Jet Black)
```

**Valores para Web:**
```css
color: #1A1A1A;
background: #1A1A1A;
```

**Valores para Sass/Less:**
```scss
$color-negro: #1A1A1A;
$color-primary-dark: #1A1A1A;
```

#### **Uso Principal:**
- Fondos de secciones hero
- Overlays sobre imágenes
- Texto principal sobre fondos claros
- Cards y elementos de fondo
- Navegación y headers

#### **Significado y Psicología:**
- **Elegancia:** El color de la sofisticación
- **Exclusividad:** Premium y distinguido
- **Poder:** Fuerte y seguro
- **Atemporalidad:** Clásico que no pasa de moda

#### **Dónde Usar:**
✅ Fondos principales del sitio web  
✅ Secciones destacadas  
✅ Overlays sobre fotografías (70-90% opacidad)  
✅ Uniformes del equipo  
✅ Material impreso premium  
✅ Packaging

#### **Combinaciones Recomendadas:**
```css
Negro + Dorado + Blanco → Máximo impacto
Negro + Blanco → Contraste fuerte, legibilidad perfecta
Negro + Dorado → Lujo extremo
```

---

### **2. Dorado Elegante**

```css
HEX: #D4AF37
RGB: 212, 175, 55
CMYK: 0, 17, 74, 17
Pantone: 7502 C
RAL: 1036 (Pearl Gold)
```

**Valores para Web:**
```css
color: #D4AF37;
background: linear-gradient(135deg, #D4AF37, #F59E0B);
```

**Valores para Sass/Less:**
```scss
$color-dorado: #D4AF37;
$color-primary: #D4AF37;
$color-gold: #D4AF37;
```

#### **Uso Principal:**
- Color de acento en todo el sitio
- Botones de acción principal (CTAs)
- Líneas decorativas
- Highlights y elementos importantes
- Iconos destacados
- Hover states

#### **Significado y Psicología:**
- **Lujo:** Asociado con oro y premium
- **Prestigio:** Éxito y logro
- **Calidez:** Acogedor y atractivo
- **Exclusividad:** Edición limitada, VIP

#### **Dónde Usar:**
✅ Botones principales  
✅ Links y elementos interactivos  
✅ Línea decorativa del logo  
✅ Acentos en diseño  
✅ Iconos importantes  
✅ Badges y etiquetas premium  
✅ Detalles en uniformes (bordados)

#### **Dónde NO Usar:**
❌ Texto largo sobre blanco (baja legibilidad)  
❌ Fondos completos grandes (puede ser abrumador)  
❌ Texto pequeño (difícil de leer)

#### **Combinaciones Recomendadas:**
```css
Dorado sobre Negro → Excelente contraste
Dorado sobre Gris Oscuro (#2D2D2D) → Muy bueno
Dorado como acento con Negro/Blanco → Perfecto
```

#### **Gradientes con Dorado:**
```css
/* Gradiente Dorado Principal */
background: linear-gradient(135deg, #D4AF37 0%, #F59E0B 100%);

/* Gradiente Dorado Sutil */
background: linear-gradient(135deg, #D4AF37 0%, #B8941F 100%);

/* Gradiente Dorado con Brillo */
background: linear-gradient(135deg, #F4E4BC 0%, #D4AF37 50%, #B8960F 100%);
```

---

### **3. Blanco Puro**

```css
HEX: #FFFFFF
RGB: 255, 255, 255
CMYK: 0, 0, 0, 0
Pantone: N/A (blanco estándar)
RAL: 9016 (Traffic White)
```

**Valores para Web:**
```css
color: #FFFFFF;
background: #FFFFFF;
```

**Valores para Sass/Less:**
```scss
$color-blanco: #FFFFFF;
$color-light: #FFFFFF;
```

#### **Uso Principal:**
- Texto sobre fondos oscuros
- Fondos de secciones alternas
- Espacios negativos
- Cards sobre fondos oscuros
- Elementos de contraste

#### **Significado y Psicología:**
- **Limpieza:** Pulcritud e higiene
- **Claridad:** Transparencia y honestidad
- **Elegancia:** Minimalismo refinado
- **Pureza:** Calidad sin compromisos

#### **Dónde Usar:**
✅ Texto sobre negro/oscuro  
✅ Fondos de secciones (alternando con negro)  
✅ Cards y elementos elevados  
✅ Íconos sobre oscuro  
✅ Espacios de respiro visual

#### **Combinaciones Recomendadas:**
```css
Blanco sobre Negro → Contraste máximo (21:1)
Blanco + Negro + Dorado → Clásico premium
Blanco sobre Gris Oscuro → Muy bueno
```

---

## 🎨 Colores Secundarios (Apoyo)

### **Gris Oscuro**
```css
HEX: #2D2D2D
RGB: 45, 45, 45
```

**Uso:**
- Fondos alternativos menos intensos que negro
- Variaciones en diseño
- Texto secundario sobre blanco
- Cards y elementos de fondo

**Cuándo usar:**
- Cuando negro puro es muy fuerte
- Secciones alternas del sitio
- Fondos de admin panel

---

### **Gris Medio**
```css
HEX: #6B6B6B
RGB: 107, 107, 107
```

**Uso:**
- Texto secundario y complementario
- Metadata (fechas, info adicional)
- Placeholders en formularios
- Íconos no activos

**Ejemplos:**
```css
/* Texto secundario */
color: #6B6B6B;
font-size: 14px;

/* Placeholder */
::placeholder {
  color: #6B6B6B;
  opacity: 0.7;
}
```

---

### **Gris Claro**
```css
HEX: #D1D1D1
RGB: 209, 209, 209
```

**Uso:**
- Bordes sutiles
- Divisores entre secciones
- Líneas de separación
- Backgrounds muy suaves

**Ejemplos:**
```css
/* Borde de card */
border: 1px solid #D1D1D1;

/* Línea divisoria */
border-bottom: 1px solid #D1D1D1;
```

---

### **Dorado Oscuro**
```css
HEX: #B8960F
RGB: 184, 150, 15
```

**Uso:**
- Hover state de botones dorados
- Elementos activos/seleccionados
- Énfasis más fuerte que dorado principal

**Ejemplos:**
```css
/* Hover de botón */
.btn-primary:hover {
  background: #B8960F;
}

/* Estado activo */
.nav-link.active {
  color: #B8960F;
}
```

---

## 🎨 Variantes Extendidas para Web (Tailwind)

Para mayor flexibilidad en desarrollo web, usamos estas variantes:

### **Primary (Dorado) - Escala Completa**
```javascript
primary: {
  50:  '#FEF9E7',  // Muy claro - backgrounds sutiles, hover suave
  100: '#FDF3D0',  // Claro - highlights
  200: '#FAE7A1',  // Claro medio
  300: '#F7DB72',  // Medio claro
  400: '#F4CF43',  // Medio
  500: '#D4AF37',  // ← PRINCIPAL (Dorado Elegante)
  600: '#B8941F',  // Oscuro - hover states
  700: '#8A6F17',  // Muy oscuro
  800: '#5C4A0F',  // Casi negro
  900: '#2E2508',  // Negro dorado
}
```

**Uso de variantes:**
```css
50-100: Backgrounds muy sutiles, hover en elementos claros
200-300: Borders, elementos secundarios
400-500: Elementos principales, botones, links
600-700: Hover states, elementos activos
800-900: Textos sobre dorado, sombras
```

---

### **Secondary (Negro/Gris) - Escala Completa**
```javascript
secondary: {
  50:  '#F5F5F5',  // Casi blanco - backgrounds claros
  100: '#E5E5E5',  // Gris muy claro
  200: '#CCCCCC',  // Gris claro
  300: '#B3B3B3',  // Gris medio claro
  400: '#999999',  // Gris medio
  500: '#2D2D2D',  // Gris oscuro
  600: '#1A1A1A',  // ← PRINCIPAL (Negro Profundo)
  700: '#0D0D0D',  // Negro más intenso
  800: '#000000',  // Negro puro
  900: '#000000',  // Negro puro
}
```

---

### **Accent (Amarillo/Dorado Brillante)**
```javascript
accent: {
  DEFAULT: '#F59E0B',
  50:  '#FEF3E2',
  100: '#FDE8C5',
  200: '#FBD18B',
  300: '#F9BA51',
  400: '#F7A317',
  500: '#F59E0B',  // ← PRINCIPAL
  600: '#C47E09',
  700: '#935F07',
  800: '#623F04',
  900: '#312002',
}
```

**Uso del Accent:**
- Badges y etiquetas
- Notificaciones importantes
- Elementos que necesitan destacar más que el dorado
- CTAs secundarios muy llamativos

---

## 🎨 Combinaciones de Colores Aprobadas

### **1. Negro + Dorado + Blanco (Principal)**

**Uso:** Máximo impacto visual, materiales principales

```css
/* Hero Section */
background: #1A1A1A;
color: #FFFFFF;
accent: #D4AF37;
```

**Aplicaciones:**
- Hero del sitio web
- Banners principales
- Posts destacados en redes
- Material impreso premium
- Presentaciones importantes

**Ejemplo visual:**
```css
━━━━━━━━━━━━━━━━━━━━━━
▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓ Negro (#1A1A1A)
    Texto Blanco
    ─────────────── Línea Dorada (#D4AF37)
▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓
━━━━━━━━━━━━━━━━━━━━━━
```

---

### **2. Blanco + Negro + Dorado (Documentos)**

**Uso:** Fondos claros, documentos oficiales, contenido extenso

```css
/* Documento/Página Clara */
background: #FFFFFF;
text: #1A1A1A;
accent: #D4AF37;
secondary-text: #2D2D2D;
```

**Aplicaciones:**
- Cotizaciones PDF
- Contratos y documentos
- Blog posts
- Páginas de contenido largo
- Material administrativo

---

### **3. Gris Oscuro + Blanco (Alternativa Elegante)**

**Uso:** Variación menos intensa, contenido secundario

```css
/* Sección Alterna */
background: #2D2D2D;
text: #FFFFFF;
accent: #D4AF37;
```

**Aplicaciones:**
- Secciones alternas del sitio
- Footer
- Sidebars
- Panel admin
- Cards sobre fondo oscuro

---

### **4. Dorado + Negro (Eventos Especiales)**

**Uso:** Destacados máximos, promociones exclusivas

```css
/* CTA Destacado */
background: linear-gradient(135deg, #D4AF37, #F59E0B);
text: #1A1A1A;
```

**Aplicaciones:**
- CTAs muy importantes
- Badges "Premium" o "Exclusivo"
- Promociones limitadas
- Anuncios especiales
- Highlights en redes sociales

---

## ♿ Accesibilidad de Color

### **Ratios de Contraste (WCAG 2.1)**

**Nivel AAA (Óptimo - 7:1 o mayor):**
```css
✅ Negro (#1A1A1A) sobre Blanco (#FFFFFF): 21:1
✅ Blanco (#FFFFFF) sobre Negro (#1A1A1A): 21:1
```

**Nivel AA (Bueno - 4.5:1 o mayor):**
```css
✅ Dorado (#D4AF37) sobre Negro (#1A1A1A): 8.2:1
✅ Gris Medio (#6B6B6B) sobre Blanco (#FFFFFF): 4.6:1
✅ Negro (#1A1A1A) sobre Dorado Claro (#FEF9E7): 18:1
```

**No Accesibles para Texto:**
```css
❌ Dorado (#D4AF37) sobre Blanco (#FFFFFF): 2.8:1 (bajo)
❌ Gris Claro (#D1D1D1) sobre Blanco (#FFFFFF): 1.8:1 (muy bajo)
❌ Dorado Claro (#F4CF43) sobre Blanco: 1.9:1 (muy bajo)
```

### **Reglas de Accesibilidad:**

**Para Texto Normal (< 18px):**
- Usar Negro sobre Blanco ✅
- Usar Blanco sobre Negro ✅
- Usar Dorado sobre Negro ✅
- NO usar Dorado sobre Blanco ❌

**Para Texto Grande (≥ 18px o ≥ 14px bold):**
- Todas las combinaciones AAA y AA son válidas
- Dorado sobre Blanco puede usarse solo en títulos muy grandes (≥24px)

**Para Elementos NO Texto (iconos, decoración):**
- Ratio mínimo 3:1
- Dorado sobre Blanco es aceptable para decoración

---

## 🎨 Guía de Uso por Elemento

### **Botones:**
```css
/* Primario */
.btn-primary {
  background: linear-gradient(135deg, #D4AF37, #F59E0B);
  color: #1A1A1A;
}
.btn-primary:hover {
  background: linear-gradient(135deg, #B8941F, #C47E09);
}

/* Secundario */
.btn-secondary {
  background: transparent;
  border: 2px solid #D4AF37;
  color: #D4AF37;
}
.btn-secondary:hover {
  background: #D4AF37;
  color: #1A1A1A;
}
```

---

### **Links:**
```css
/* Link normal */
a {
  color: #D4AF37;
  text-decoration: none;
}
a:hover {
  color: #B8960F;
  text-decoration: underline;
}

/* Link en texto oscuro */
.dark-bg a {
  color: #D4AF37;
}

/* Link en texto claro */
.light-bg a {
  color: #1A1A1A;
  text-decoration: underline;
}
```

---

### **Backgrounds:**
```css
/* Sección Hero */
.hero {
  background: #1A1A1A;
  color: #FFFFFF;
}

/* Sección Alterna */
.section-alt {
  background: #2D2D2D;
  color: #FFFFFF;
}

/* Sección Clara */
.section-light {
  background: #FFFFFF;
  color: #1A1A1A;
}
```

---

### **Cards:**
```css
/* Card sobre fondo oscuro */
.card-dark {
  background: #FFFFFF;
  color: #1A1A1A;
  border: 1px solid #D4AF37;
}

/* Card sobre fondo claro */
.card-light {
  background: #1A1A1A;
  color: #FFFFFF;
  box-shadow: 0 4px 20px rgba(212, 175, 55, 0.3);
}
```

---

### **Textos:**
```css
/* Título principal */
h1 {
  color: #1A1A1A; /* o #D4AF37 para impacto */
}

/* Texto normal */
p {
  color: #2D2D2D;
}

/* Texto secundario */
.text-secondary {
  color: #6B6B6B;
}

/* Texto sobre oscuro */
.dark-bg p {
  color: #FFFFFF;
}
```

---

# 5. TIPOGRAFÍA

## ✍️ Filosofía Tipográfica

La Reserva utiliza una combinación de:
- **Playfair Display (Serif):** Para transmitir elegancia, tradición y sofisticación
- **Montserrat (Sans-serif):** Para legibilidad moderna y profesionalismo

Esta dualidad crea un **balance perfecto entre lo clásico y lo contemporáneo**, reflejando la esencia de la marca: tradición en mixología con innovación en servicio.

---

## ✍️ Fuente Principal: Playfair Display

### **Información General:**

```css
Familia: Playfair Display
Tipo: Serif (serifas altas y delgadas)
Diseñador: Claus Eggers Sørensen
Año: 2011
Inspiración: Tipografías de transición del siglo XVIII
Licencia: Open Font License (SIL OFL) - Gratuita
```

### **Características Visuales:**
- Alto contraste entre trazos gruesos y delgados
- Serifas delgadas y afiladas
- Formas elegantes y refinadas
- Inspirada en tipos clásicos británicos
- Optimizada para títulos y displays
- Excelente presencia en tamaños grandes

### **Pesos Disponibles:**

```scc
Light (300)       - Para títulos muy grandes y elegantes
Regular (400)     - Uso general en títulos
Medium (500)      - Subtítulos con más peso
SemiBold (600)    - Títulos principales importantes
Bold (700)        - Logo y títulos hero
Black (900)       - Impacto máximo (uso ocasional)

+ Todas las variantes en cursiva (italic)
```

### **Uso Principal:**

#### **1. Logo**
```css
font-family: 'Playfair Display', serif;
font-weight: 700; /* Bold */
font-size: variable;
letter-spacing: 0.10em a 0.12em; /* +100 a +120 tracking */
text-transform: uppercase;
```

#### **2. Títulos Principales (H1)**
```css
font-family: 'Playfair Display', serif;
font-weight: 700; /* Bold */
font-size: 48-72px; /* Desktop */
font-size: 32-40px; /* Mobile */
letter-spacing: 0.08em; /* +80 */
line-height: 1.2;
color: #1A1A1A o #D4AF37;
```

**Ejemplo:**
```html
<h1 class="hero-title">
  Mixología Exclusiva para Momentos Únicos
</h1>
```

#### **3. Subtítulos (H2)**
```css
font-family: 'Playfair Display', serif;
font-weight: 600; /* SemiBold */
font-size: 32-40px; /* Desktop */
font-size: 24-32px; /* Mobile */
letter-spacing: 0.06em; /* +60 */
line-height: 1.3;
color: #1A1A1A;
```

**Ejemplo:**
```html
<h2 class="section-title">
  Nuestros Servicios Premium
</h2>
```

#### **4. Nombres de Cócteles**
```css
font-family: 'Playfair Display', serif;
font-weight: 600; /* SemiBold */
font-size: 20-24px;
letter-spacing: 0.04em; /* +40 */
color: #D4AF37;
```

**Ejemplo:**
```html
<h3 class="cocktail-name">
  Old Fashioned Reserva
</h3>
```

#### **5. Quotes y Destacados**
```css
font-family: 'Playfair Display', serif;
font-weight: 400; /* Regular o Medium */
font-size: 24-32px;
font-style: italic; /* Cursiva para quotes */
letter-spacing: 0.02em;
line-height: 1.5;
color: #2D2D2D;
```

**Ejemplo:**
```html
<blockquote class="testimonial-quote">
  "La mejor experiencia de bartending que hemos tenido. 
   Cada detalle fue perfecto."
</blockquote>
```

### **Dónde USAR Playfair Display:**
✅ Logo  
✅ Títulos principales (H1, H2)  
✅ Nombres de cócteles  
✅ Quotes y testimonios  
✅ Headers de secciones importantes  
✅ Material impreso destacado  
✅ Elementos de marca fuerte

### **Dónde NO USAR Playfair Display:**
❌ Cuerpo de texto largo (difícil de leer)  
❌ Texto pequeño (< 14px)  
❌ Párrafos extensos  
❌ Formularios y campos de entrada  
❌ Navegación (excepto logo)  
❌ Botones (excepto muy específicos)

### **Importar Playfair Display:**

**Google Fonts:**
```html
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,500;0,600;0,700;0,900;1,400;1,600&display=swap" rel="stylesheet">
```

**CSS Import:**
```css
@import url('https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,500;0,600;0,700;0,900;1,400;1,600&display=swap');
```

**CSS Variable:**
```css
:root {
  --font-display: 'Playfair Display', Georgia, serif;
}

h1, h2, .logo {
  font-family: var(--font-display);
}
```

### **Alternativa de Fallback:**
```css
font-family: 'Playfair Display', 'Cormorant Garamond', Georgia, 'Times New Roman', serif;
```

---

## ✍️ Fuente Secundaria: Montserrat

### **Información General:**

```css
Familia: Montserrat
Tipo: Sans-serif (geométrica humanista)
Diseñadora: Julieta Ulanovsky
Año: 2010
Inspiración: Carteles del barrio Montserrat, Buenos Aires
Licencia: Open Font License (SIL OFL) - Gratuita
```

### **Características Visuales:**
- Formas geométricas pero amigables
- Muy legible en tamaños pequeños
- Versatil para digital e impreso
- Limpia y moderna
- Excelente espaciado
- Funciona bien en párrafos

### **Pesos Disponibles:**

```css
Thin (100)        - Decorativo, uso muy específico
Light (300)       - Texto ligero, elegante
Regular (400)     - Cuerpo de texto principal
Medium (500)      - Texto con más presencia
SemiBold (600)    - Subtítulos, destacados
Bold (700)        - Botones, énfasis fuerte
ExtraBold (800)   - Uso ocasional
Black (900)       - Impacto máximo (raro)

+ Todas las variantes en cursiva
```

### **Uso Principal:**

#### **1. Cuerpo de Texto**
```css
font-family: 'Montserrat', sans-serif;
font-weight: 400; /* Regular */
font-size: 16-18px; /* Desktop */
font-size: 16px; /* Mobile */
letter-spacing: normal;
line-height: 1.6;
color: #2D2D2D;
```

**Ejemplo:**
```html
<p class="body-text">
  La Reserva es una empresa de bartending premium 
  especializada en crear experiencias memorables para 
  eventos exclusivos en Lima.
</p>
```

#### **2. Subtítulos (H3, H4)**
```css
font-family: 'Montserrat', sans-serif;
font-weight: 700; /* Bold */
font-size: 20-24px; /* H3 */
font-size: 18-20px; /* H4 */
letter-spacing: normal;
line-height: 1.4;
color: #1A1A1A;
text-transform: none;
```

#### **3. Botones y CTAs**
```css
font-family: 'Montserrat', sans-serif;
font-weight: 600; /* SemiBold */
font-size: 14-16px;
letter-spacing: 0.04em; /* +40 */
text-transform: uppercase;
color: variable;
```

**Ejemplo:**
```html
<button class="btn-primary">
  COTIZA TU EVENTO
</button>
```

#### **4. Navegación**
```css
font-family: 'Montserrat', sans-serif;
font-weight: 500; /* Medium */
font-size: 15-16px;
letter-spacing: 0.02em;
color: #FFFFFF o #1A1A1A;
```

#### **5. Texto Secundario / Metadata**
```css
font-family: 'Montserrat', sans-serif;
font-weight: 400; /* Regular */
font-size: 14px;
letter-spacing: normal;
line-height: 1.5;
color: #6B6B6B;
```

**Ejemplo:**
```html
<p class="event-date">
  Publicado el 15 de octubre, 2025
</p>
```

#### **6. Formularios**
```css
/* Labels */
font-family: 'Montserrat', sans-serif;
font-weight: 600; /* SemiBold */
font-size: 14px;
color: #2D2D2D;

/* Inputs */
font-family: 'Montserrat', sans-serif;
font-weight: 400; /* Regular */
font-size: 16px;
color: #1A1A1A;
```

### **Dónde USAR Montserrat:**
✅ Todo el cuerpo de texto  
✅ Navegación  
✅ Botones y CTAs  
✅ Formularios  
✅ Descripciones de productos/servicios  
✅ Listas y bullets  
✅ Subtítulos H3, H4, H5, H6  
✅ Metadata y fechas  
✅ Footer content

### **Importar Montserrat:**

**Google Fonts:**
```html
<link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@300;400;500;600;700&display=swap" rel="stylesheet">
```

**CSS Import:**
```css
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@300;400;500;600;700&display=swap');
```

**CSS Variable:**
```css
:root {
  --font-body: 'Montserrat', 'Helvetica Neue', Arial, sans-serif;
}

body, p, button, input {
  font-family: var(--font-body);
}
```

### **Alternativa de Fallback:**
```css
font-family: 'Montserrat', 'Inter', 'Lato', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
```

---

## 📊 Jerarquía Tipográfica Completa

### **Sistema de Escalado:**

```css
H1 (Hero Title):     48-72px  | Playfair Display Bold
H2 (Section Title):  32-40px  | Playfair Display SemiBold  
H3 (Subsection):     20-24px  | Montserrat Bold
H4 (Card Title):     18-20px  | Montserrat Bold
H5 (Small Title):    16-18px  | Montserrat SemiBold
H6 (Tiny Title):     14-16px  | Montserrat SemiBold

Body Large:          18px     | Montserrat Regular
Body Regular:        16px     | Montserrat Regular
Body Small:          14px     | Montserrat Regular
Caption:             12px     | Montserrat Regular

Button Large:        16px     | Montserrat SemiBold
Button Regular:      14px     | Montserrat SemiBold
Button Small:        12px     | Montserrat SemiBold
```

### **Configuración Responsive:**

```css
/* Desktop (> 1024px) */
h1 { font-size: 72px; }
h2 { font-size: 40px; }
h3 { font-size: 24px; }
p  { font-size: 18px; }

/* Tablet (768px - 1024px) */
@media (max-width: 1024px) {
  h1 { font-size: 56px; }
  h2 { font-size: 36px; }
  h3 { font-size: 22px; }
  p  { font-size: 17px; }
}

/* Mobile (< 768px) */
@media (max-width: 768px) {
  h1 { font-size: 40px; }
  h2 { font-size: 32px; }
  h3 { font-size: 20px; }
  p  { font-size: 16px; }
}

/* Small Mobile (< 480px) */
@media (max-width: 480px) {
  h1 { font-size: 32px; }
  h2 { font-size: 24px; }
  h3 { font-size: 18px; }
  p  { font-size: 16px; }
}
```

---

## 📐 Reglas Tipográficas

### **1. Letter Spacing (Tracking)**

**Playfair Display:**
```css
/* Logo */
letter-spacing: 0.10em a 0.12em; /* +100 a +120 */

/* H1 */
letter-spacing: 0.08em; /* +80 */

/* H2 */
letter-spacing: 0.06em; /* +60 */

/* Nombres de cócteles */
letter-spacing: 0.04em; /* +40 */
```

**Montserrat:**
```css
/* Botones uppercase */
letter-spacing: 0.04em; /* +40 */

/* Navegación */
letter-spacing: 0.02em; /* +20 */

/* Cuerpo de texto */
letter-spacing: normal; /* 0 */
```

**Regla general:**
- **Playfair:** Siempre usar tracking amplio en títulos
- **Montserrat:** Tracking normal, excepto botones uppercase
- **Nunca usar tracking negativo**

---

### **2. Line Height (Interlineado)**

```css
/* Títulos */
line-height: 1.2;  /* Para H1, H2 - Playfair */
line-height: 1.3;  /* Para H3, H4 - Montserrat */

/* Cuerpo de texto */
line-height: 1.6;  /* Óptimo para legibilidad */

/* Texto pequeño */
line-height: 1.5;  /* Para < 16px */

/* Quotes */
line-height: 1.5-1.7;  /* Más espaciado para respirar */
```

**Regla:** Mínimo 1.5 para cuerpo de texto (accesibilidad)

---

### **3. Párrafos y Bloques**

**Ancho de línea óptimo:**
```css
max-width: 65ch;  /* 65 caracteres por línea */
/* O */
max-width: 700px; /* Aproximadamente 75 caracteres */
```

**Espaciado entre párrafos:**
```css
margin-bottom: 1em;  /* Un espacio de línea */
/* O */
margin-bottom: 24px; /* Valor fijo */
```

**Sangría:**
```css
/* NO usar sangría en web (usar espaciado entre párrafos) */
text-indent: 0;

/* Solo en documentos impresos muy específicos */
text-indent: 2em; /* Si se requiere estilo clásico */
```

---

### **4. Alineación**

**Texto largo:**
```css
text-align: left; /* SIEMPRE para bloques largos */
```

**Títulos:**
```css
text-align: center; /* Títulos de sección */
text-align: left;   /* Títulos de contenido */
```

**Botones y CTAs:**
```css
text-align: center; /* Centrado visual */
```

**NUNCA usar:**
```css
text-align: justify; /* Crea espacios irregulares en web */
```

---

### **5. Mayúsculas (Uppercase)**

**Usar uppercase en:**
✅ Logo ("LA RESERVA")
✅ Botones importantes
✅ Subtítulo del logo ("MIXOLOGÍA EXCLUSIVA")
✅ Labels pequeños o tags

**NO usar uppercase en:**
❌ Párrafos largos (difícil de leer)
❌ Títulos muy largos (H1, H2)
❌ Nombres propios normales

**Ejemplo correcto:**
```html
<!-- Correcto -->
<h1>Mixología Exclusiva para Momentos Únicos</h1>
<button>COTIZA TU EVENTO</button>

<!-- Incorrecto -->
<h1>MIXOLOGÍA EXCLUSIVA PARA MOMENTOS ÚNICOS</h1>
```

---

### **6. Negritas (Bold)**

**Usar bold:**
✅ Títulos (H1-H6)
✅ Énfasis en párrafos (máximo 10-15%)
✅ Botones
✅ Labels de formularios
✅ Navegación activa

**NO usar bold:**
❌ Playfair Display en textos largos (muy pesado)
❌ Más del 15% del contenido
❌ Todo un párrafo completo

**Ejemplo:**
```html
<p>
  Nuestro servicio incluye <strong>bartenders certificados</strong> 
  con más de 10 años de experiencia.
</p>
```

---

### **7. Cursiva (Italic)**

**Usar cursiva:**
✅ Énfasis sutil
✅ Términos extranjeros (ej: "mise en place")
✅ Quotes y testimonios (Playfair italic)
✅ Nombres de cócteles en texto (opcional)

**NO usar cursiva:**
❌ Textos largos (difícil de leer)
❌ Títulos principales
❌ Navegación

**Ejemplo:**
```html
<blockquote>
  <p style="font-style: italic;">
    La mejor experiencia de bartending que hemos tenido.
  </p>
</blockquote>
```

---

## 🎨 Ejemplos de Aplicación

### **Ejemplo 1: Hero Section**

```html
<section class="hero">
  <h1 class="hero-title">
    <!-- Playfair Display Bold, 72px, +80 tracking, color dorado -->
    Mixología Exclusiva para Momentos Únicos
  </h1>
  
  <p class="hero-subtitle">
    <!-- Montserrat Regular, 20px, line-height 1.6, color blanco -->
    Transformamos tu celebración en una experiencia memorable 
    con cócteles de autor y servicio excepcional.
  </p>
  
  <button class="btn-primary">
    <!-- Montserrat SemiBold, 16px, uppercase, +40 tracking -->
    COTIZA TU EVENTO
  </button>
</section>
```

**CSS:**
```css
.hero {
  background: #1A1A1A;
  color: #FFFFFF;
  text-align: center;
  padding: 120px 20px;
}

.hero-title {
  font-family: 'Playfair Display', serif;
  font-weight: 700;
  font-size: 72px;
  letter-spacing: 0.08em;
  line-height: 1.2;
  color: #D4AF37;
  margin-bottom: 24px;
}

.hero-subtitle {
  font-family: 'Montserrat', sans-serif;
  font-weight: 400;
  font-size: 20px;
  line-height: 1.6;
  color: #FFFFFF;
  max-width: 700px;
  margin: 0 auto 40px;
}

.btn-primary {
  font-family: 'Montserrat', sans-serif;
  font-weight: 600;
  font-size: 16px;
  letter-spacing: 0.04em;
  text-transform: uppercase;
  background: linear-gradient(135deg, #D4AF37, #F59E0B);
  color: #1A1A1A;
  padding: 16px 40px;
  border: none;
  border-radius: 50px;
  cursor: pointer;
}
```

---

### **Ejemplo 2: Sección de Contenido**

```html
<section class="content-section">
  <h2 class="section-title">
    <!-- Playfair Display SemiBold, 40px, +60 tracking -->
    Nuestros Servicios Premium
  </h2>
  
  <div class="gold-line"></div>
  
  <p class="section-intro">
    <!-- Montserrat Regular, 18px, line-height 1.6 -->
    Ofrecemos servicios de bartending exclusivos diseñados 
    para crear experiencias únicas en cada evento.
  </p>
  
  <div class="service-card">
    <h3 class="card-title">
      <!-- Montserrat Bold, 24px -->
      Bartending para Eventos
    </h3>
    <p class="card-description">
      <!-- Montserrat Regular, 16px -->
      Servicio completo de barra y bartenders profesionales 
      para tu celebración especial.
    </p>
  </div>
</section>
```

---

### **Ejemplo 3: Carta de Cócteles**

```html
<div class="cocktail-menu">
  <h3 class="menu-category">
    <!-- Playfair Display SemiBold, 28px, color dorado -->
    Clásicos Reserva
  </h3>
  
  <div class="cocktail-item">
    <h4 class="cocktail-name">
      <!-- Playfair Display SemiBold, 22px, +40 tracking -->
      Old Fashioned Reserva
    </h4>
    
    <p class="cocktail-description">
      <!-- Montserrat Regular, 16px, color gris medio -->
      Bourbon premium, angostura, azúcar demerara, 
      twist de naranja
    </p>
    
    <span class="cocktail-price">
      <!-- Montserrat SemiBold, 18px, color dorado -->
      S/ 45
    </span>
  </div>
</div>
```

---

### **Ejemplo 4: Formulario**

```html
<form class="quote-form">
  <label class="form-label">
    <!-- Montserrat SemiBold, 14px -->
    Nombre Completo *
  </label>
  
  <input 
    type="text" 
    class="form-input"
    placeholder="Ingresa tu nombre"
  >
  <!-- Input: Montserrat Regular, 16px -->
  <!-- Placeholder: Montserrat Regular, 16px, color gris medio -->
  
  <p class="form-help">
    <!-- Montserrat Regular, 14px, color gris medio -->
    Este campo es obligatorio
  </p>
</form>
```

---

## 💾 Recursos Tipográficos

### **Descarga de Fuentes:**

**Google Fonts:**
- [Playfair Display](https://fonts.google.com/specimen/Playfair+Display)
- [Montserrat](https://fonts.google.com/specimen/Montserrat)

**Formato Requerido:**
```css
Playfair Display: TTF, OTF, WOFF, WOFF2
Montserrat: TTF, OTF, WOFF, WOFF2
```

### **Kit de Tipografía Completo:**

```css
/fonts/
  ├── playfair-display/
  │   ├── PlayfairDisplay-Regular.ttf
  │   ├── PlayfairDisplay-Medium.ttf
  │   ├── PlayfairDisplay-SemiBold.ttf
  │   ├── PlayfairDisplay-Bold.ttf
  │   ├── PlayfairDisplay-Black.ttf
  │   └── PlayfairDisplay-Italic.ttf
  │
  └── montserrat/
      ├── Montserrat-Light.ttf
      ├── Montserrat-Regular.ttf
      ├── Montserrat-Medium.ttf
      ├── Montserrat-SemiBold.ttf
      ├── Montserrat-Bold.ttf
      └── Montserrat-Italic.ttf
```

---

## ✅ Checklist Tipográfico

### **Antes de Publicar, Verificar:**

- [ ] Playfair Display solo en títulos (H1, H2) y elementos destacados
- [ ] Montserrat en todo el cuerpo de texto
- [ ] Tracking amplio (+60 a +120) en títulos con Playfair
- [ ] Line-height mínimo 1.5 en cuerpo de texto
- [ ] Máximo 75 caracteres por línea en párrafos
- [ ] Contraste de color suficiente (mínimo 4.5:1)
- [ ] Texto alineado a la izquierda (no justificado)
- [ ] Uppercase solo en logo, botones y labels pequeños
- [ ] Tamaño mínimo 16px en cuerpo de texto
- [ ] Responsive: texto legible en móvil
- [ ] Negritas usadas con moderación (<15%)
- [ ] Cursiva solo para énfasis o quotes
- [ ] Fallback fonts configuradas

---

## 🚨 Errores Comunes a Evitar

❌ **Usar Playfair Display en párrafos largos**
```html
<!-- MAL -->
<p style="font-family: Playfair Display;">
  Lorem ipsum dolor sit amet, consectetur adipiscing elit...
  (texto largo)
</p>

<!-- BIEN -->
<p style="font-family: Montserrat;">
  Lorem ipsum dolor sit amet, consectetur adipiscing elit...
</p>
```

---

❌ **No aplicar tracking en títulos Playfair**
```css
/* MAL */
h1 {
  font-family: 'Playfair Display';
  letter-spacing: normal;
}

/* BIEN */
h1 {
  font-family: 'Playfair Display';
  letter-spacing: 0.08em; /* +80 */
}
```

---

❌ **Line-height muy bajo**
```css
/* MAL */
p {
  line-height: 1.2; /* Muy apretado */
}

/* BIEN */
p {
  line-height: 1.6; /* Respirable */
}
```

---

❌ **Texto largo centrado**
```css
/* MAL */
.article-content {
  text-align: center; /* Difícil de leer */
}

/* BIEN */
.article-content {
  text-align: left;
}
```

---

❌ **Uppercase en títulos largos**
```html
<!-- MAL -->
<h1 style="text-transform: uppercase;">
  MIXOLOGÍA EXCLUSIVA PARA MOMENTOS ÚNICOS EN LIMA PERÚ
</h1>

<!-- BIEN -->
<h1>
  Mixología Exclusiva para Momentos Únicos en Lima
</h1>
```

---

❌ **Mezclar demasiadas fuentes**
```css
/* MAL - No hacer esto */
h1 { font-family: 'Playfair Display'; }
h2 { font-family: 'Cormorant'; }
h3 { font-family: 'Lora'; }
p  { font-family: 'Roboto'; }

/* BIEN - Solo 2 fuentes */
h1, h2 { font-family: 'Playfair Display'; }
h3, p, button { font-family: 'Montserrat'; }
```

---

## 📱 Tipografía Responsive

### **Escalado Fluido:**

```css
/* Usando clamp() para escalado suave */
h1 {
  font-size: clamp(32px, 5vw, 72px);
}

h2 {
  font-size: clamp(24px, 4vw, 40px);
}

p {
  font-size: clamp(16px, 1.2vw, 18px);
}
```

### **Media Queries Específicas:**

```css
/* Base (Mobile First) */
body {
  font-size: 16px;
  line-height: 1.6;
}

h1 {
  font-size: 32px;
  letter-spacing: 0.06em;
}

/* Tablet */
@media (min-width: 768px) {
  h1 {
    font-size: 48px;
    letter-spacing: 0.08em;
  }
}

/* Desktop */
@media (min-width: 1024px) {
  body {
    font-size: 18px;
  }
  
  h1 {
    font-size: 72px;
  }
}

/* Large Desktop */
@media (min-width: 1440px) {
  h1 {
    font-size: 80px;
  }
}
```

---

## 🎓 Recursos Adicionales

### **Testing de Tipografía:**
- [Type Scale Calculator](https://type-scale.com/)
- [Modular Scale](https://www.modularscale.com/)
- [Font Pair](https://www.fontpair.co/)

### **Legibilidad:**
- [WebAIM Contrast Checker](https://webaim.org/resources/contrastchecker/)
- [Readable.com](https://readable.com/)

### **Performance:**
- [Google Fonts Helper](https://google-webfonts-helper.herokuapp.com/)
- [Font Squirrel Webfont Generator](https://www.fontsquirrel.com/tools/webfont-generator)

---

**Siguiente archivo:** 01C - Manual de Marca - Estilo Fotográfico y Tono de Voz

---

© 2025 La Reserva. Manual de uso exclusivo interno.