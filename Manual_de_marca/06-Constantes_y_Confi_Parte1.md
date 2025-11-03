# 💻 LA RESERVA - CONSTANTES Y CONFIGURACIÓN
## PARTE 1: Índice y constants.ts (Parte 1)

**Versión:** 1.0  
**Fecha:** Octubre 2025  
**Tiempo de lectura:** 20 minutos

---

## 📑 ÍNDICE GENERAL DEL DOCUMENTO 06

Este documento está dividido en **6 partes** para facilitar la lectura:

### Parte 1 (Este archivo)
- Índice general
- Introducción
- `constants.ts` - Sección 1: Información básica y contacto

### Parte 2
- `constants.ts` - Sección 2: Servicios y paquetes
- `constants.ts` - Sección 3: Configuraciones de UI

### Parte 3
- `types/index.ts` - Tipos TypeScript completos

### Parte 4
- `utils.ts` - Funciones de utilidad

### Parte 5
- `validators.ts` - Validadores con Zod
- `formatters.ts` - Formateo de datos

### Parte 6
- `whatsapp.ts` - Helpers de WhatsApp
- Variables de entorno
- Configuraciones de servicios externos

---

## 🎯 INTRODUCCIÓN

El archivo **06-CONSTANTES-Y-CONFIG** contiene todo el código reutilizable del proyecto La Reserva.

### Propósito
- Centralizar constantes y configuraciones
- Evitar valores "mágicos" hardcodeados
- Facilitar mantenimiento y escalabilidad
- Proporcionar tipos TypeScript seguros

### Estructura de Archivos

```css
src/
├── utils/
│   ├── constants.ts         ← Constantes del proyecto
│   ├── validators.ts         ← Validadores Zod
│   ├── formatters.ts         ← Formateo de datos
│   ├── utils.ts              ← Utilidades generales
│   └── whatsapp.ts           ← Helpers WhatsApp
│
├── types/
│   └── index.ts              ← Tipos TypeScript
│
└── lib/
    ├── supabase.ts           ← Cliente Supabase
    └── resend.ts             ← Cliente Resend
```

---

## 📄 ARCHIVO: constants.ts (PARTE 1)

### Ubicación: `src/utils/constants.ts`

```typescript
// src/utils/constants.ts

/**
 * LA RESERVA - CONSTANTES DEL PROYECTO
 * 
 * Centraliza todas las constantes utilizadas en el proyecto.
 * 
 * @version 1.0
 * @date Octubre 2025
 */

// ============================================
// 1. INFORMACIÓN BÁSICA
// ============================================

export const SITE_URL = import.meta.env.PUBLIC_SITE_URL || 'https://lareserva.pe';
export const API_URL = `${SITE_URL}/api`;

export const SITE_INFO = {
  name: 'La Reserva',
  tagline: 'Mixología Exclusiva',
  fullName: 'La Reserva - Mixología Exclusiva',
  description: 'Bartending premium para eventos exclusivos en Lima, Perú.',
  location: 'Lima, Perú',
  founded: 2015,
  yearsOfExperience: 10,
} as const;

export const CONTACT_INFO = {
  phone: '+51999888777',
  phoneFormatted: '+51 999 888 777',
  email: 'lareservabartending@gmail.com',
  whatsapp: '+51999888777',
  whatsappUrl: 'https://wa.me/51999888777',
  address: 'Lima, Perú',
} as const;

export const BUSINESS_HOURS = {
  weekdays: 'Lunes - Viernes: 9:00 AM - 5:00 PM',
  saturday: 'Sábado: 9:00 AM - 1:00 PM',
  sunday: 'Domingo: Cerrado',
  responseTime: 'Respuestas dentro de 1 hora',
} as const;

export const SOCIAL_LINKS = {
  instagram: {
    url: 'https://instagram.com/lareservabar',
    handle: '@lareservabar',
  },
  facebook: {
    url: 'https://facebook.com/lareservabar',
    handle: 'La Reserva',
  },
  tiktok: {
    url: 'https://tiktok.com/@lareserva',
    handle: '@lareserva',
  },
} as const;

// ============================================
// 2. LÍMITES Y VALIDACIONES
// ============================================

export const GUEST_LIMITS = {
  min: 25,
  max: 500,
  recommended: 100,
} as const;

export const GUEST_RANGES = [
  { value: '25-50', label: '25 - 50 invitados' },
  { value: '51-100', label: '51 - 100 invitados' },
  { value: '101-200', label: '101 - 200 invitados' },
  { value: '201-300', label: '201 - 300 invitados' },
  { value: '301-500', label: '301 - 500 invitados' },
  { value: '500+', label: 'Más de 500 invitados' },
] as const;

export const VALIDATION = {
  name: { min: 2, max: 100 },
  email: { max: 255 },
  phone: { min: 9, max: 15 },
  message: { min: 10, max: 1000 },
  guests: { min: 25, max: 500 },
} as const;

// ============================================
// 3. TIPOS DE EVENTOS Y ESTADOS
// ============================================

export const EVENT_TYPES = [
  { value: 'boda', label: 'Boda', icon: '💍' },
  { value: 'corporativo', label: 'Evento Corporativo', icon: '🏢' },
  { value: 'cumpleanos', label: 'Cumpleaños', icon: '🎂' },
  { value: 'aniversario', label: 'Aniversario', icon: '🥂' },
  { value: 'graduacion', label: 'Graduación', icon: '🎓' },
  { value: 'baby-shower', label: 'Baby Shower', icon: '👶' },
  { value: 'otro', label: 'Otro', icon: '🎉' },
] as const;

export const QUOTE_STATUSES = {
  new: { label: 'Nueva', color: 'blue' },
  contacted: { label: 'Contactada', color: 'yellow' },
  quoted: { label: 'Cotizada', color: 'purple' },
  converted: { label: 'Convertida', color: 'green' },
  declined: { label: 'Declinada', color: 'red' },
} as const;

export const EVENT_STATUSES = {
  pending: { label: 'Pendiente', color: 'yellow' },
  confirmed: { label: 'Confirmado', color: 'green' },
  completed: { label: 'Completado', color: 'blue' },
  cancelled: { label: 'Cancelado', color: 'red' },
} as const;

// ============================================
// 4. MENSAJES
// ============================================

export const ERROR_MESSAGES = {
  required: 'Este campo es obligatorio',
  invalidEmail: 'Email inválido',
  invalidPhone: 'Teléfono inválido',
  minLength: (min: number) => `Mínimo ${min} caracteres`,
  maxLength: (max: number) => `Máximo ${max} caracteres`,
  minValue: (min: number) => `Valor mínimo: ${min}`,
  maxValue: (max: number) => `Valor máximo: ${max}`,
  pastDate: 'La fecha debe ser futura',
  generic: 'Ocurrió un error. Intenta de nuevo.',
} as const;

export const SUCCESS_MESSAGES = {
  quoteSubmitted: '¡Gracias! Tu cotización ha sido enviada.',
  contactSubmitted: '¡Mensaje enviado!',
  subscribed: '¡Suscripción exitosa!',
  copied: 'Copiado al portapapeles',
} as const;
```

---

**Continúa en:** Parte 2 - Servicios y Paquetes

© 2025 La Reserva