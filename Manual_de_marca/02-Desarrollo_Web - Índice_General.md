# 💻 LA RESERVA - DESARROLLO WEB
## Índice General de Archivos Técnicos

**Versión:** 1.0  
**Fecha:** Octubre 2025  
**Stack:** Astro + TypeScript + Supabase + Tailwind CSS

---

## 📚 DIVISIÓN DE ARCHIVOS

Este módulo de Desarrollo Web está dividido en **4 archivos** especializados para facilitar la lectura y el seguimiento:

---

### **📄 Archivo 02A: Introducción y Stack Tecnológico**
**Archivo:** `02A-INTRO-Y-STACK.md`

**Contenido:**
- Introducción al proyecto
- Objetivos y arquitectura
- Stack tecnológico completo explicado
- Por qué cada tecnología
- Requisitos previos (software, cuentas, conocimientos)

**Para quién:**
- Desarrolladores nuevos en el proyecto
- Team leads que quieren entender la arquitectura
- Stakeholders técnicos

**Tiempo de lectura:** 15 minutos

---

### **📄 Archivo 02B: Instalación y Configuración**
**Archivo:** `02B-INSTALACION-Y-CONFIG.md`

**Contenido:**
- Instalación de pnpm
- Creación del proyecto Astro
- Instalación de todas las dependencias (con comentarios)
- Configuración de Astro
- Configuración de Tailwind CSS
- Configuración de TypeScript
- Variables de entorno
- Configuración de Prettier y Git

**Para quién:**
- Desarrolladores que van a hacer el setup inicial
- Nuevos miembros del equipo

**Tiempo de lectura:** 20 minutos  
**Tiempo de ejecución:** 30-45 minutos

---

### **📄 Archivo 02C: Estructura y Estilos**
**Archivo:** `02C-ESTRUCTURA-Y-ESTILOS.md`

**Contenido:**
- Estructura completa del proyecto (carpetas y archivos)
- Explicación de cada directorio
- Sistema de rutas de Astro
- Estilos globales (global.css completo)
- Componentes CSS reutilizables
- Utilidades de Tailwind customizadas

**Para quién:**
- Desarrolladores frontend
- Diseñadores que trabajan con desarrollo

**Tiempo de lectura:** 15 minutos

---

### **📄 Archivo 02D: Utilidades y Mejores Prácticas**
**Archivo:** `02D-UTILS-Y-PRACTICAS.md`

**Contenido:**
- Archivo utils.ts (funciones de utilidad)
- Archivo constants.ts (constantes del proyecto)
- Archivo whatsapp.ts (helpers de WhatsApp)
- Archivo validators.ts (validaciones con Zod)
- Mejores prácticas de código
- Convenciones de nomenclatura
- Seguridad y performance
- Testing (opcional)
- Comandos útiles

**Para quién:**
- Todo el equipo de desarrollo
- Code reviewers
- Nuevos desarrolladores

**Tiempo de lectura:** 20 minutos

---

## 🎯 ORDEN DE LECTURA RECOMENDADO

### **Para Desarrolladores Nuevos:**
1. Leer **02A** - Entender el stack y arquitectura
2. Ejecutar **02B** - Hacer el setup del proyecto
3. Revisar **02C** - Familiarizarse con la estructura
4. Estudiar **02D** - Conocer utilidades y estándares

### **Para Desarrolladores Experimentados:**
1. Escanear **02A** - Verificar stack
2. Ejecutar **02B** - Setup rápido
3. Referencia **02C** y **02D** - Según necesidad

### **Para Team Leads / Arquitectos:**
1. Leer **02A** - Decisiones de arquitectura
2. Revisar **02D** - Estándares y prácticas
3. Opcional **02B** y **02C** - Si harán setup o code review

---

## 📊 RESUMEN DE CONTENIDO

### **Stack Principal:**
```css
Frontend:
├── Astro 4.x (Framework principal)
├── React 18 (Componentes interactivos)
├── TypeScript (Tipado estático)
└── Tailwind CSS (Estilos)

Backend:
└── Supabase
    ├── PostgreSQL (Database)
    ├── Auth (Autenticación)
    ├── Storage (Imágenes)
    └── Edge Functions (Serverless)

Tools:
├── pnpm (Package manager)
├── Prettier (Code formatter)
└── Git (Version control)
```

---

## 🔧 REQUISITOS MÍNIMOS

Antes de empezar con cualquier archivo, asegúrate de tener:

**Software:**
- ✅ Node.js 18.14.1+
- ✅ pnpm (instalar con npm)
- ✅ Git
- ✅ VS Code (recomendado)

**Cuentas:**
- ✅ GitHub (para repositorio)
- ✅ Supabase (free tier)
- ✅ Resend (free tier)

**Conocimientos:**
- ✅ JavaScript/TypeScript básico
- ✅ HTML/CSS
- ✅ Terminal básico
- ✅ Git básico

---

## 📝 CHECKLIST GENERAL

### **Fase 1: Preparación**
- [ ] Leer archivo 02A (Intro y Stack)
- [ ] Verificar requisitos de software
- [ ] Crear cuentas necesarias (Supabase, Resend)
- [ ] Preparar VS Code con extensiones

### **Fase 2: Setup**
- [ ] Seguir archivo 02B paso a paso
- [ ] Instalar pnpm
- [ ] Crear proyecto
- [ ] Instalar dependencias
- [ ] Configurar todo
- [ ] Verificar que `pnpm dev` funciona

### **Fase 3: Familiarización**
- [ ] Leer archivo 02C (Estructura)
- [ ] Entender organización de carpetas
- [ ] Revisar estilos globales

### **Fase 4: Desarrollo**
- [ ] Usar archivo 02D como referencia
- [ ] Seguir mejores prácticas
- [ ] Usar utilidades predefinidas

---

## 🚀 INICIO RÁPIDO

Si ya tienes experiencia y quieres empezar rápido:

```bash
# 1. Instalar pnpm
npm install -g pnpm

# 2. Crear proyecto
pnpm create astro@latest la-reserva
# Seleccionar: Empty, Yes, Yes (Strict), Yes

# 3. Entrar e instalar dependencias
cd la-reserva
# Copiar y pegar todos los comandos del archivo 02B

# 4. Configurar archivos
# Copiar configuraciones de 02B:
# - astro.config.mjs
# - tailwind.config.mjs
# - tsconfig.json
# - .env.example

# 5. Iniciar desarrollo
pnpm dev
```

---

## 📞 SOPORTE

**Dudas técnicas:**
- Revisa primero el archivo correspondiente
- Consulta documentación oficial de cada tech
- Pregunta al team lead

**Errores comunes:**
- Verificar versiones de Node/pnpm
- Revisar que `.env` esté configurado
- Borrar `node_modules` y reinstalar si hay problemas

---

## 🔄 ACTUALIZACIONES

**Versión 1.0 - Octubre 2025**
- Setup inicial completo
- 4 archivos de documentación
- Stack: Astro + React + Supabase

**Próximas versiones:**
- Agregar testing setup
- Docker configuration (opcional)
- CI/CD pipelines

---

**Siguiente archivo:** 02A - Introducción y Stack Tecnológico

---

© 2025 La Reserva. Documentación técnica del proyecto.