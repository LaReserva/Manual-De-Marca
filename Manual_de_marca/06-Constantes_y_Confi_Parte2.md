# 💻 LA RESERVA - CONSTANTES Y CONFIGURACIÓN
## PARTE 2: Servicios y Paquetes

**Versión:** 1.0  
**Fecha:** Octubre 2025

---

## 📄 ARCHIVO: constants.ts (CONTINUACIÓN)

### Sección 5: SERVICIOS PRINCIPALES

```typescript
// ============================================
// 5. SERVICIOS PRINCIPALES
// ============================================

/**
 * Servicios ofrecidos por La Reserva
 */
export const SERVICES = [
  {
    id: 'bartending-eventos',
    name: 'Bartending para Eventos',
    slug: 'bartending-eventos',
    description: 'Servicio completo de barra y bartenders profesionales para tu evento especial.',
    priceFrom: 1800,
    icon: 'cocktail',
    features: [
      'Bartenders profesionales certificados',
      'Barra completa equipada',
      'Cristalería premium',
      'Ingredientes frescos y garnish',
      'Setup y decoración de barra',
      'Servicio durante todo el evento',
    ],
    guestRange: '25-500',
    duration: 4,
    popular: true,
  },
  {
    id: 'mixologia-corporativa',
    name: 'Mixología Corporativa',
    slug: 'mixologia-corporativa',
    description: 'Experiencia de coctelería personalizada para eventos empresariales y team building.',
    priceFrom: 2500,
    icon: 'briefcase',
    features: [
      'Cócteles signature con branding',
      'Presentación profesional',
      'Team building de mixología',
      'Barra corporativa premium',
      'Material promocional incluido',
    ],
    guestRange: '30-500',
    duration: 4,
    popular: false,
  },
  {
    id: 'cocteles-autor',
    name: 'Cócteles de Autor',
    slug: 'cocteles-autor',
    description: 'Creación de cócteles exclusivos diseñados especialmente para tu evento íntimo.',
    priceFrom: 2200,
    icon: 'sparkles',
    features: [
      'Consulta previa personalizada',
      'Receta exclusiva creada para ti',
      'Ingredientes premium seleccionados',
      'Técnicas artesanales',
      'Presentación impecable',
    ],
    guestRange: '25-100',
    duration: 4,
    popular: false,
  },
  {
    id: 'barra-movil',
    name: 'Barra Móvil Premium',
    slug: 'barra-movil',
    description: 'Barra móvil completamente equipada con todo lo necesario para tu evento.',
    priceFrom: 800,
    icon: 'truck',
    features: [
      'Barra portátil elegante',
      'Equipo completo de bartending',
      'Decoración incluida',
      'Setup y desmontaje',
      'Variedad de diseños disponibles',
    ],
    guestRange: '20-200',
    duration: 8,
    popular: false,
  },
] as const;

// ============================================
// 6. PAQUETES PREDEFINIDOS
// ============================================

/**
 * Paquetes predefinidos de servicios
 */
export const PACKAGES = [
  {
    id: 'basico',
    name: 'Paquete Básico',
    slug: 'basico',
    description: 'Ideal para eventos íntimos',
    price: 1800,
    guestRange: '25-50',
    duration: 4,
    bartenders: 1,
    cocktails: 3,
    features: [
      '1 bartender profesional',
      'Barra básica equipada',
      '3 cócteles a elegir',
      'Cristalería y hielo',
      'Setup y limpieza',
    ],
    popular: false,
    serviceType: 'bartending-eventos',
  },
  {
    id: 'completo',
    name: 'Paquete Completo',
    slug: 'completo',
    description: 'Perfecto para bodas y eventos medianos',
    price: 3500,
    guestRange: '100-200',
    duration: 5,
    bartenders: 2,
    cocktails: 5,
    features: [
      '2 bartenders profesionales',
      'Barra premium equipada',
      '5 cócteles de autor',
      'Cristalería premium',
      'Decoración de barra',
      'Garnish artístico',
      'Setup y limpieza completa',
    ],
    popular: true,
    serviceType: 'bartending-eventos',
  },
  {
    id: 'premium',
    name: 'Paquete Premium',
    slug: 'premium',
    description: 'Experiencia exclusiva para eventos grandes',
    price: 6500,
    guestRange: '200-500',
    duration: 6,
    bartenders: 3,
    cocktails: 8,
    features: [
      '3+ bartenders profesionales',
      'Doble barra premium',
      'Cócteles de autor ilimitados',
      'Cristalería de lujo',
      'Decoración personalizada',
      'Garnish gourmet',
      'Sommelier de cócteles',
      'Servicio de fotografía de bebidas',
      'Setup, limpieza y coordinación completa',
    ],
    popular: false,
    serviceType: 'bartending-eventos',
  },
] as const;

// ============================================
// 7. CÓCTELES DESTACADOS
// ============================================

/**
 * Cócteles para mostrar en portafolio/menú
 */
export const FEATURED_COCKTAILS = [
  {
    id: 'pisco-sour-reserva',
    name: 'Pisco Sour Reserva',
    description: 'Nuestro clásico peruano con un toque especial',
    category: 'Clásicos',
    ingredients: ['Pisco acholado', 'Limón', 'Jarabe', 'Amargo de angostura'],
    difficulty: 'medium',
  },
  {
    id: 'old-fashioned-ahumado',
    name: 'Old Fashioned Ahumado',
    description: 'Bourbon premium con ahumado artesanal',
    category: 'Clásicos',
    ingredients: ['Bourbon', 'Angostura', 'Azúcar demerara', 'Twist de naranja'],
    difficulty: 'hard',
  },
  {
    id: 'margarita-maracuya',
    name: 'Margarita de Maracuyá',
    description: 'Fusión tropical con maracuyá fresco',
    category: 'Tropicales',
    ingredients: ['Tequila', 'Triple sec', 'Maracuyá', 'Limón'],
    difficulty: 'medium',
  },
  {
    id: 'mojito-clasico',
    name: 'Mojito Clásico',
    description: 'Refrescante cóctel cubano',
    category: 'Clásicos',
    ingredients: ['Ron blanco', 'Menta', 'Limón', 'Azúcar', 'Soda'],
    difficulty: 'easy',
  },
  {
    id: 'negroni',
    name: 'Negroni',
    description: 'Clásico italiano amargo y sofisticado',
    category: 'Clásicos',
    ingredients: ['Gin', 'Campari', 'Vermut rojo'],
    difficulty: 'easy',
  },
] as const;

// ============================================
// 8. ADD-ONS Y PERSONALIZACIONES
// ============================================

/**
 * Servicios adicionales disponibles
 */
export const ADD_ONS = [
  {
    id: 'decoracion-tematica',
    name: 'Decoración Temática',
    description: 'Decoración personalizada de barra según tema del evento',
    price: 400,
    unit: 'evento',
  },
  {
    id: 'bartender-extra',
    name: 'Bartender Adicional',
    description: 'Bartender profesional extra por 4 horas',
    price: 300,
    unit: 'bartender',
  },
  {
    id: 'hora-extra',
    name: 'Hora Adicional',
    description: 'Extensión de servicio por hora adicional',
    price: 80,
    unit: 'hora/bartender',
  },
  {
    id: 'coctel-signature',
    name: 'Cóctel Signature',
    description: 'Creación de cóctel exclusivo para tu evento',
    price: 350,
    unit: 'cóctel',
  },
  {
    id: 'tasting-session',
    name: 'Tasting Session',
    description: 'Degustación previa de cócteles (hasta 6 personas)',
    price: 250,
    unit: 'sesión',
  },
  {
    id: 'workshop',
    name: 'Workshop de Mixología',
    description: 'Taller de preparación de cócteles (1 hora)',
    price: 500,
    unit: 'hora',
  },
  {
    id: 'estacion-mocktails',
    name: 'Estación de Mocktails',
    description: 'Barra separada de cócteles sin alcohol',
    price: 400,
    unit: 'estación',
  },
  {
    id: 'branding-corporativo',
    name: 'Branding Corporativo',
    description: 'Servilletas, coasters y menú con logo de empresa',
    price: 600,
    unit: 'evento',
  },
] as const;

// ============================================
// 9. PRECIOS Y DESCUENTOS
// ============================================

/**
 * Estructura de descuentos
 */
export const DISCOUNTS = {
  recurrentClient: {
    second: 0.10, // 10%
    third: 0.15,  // 15%
    frequent: 0.20, // 20%
  },
  largeEvents: {
    '200-299': 0.05, // 5%
    '300-499': 0.08, // 8%
    '500+': 0.10,    // 10%
  },
  lowSeason: {
    months: [1, 2, 3], // Enero, Febrero, Marzo
    discount: 0.15,     // 15%
  },
  earlyPayment: {
    daysInAdvance: 30,
    discount: 0.05, // 5%
  },
  referral: {
    referrer: 100,  // S/ 100 off
    referred: 50,   // S/ 50 off
  },
} as const;

/**
 * Políticas de pago
 */
export const PAYMENT_POLICIES = {
  deposit: {
    percentage: 50,
    description: '50% de adelanto para confirmar',
  },
  balance: {
    dueDate: 'Antes del evento',
    description: '50% restante antes o el día del evento',
  },
  methods: [
    { id: 'transfer', name: 'Transferencia bancaria', fee: 0 },
    { id: 'deposit', name: 'Depósito bancario', fee: 0 },
    { id: 'yape', name: 'Yape / Plin', fee: 0 },
    { id: 'cash', name: 'Efectivo', fee: 0 },
  ],
} as const;

/**
 * FIN DE LA PARTE 2
 * Continúa en: 06C-CONSTANTES-Y-CONFIG-Parte3.md
 */
```

---

## ✅ VERIFICACIÓN - PARTE 2

- [ ] Servicios definidos correctamente
- [ ] Precios actualizados
- [ ] Features de cada servicio completas
- [ ] Paquetes con toda la información
- [ ] Add-ons disponibles listados
- [ ] Políticas de descuento configuradas

---

**Próximo archivo:** Parte 3 - Tipos TypeScript

© 2025 La Reserva