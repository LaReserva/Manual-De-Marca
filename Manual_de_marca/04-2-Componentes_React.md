# 💻 LA RESERVA - DESARROLLO WEB
## PARTE 4-2: Componentes React Interactivos

**Versión:** 1.0  
**Fecha:** Octubre 2025  
**Tiempo de lectura:** 25 minutos

---

## 📑 CONTENIDO

1. Modal Component
2. Toast Notifications
3. QuoteForm Component
4. Hero Section Component
5. Testimonials Slider

---

## 1. MODAL COMPONENT

### 1.1 Modal.tsx

```css
// src/components/ui/Modal.tsx
import { useEffect, useState } from 'react';
import { createPortal } from 'react-dom';
import { motion, AnimatePresence } from 'framer-motion';
import { cn } from '@/utils/utils';

interface ModalProps {
  isOpen: boolean;
  onClose: () => void;
  title?: string;
  size?: 'sm' | 'md' | 'lg' | 'xl' | 'full';
  children: React.ReactNode;
  showCloseButton?: boolean;
  closeOnOverlayClick?: boolean;
}

export function Modal({
  isOpen,
  onClose,
  title,
  size = 'md',
  children,
  showCloseButton = true,
  closeOnOverlayClick = true,
}: ModalProps) {
  const [mounted, setMounted] = useState(false);

  useEffect(() => {
    setMounted(true);
    return () => setMounted(false);
  }, []);

  useEffect(() => {
    if (isOpen) {
      document.body.style.overflow = 'hidden';
    } else {
      document.body.style.overflow = 'unset';
    }

    return () => {
      document.body.style.overflow = 'unset';
    };
  }, [isOpen]);

  const sizeClasses = {
    sm: 'max-w-md',
    md: 'max-w-lg',
    lg: 'max-w-2xl',
    xl: 'max-w-4xl',
    full: 'max-w-full mx-4',
  };

  if (!mounted) return null;

  return createPortal(
    <AnimatePresence>
      {isOpen && (
        <>
          {/* Overlay */}
          <motion.div
            initial={{ opacity: 0 }}
            animate={{ opacity: 1 }}
            exit={{ opacity: 0 }}
            onClick={closeOnOverlayClick ? onClose : undefined}
            className="fixed inset-0 bg-black/60 backdrop-blur-sm z-50"
          />

          {/* Modal */}
          <div className="fixed inset-0 z-50 flex items-center justify-center p-4">
            <motion.div
              initial={{ opacity: 0, scale: 0.95, y: 20 }}
              animate={{ opacity: 1, scale: 1, y: 0 }}
              exit={{ opacity: 0, scale: 0.95, y: 20 }}
              className={cn(
                'relative bg-white rounded-lg shadow-2xl w-full',
                sizeClasses[size]
              )}
            >
              {/* Header */}
              {(title || showCloseButton) && (
                <div className="flex items-center justify-between px-6 py-4 border-b border-secondary-200">
                  {title && (
                    <h3 className="text-xl font-display font-semibold text-secondary-600">
                      {title}
                    </h3>
                  )}
                  {showCloseButton && (
                    <button
                      onClick={onClose}
                      className="p-2 hover:bg-secondary-100 rounded-full transition-colors"
                      aria-label="Cerrar modal"
                    >
                      <svg
                        className="w-5 h-5 text-secondary-600"
                        fill="none"
                        stroke="currentColor"
                        viewBox="0 0 24 24"
                      >
                        <path
                          strokeLinecap="round"
                          strokeLinejoin="round"
                          strokeWidth={2}
                          d="M6 18L18 6M6 6l12 12"
                        />
                      </svg>
                    </button>
                  )}
                </div>
              )}

              {/* Content */}
              <div className="px-6 py-4 max-h-[calc(100vh-200px)] overflow-y-auto">
                {children}
              </div>
            </motion.div>
          </div>
        </>
      )}
    </AnimatePresence>,
    document.body
  );
}
```

### 1.2 Ejemplo de uso

```css
// En cualquier componente React
import { useState } from 'react';
import { Modal } from '@/components/ui/Modal';

export function MyComponent() {
  const [isModalOpen, setIsModalOpen] = useState(false);

  return (
    <>
      <button onClick={() => setIsModalOpen(true)}>
        Abrir Modal
      </button>

      <Modal
        isOpen={isModalOpen}
        onClose={() => setIsModalOpen(false)}
        title="Título del Modal"
        size="md"
      >
        <p>Contenido del modal aquí</p>
        <button onClick={() => setIsModalOpen(false)}>
          Cerrar
        </button>
      </Modal>
    </>
  );
}
```

---

## 2. TOAST NOTIFICATIONS

### 2.1 Toast Context y Provider

```css
// src/components/ui/Toast.tsx
import { createContext, useContext, useState, useCallback } from 'react';
import { motion, AnimatePresence } from 'framer-motion';
import { cn } from '@/utils/utils';

type ToastType = 'success' | 'error' | 'warning' | 'info';

interface Toast {
  id: string;
  message: string;
  type: ToastType;
}

interface ToastContextType {
  showToast: (message: string, type?: ToastType) => void;
}

const ToastContext = createContext<ToastContextType | undefined>(undefined);

export function ToastProvider({ children }: { children: React.ReactNode }) {
  const [toasts, setToasts] = useState<Toast[]>([]);

  const showToast = useCallback((message: string, type: ToastType = 'info') => {
    const id = Math.random().toString(36).substr(2, 9);
    const newToast = { id, message, type };

    setToasts((prev) => [...prev, newToast]);

    // Auto-remove after 5 seconds
    setTimeout(() => {
      setToasts((prev) => prev.filter((toast) => toast.id !== id));
    }, 5000);
  }, []);

  const removeToast = useCallback((id: string) => {
    setToasts((prev) => prev.filter((toast) => toast.id !== id));
  }, []);

  return (
    <ToastContext.Provider value={{ showToast }}>
      {children}
      
      {/* Toast Container */}
      <div className="fixed bottom-4 right-4 z-50 space-y-2">
        <AnimatePresence>
          {toasts.map((toast) => (
            <ToastItem
              key={toast.id}
              toast={toast}
              onClose={() => removeToast(toast.id)}
            />
          ))}
        </AnimatePresence>
      </div>
    </ToastContext.Provider>
  );
}

function ToastItem({ toast, onClose }: { toast: Toast; onClose: () => void }) {
  const typeConfig = {
    success: {
      bg: 'bg-green-50',
      border: 'border-green-500',
      text: 'text-green-800',
      icon: '✓',
    },
    error: {
      bg: 'bg-red-50',
      border: 'border-red-500',
      text: 'text-red-800',
      icon: '✕',
    },
    warning: {
      bg: 'bg-yellow-50',
      border: 'border-yellow-500',
      text: 'text-yellow-800',
      icon: '⚠',
    },
    info: {
      bg: 'bg-blue-50',
      border: 'border-blue-500',
      text: 'text-blue-800',
      icon: 'ℹ',
    },
  };

  const config = typeConfig[toast.type];

  return (
    <motion.div
      initial={{ opacity: 0, x: 100 }}
      animate={{ opacity: 1, x: 0 }}
      exit={{ opacity: 0, x: 100 }}
      className={cn(
        'flex items-center gap-3 px-4 py-3 rounded-lg shadow-lg border-l-4 min-w-[300px]',
        config.bg,
        config.border
      )}
    >
      <span className="text-2xl">{config.icon}</span>
      <p className={cn('flex-1 font-medium', config.text)}>{toast.message}</p>
      <button
        onClick={onClose}
        className={cn('p-1 hover:opacity-70 transition-opacity', config.text)}
      >
        <svg className="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
          <path strokeLinecap="round" strokeLinejoin="round" strokeWidth={2} d="M6 18L18 6M6 6l12 12" />
        </svg>
      </button>
    </motion.div>
  );
}

export function useToast() {
  const context = useContext(ToastContext);
  if (!context) {
    throw new Error('useToast must be used within ToastProvider');
  }
  return context;
}
```

### 2.2 Agregar Provider en Layout

```css
---
// src/layouts/BaseLayout.astro (modificar)
import { ToastProvider } from '@/components/ui/Toast';
---

<!doctype html>
<html>
  <head>...</head>
  <body>
    <ToastProvider client:load>
      <slot />
    </ToastProvider>
  </body>
</html>
```

### 2.3 Uso del Toast

```css
// En cualquier componente
import { useToast } from '@/components/ui/Toast';

export function MyForm() {
  const { showToast } = useToast();

  const handleSubmit = async () => {
    try {
      // ... lógica
      showToast('¡Formulario enviado con éxito!', 'success');
    } catch (error) {
      showToast('Error al enviar el formulario', 'error');
    }
  };

  return <form onSubmit={handleSubmit}>...</form>;
}
```

---

## 3. QUOTEFORM COMPONENT

### 3.1 QuoteForm.tsx (Formulario de Cotización)

```css
// src/components/forms/QuoteForm.tsx
import { useState } from 'react';
import { useForm } from 'react-hook-form';
import { zodResolver } from '@hookform/resolvers/zod';
import { quoteSchema, type QuoteFormData } from '@/utils/validators';
import { EVENT_TYPES } from '@/utils/constants';
import { supabase } from '@/lib/supabase';
import { useToast } from '@/components/ui/Toast';
import { cn } from '@/utils/utils';

export function QuoteForm() {
  const [isSubmitting, setIsSubmitting] = useState(false);
  const { showToast } = useToast();

  const {
    register,
    handleSubmit,
    reset,
    formState: { errors },
  } = useForm<QuoteFormData>({
    resolver: zodResolver(quoteSchema),
    defaultValues: {
      guestCount: 100,
    },
  });

  const onSubmit = async (data: QuoteFormData) => {
    try {
      setIsSubmitting(true);

      const { error } = await supabase.from('quotes').insert({
        client_name: data.name,
        client_email: data.email,
        client_phone: data.phone,
        event_type: data.eventType,
        event_date: data.eventDate,
        guest_count: data.guestCount,
        message: data.message,
        status: 'new',
      });

      if (error) throw error;

      showToast('¡Cotización enviada! Te contactaremos pronto.', 'success');
      reset();

      // Opcional: Trigger email via Edge Function
      // await fetch('/api/send-quote-email', { method: 'POST', body: JSON.stringify(data) });
    } catch (error) {
      console.error('Error:', error);
      showToast('Error al enviar cotización. Por favor intenta de nuevo.', 'error');
    } finally {
      setIsSubmitting(false);
    }
  };

  return (
    <form onSubmit={handleSubmit(onSubmit)} className="space-y-6">
      {/* Nombre */}
      <div>
        <label htmlFor="name" className="label">
          Nombre completo <span className="text-red-500">*</span>
        </label>
        <input
          {...register('name')}
          id="name"
          type="text"
          className={cn('input', errors.name && 'border-red-500')}
          placeholder="Juan Pérez"
        />
        {errors.name && (
          <p className="text-sm text-red-500 mt-1">{errors.name.message}</p>
        )}
      </div>

      {/* Email */}
      <div>
        <label htmlFor="email" className="label">
          Email <span className="text-red-500">*</span>
        </label>
        <input
          {...register('email')}
          id="email"
          type="email"
          className={cn('input', errors.email && 'border-red-500')}
          placeholder="juan@ejemplo.com"
        />
        {errors.email && (
          <p className="text-sm text-red-500 mt-1">{errors.email.message}</p>
        )}
      </div>

      {/* Teléfono */}
      <div>
        <label htmlFor="phone" className="label">
          Teléfono / WhatsApp <span className="text-red-500">*</span>
        </label>
        <input
          {...register('phone')}
          id="phone"
          type="tel"
          className={cn('input', errors.phone && 'border-red-500')}
          placeholder="999 888 777"
        />
        {errors.phone && (
          <p className="text-sm text-red-500 mt-1">{errors.phone.message}</p>
        )}
      </div>

      {/* Tipo de Evento */}
      <div>
        <label htmlFor="eventType" className="label">
          Tipo de evento <span className="text-red-500">*</span>
        </label>
        <select
          {...register('eventType')}
          id="eventType"
          className={cn('input appearance-none', errors.eventType && 'border-red-500')}
        >
          <option value="">Selecciona un tipo</option>
          {EVENT_TYPES.map((type) => (
            <option key={type.value} value={type.value}>
              {type.label}
            </option>
          ))}
        </select>
        {errors.eventType && (
          <p className="text-sm text-red-500 mt-1">{errors.eventType.message}</p>
        )}
      </div>

      {/* Fecha del Evento */}
      <div>
        <label htmlFor="eventDate" className="label">
          Fecha del evento <span className="text-red-500">*</span>
        </label>
        <input
          {...register('eventDate')}
          id="eventDate"
          type="date"
          min={new Date().toISOString().split('T')[0]}
          className={cn('input', errors.eventDate && 'border-red-500')}
        />
        {errors.eventDate && (
          <p className="text-sm text-red-500 mt-1">{errors.eventDate.message}</p>
        )}
      </div>

      {/* Número de Invitados */}
      <div>
        <label htmlFor="guestCount" className="label">
          Número de invitados <span className="text-red-500">*</span>
        </label>
        <input
          {...register('guestCount', { valueAsNumber: true })}
          id="guestCount"
          type="number"
          min={25}
          max={500}
          className={cn('input', errors.guestCount && 'border-red-500')}
        />
        {errors.guestCount && (
          <p className="text-sm text-red-500 mt-1">{errors.guestCount.message}</p>
        )}
        <p className="text-sm text-secondary-400 mt-1">Mínimo 25, máximo 500</p>
      </div>

      {/* Mensaje Opcional */}
      <div>
        <label htmlFor="message" className="label">
          Mensaje adicional (opcional)
        </label>
        <textarea
          {...register('message')}
          id="message"
          rows={4}
          className="input resize-none"
          placeholder="Cuéntanos más sobre tu evento..."
        />
      </div>

      {/* Submit Button */}
      <button
        type="submit"
        disabled={isSubmitting}
        className="btn-primary w-full"
      >
        {isSubmitting ? 'Enviando...' : 'Solicitar Cotización'}
      </button>

      <p className="text-sm text-secondary-400 text-center">
        Te contactaremos dentro de las próximas 24 horas
      </p>
    </form>
  );
}
```

### 3.2 Uso en página Astro

```css
---
// src/pages/cotizacion.astro
import PageLayout from '@/layouts/PageLayout.astro';
import { QuoteForm } from '@/components/forms/QuoteForm';
---

<PageLayout title="Solicitar Cotización">
  <section class="section">
    <div class="container-custom max-w-2xl">
      <div class="text-center mb-12">
        <h1 class="mb-4">Solicita tu Cotización</h1>
        <p class="text-lg text-secondary-400">
          Completa el formulario y te contactaremos pronto
        </p>
      </div>

      <div class="card">
        <QuoteForm client:load />
      </div>
    </div>
  </section>
</PageLayout>
```

---

## 4. HERO SECTION COMPONENT

### 4.1 Hero.tsx (Hero animado)

```css
// src/components/sections/Hero.tsx
import { motion } from 'framer-motion';
import { getWhatsAppUrl } from '@/utils/whatsapp';

interface HeroProps {
  title: string;
  subtitle: string;
  ctaPrimary?: { text: string; href: string };
  ctaSecondary?: { text: string; href: string };
  backgroundImage?: string;
}

export function Hero({
  title,
  subtitle,
  ctaPrimary = { text: 'Cotizar Evento', href: '/cotizacion' },
  ctaSecondary = { text: 'Ver Portafolio', href: '/portafolio' },
  backgroundImage = '/images/hero-bg.jpg',
}: HeroProps) {
  const handleWhatsApp = () => {
    const message = '¡Hola! Me gustaría obtener más información sobre sus servicios.';
    window.open(getWhatsAppUrl(message), '_blank');
  };

  return (
    <section className="relative min-h-screen flex items-center justify-center overflow-hidden">
      {/* Background Image */}
      <div
        className="absolute inset-0 bg-cover bg-center"
        style={{ backgroundImage: `url(${backgroundImage})` }}
      >
        <div className="absolute inset-0 bg-black/60" />
      </div>

      {/* Content */}
      <div className="relative z-10 container-custom text-center text-white">
        <motion.div
          initial={{ opacity: 0, y: 30 }}
          animate={{ opacity: 1, y: 0 }}
          transition={{ duration: 0.8 }}
        >
          <h1 className="text-5xl md:text-6xl lg:text-7xl font-display font-bold mb-6 tracking-wide">
            {title}
          </h1>
          
          <motion.p
            initial={{ opacity: 0, y: 20 }}
            animate={{ opacity: 1, y: 0 }}
            transition={{ duration: 0.8, delay: 0.2 }}
            className="text-xl md:text-2xl mb-12 max-w-3xl mx-auto"
          >
            {subtitle}
          </motion.p>

          <motion.div
            initial={{ opacity: 0, y: 20 }}
            animate={{ opacity: 1, y: 0 }}
            transition={{ duration: 0.8, delay: 0.4 }}
            className="flex flex-col sm:flex-row gap-4 justify-center"
          >
            <a href={ctaPrimary.href} className="btn-primary">
              {ctaPrimary.text}
            </a>
            <a href={ctaSecondary.href} className="btn-outline">
              {ctaSecondary.text}
            </a>
          </motion.div>

          {/* WhatsApp Float Button */}
          <motion.button
            initial={{ opacity: 0, scale: 0 }}
            animate={{ opacity: 1, scale: 1 }}
            transition={{ duration: 0.5, delay: 0.6 }}
            onClick={handleWhatsApp}
            className="fixed bottom-6 right-6 z-50 bg-green-500 hover:bg-green-600 text-white p-4 rounded-full shadow-2xl transition-all hover:scale-110"
            aria-label="Contactar por WhatsApp"
          >
            <svg className="w-8 h-8" fill="currentColor" viewBox="0 0 24 24">
              <path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 00-3.48-8.413Z"/>
            </svg>
          </motion.button>
        </motion.div>
      </div>

      {/* Scroll Indicator */}
      <motion.div
        initial={{ opacity: 0 }}
        animate={{ opacity: 1 }}
        transition={{ duration: 1, delay: 1 }}
        className="absolute bottom-8 left-1/2 -translate-x-1/2"
      >
        <motion.div
          animate={{ y: [0, 10, 0] }}
          transition={{ duration: 2, repeat: Infinity }}
          className="text-white"
        >
          <svg className="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path strokeLinecap="round" strokeLinejoin="round" strokeWidth={2} d="M19 14l-7 7m0 0l-7-7m7 7V3" />
          </svg>
        </motion.div>
      </motion.div>
    </section>
  );
}
```

### 4.2 Uso del Hero

```css
---
// src/pages/index.astro
import PageLayout from '@/layouts/PageLayout.astro';
import { Hero } from '@/components/sections/Hero';
---

<PageLayout title="Inicio">
  <Hero
    client:load
    title="Mixología Exclusiva para Momentos Únicos"
    subtitle="Transformamos tu celebración en una experiencia memorable con cócteles de autor y servicio excepcional"
    backgroundImage="/images/hero-cocktail.jpg"
  />
  
  <!-- Resto del contenido -->
</PageLayout>
```

---

## 5. TESTIMONIALS SLIDER

### 5.1 TestimonialsSlider.tsx

```css
// src/components/sections/TestimonialsSlider.tsx
import { useState, useEffect } from 'react';
import { motion, AnimatePresence } from 'framer-motion';

interface Testimonial {
  id: string;
  client_name: string;
  event_type: string;
  rating: number;
  comment: string;
  image_url?: string;
}

interface TestimonialsSliderProps {
  testimonials: Testimonial[];
}

export function TestimonialsSlider({ testimonials }: TestimonialsSliderProps) {
  const [currentIndex, setCurrentIndex] = useState(0);
  const [direction, setDirection] = useState(0);

  useEffect(() => {
    const timer = setInterval(() => {
      handleNext();
    }, 5000);

    return () => clearInterval(timer);
  }, [currentIndex]);

  const handleNext = () => {
    setDirection(1);
    setCurrentIndex((prev) => (prev + 1) % testimonials.length);
  };

  const handlePrev = () => {
    setDirection(-1);
    setCurrentIndex((prev) => (prev - 1 + testimonials.length) % testimonials.length);
  };

  const current = testimonials[currentIndex];

  const variants = {
    enter: (direction: number) => ({
      x: direction > 0 ? 1000 : -1000,
      opacity: 0,
    }),
    center: {
      x: 0,
      opacity: 1,
    },
    exit: (direction: number) => ({
      x: direction < 0 ? 1000 : -1000,
      opacity: 0,
    }),
  };

  return (
    <div className="relative max-w-4xl mx-auto">
      <AnimatePresence initial={false} custom={direction}>
        <motion.div
          key={currentIndex}
          custom={direction}
          variants={variants}
          initial="enter"
          animate="center"
          exit="exit"
          transition={{
            x: { type: 'spring', stiffness: 300, damping: 30 },
            opacity: { duration: 0.2 },
          }}
          className="bg-white p-8 md:p-12 rounded-lg shadow-xl"
        >
          {/* Stars */}
          <div className="flex justify-center mb-6">
            {Array.from({ length: 5 }).map((_, i) => (
              <svg
                key={i}
                className={`w-6 h-6 ${
                  i < current.rating ? 'text-primary-500' : 'text-secondary-200'
                }`}
                fill="currentColor"
                viewBox="0 0 20 20"
              >
                <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z" />
              </svg>
            ))}
          </div>

          {/* Quote */}
          <blockquote className="text-xl md:text-2xl text-center text-secondary-600 mb-8 font-display italic">
            "{current.comment}"
          </blockquote>

          {/* Author */}
          <div className="flex flex-col items-center">
            {current.image_url && (
              <img
                src={current.image_url}
                alt={current.client_name}
                className="w-16 h-16 rounded-full mb-4 object-cover"
              />
            )}
            <p className="font-semibold text-lg text-secondary-600">
              {current.client_name}
            </p>
            <p className="text-secondary-400 text-sm">
              {current.event_type}
            </p>
          </div>
        </motion.div>
      </AnimatePresence>

      {/* Navigation Buttons */}
      <button
        onClick={handlePrev}
        className="absolute left-0 top-1/2 -translate-y-1/2 -translate-x-12 p-3 bg-white rounded-full shadow-lg hover:bg-secondary-50 transition-colors"
        aria-label="Testimonio anterior"
      >
        <svg className="w-6 h-6 text-secondary-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
          <path strokeLinecap="round" strokeLinejoin="round" strokeWidth={2} d="M15 19l-7-7 7-7" />
        </svg>
      </button>

      <button
        onClick={handleNext}
        className="absolute right-0 top-1/2 -translate-y-1/2 translate-x-12 p-3 bg-white rounded-full shadow-lg hover:bg-secondary-50 transition-colors"
        aria-label="Siguiente testimonio"
      >
        <svg className="w-6 h-6 text-secondary-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
          <path strokeLinecap="round" strokeLinejoin="round" strokeWidth={2} d="M9 5l7 7-7 7" />
        </svg>
      </button>

      {/* Dots Indicator */}
      <div className="flex justify-center gap-2 mt-8">
        {testimonials.map((_, index) => (
          <button
            key={index}
            onClick={() => {
              setDirection(index > currentIndex ? 1 : -1);
              setCurrentIndex(index);
            }}
            className={`w-3 h-3 rounded-full transition-all ${
              index === currentIndex
                ? 'bg-primary-500 w-8'
                : 'bg-secondary-300 hover:bg-secondary-400'
            }`}
            aria-label={`Ir a testimonio ${index + 1}`}
          />
        ))}
      </div>
    </div>
  );
}
```

### 5.2 Uso del Testimonials Slider

```css
---
// src/pages/index.astro (continuación)
import { TestimonialsSlider } from '@/components/sections/TestimonialsSlider';
import { supabase } from '@/lib/supabase';

const { data: testimonials } = await supabase
  .from('testimonials')
  .select('*')
  .eq('approved', true)
  .eq('featured', true)
  .limit(5);
---

<section class="section bg-secondary-50">
  <div class="container-custom">
    <div class="text-center mb-12">
      <h2 class="mb-4">Lo que dicen nuestros clientes</h2>
      <p class="text-lg text-secondary-400">
        Experiencias reales de eventos memorables
      </p>
    </div>

    {testimonials && testimonials.length > 0 && (
      <TestimonialsSlider client:load testimonials={testimonials} />
    )}
  </div>
</section>
```

---

## 6. CONTACTFORM COMPONENT (Simple)

### 6.1 ContactForm.tsx

```css
// src/components/forms/ContactForm.tsx
import { useState } from 'react';
import { useForm } from 'react-hook-form';
import { zodResolver } from '@hookform/resolvers/zod';
import { contactSchema, type ContactFormData } from '@/utils/validators';
import { useToast } from '@/components/ui/Toast';
import { cn } from '@/utils/utils';

export function ContactForm() {
  const [isSubmitting, setIsSubmitting] = useState(false);
  const { showToast } = useToast();

  const {
    register,
    handleSubmit,
    reset,
    formState: { errors },
  } = useForm<ContactFormData>({
    resolver: zodResolver(contactSchema),
  });

  const onSubmit = async (data: ContactFormData) => {
    try {
      setIsSubmitting(true);

      // Enviar a API endpoint o directamente
      const response = await fetch('/api/contact', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(data),
      });

      if (!response.ok) throw new Error('Error al enviar');

      showToast('¡Mensaje enviado! Te responderemos pronto.', 'success');
      reset();
    } catch (error) {
      console.error('Error:', error);
      showToast('Error al enviar mensaje. Intenta de nuevo.', 'error');
    } finally {
      setIsSubmitting(false);
    }
  };

  return (
    <form onSubmit={handleSubmit(onSubmit)} className="space-y-6">
      <div>
        <label htmlFor="name" className="label">
          Nombre <span className="text-red-500">*</span>
        </label>
        <input
          {...register('name')}
          id="name"
          type="text"
          className={cn('input', errors.name && 'border-red-500')}
          placeholder="Tu nombre"
        />
        {errors.name && (
          <p className="text-sm text-red-500 mt-1">{errors.name.message}</p>
        )}
      </div>

      <div>
        <label htmlFor="email" className="label">
          Email <span className="text-red-500">*</span>
        </label>
        <input
          {...register('email')}
          id="email"
          type="email"
          className={cn('input', errors.email && 'border-red-500')}
          placeholder="tu@email.com"
        />
        {errors.email && (
          <p className="text-sm text-red-500 mt-1">{errors.email.message}</p>
        )}
      </div>

      <div>
        <label htmlFor="phone" className="label">
          Teléfono (opcional)
        </label>
        <input
          {...register('phone')}
          id="phone"
          type="tel"
          className="input"
          placeholder="999 888 777"
        />
      </div>

      <div>
        <label htmlFor="subject" className="label">
          Asunto <span className="text-red-500">*</span>
        </label>
        <input
          {...register('subject')}
          id="subject"
          type="text"
          className={cn('input', errors.subject && 'border-red-500')}
          placeholder="¿En qué podemos ayudarte?"
        />
        {errors.subject && (
          <p className="text-sm text-red-500 mt-1">{errors.subject.message}</p>
        )}
      </div>

      <div>
        <label htmlFor="message" className="label">
          Mensaje <span className="text-red-500">*</span>
        </label>
        <textarea
          {...register('message')}
          id="message"
          rows={6}
          className={cn('input resize-none', errors.message && 'border-red-500')}
          placeholder="Escribe tu mensaje aquí..."
        />
        {errors.message && (
          <p className="text-sm text-red-500 mt-1">{errors.message.message}</p>
        )}
      </div>

      <button
        type="submit"
        disabled={isSubmitting}
        className="btn-primary w-full"
      >
        {isSubmitting ? 'Enviando...' : 'Enviar Mensaje'}
      </button>
    </form>
  );
}
```

---

## ✅ CHECKLIST - Componentes React

Verifica que hayas creado:

### Componentes interactivos:
- [ ] Modal.tsx con animaciones
- [ ] Toast.tsx con ToastProvider y useToast hook
- [ ] QuoteForm.tsx con validación completa
- [ ] Hero.tsx con animaciones y WhatsApp button
- [ ] TestimonialsSlider.tsx con navegación
- [ ] ContactForm.tsx

### Integración:
- [ ] ToastProvider agregado a BaseLayout
- [ ] Componentes funcionan con `client:load`
- [ ] Formularios envían datos a Supabase
- [ ] Toast muestra mensajes correctamente

### Testing:
- [ ] Modal abre y cierra correctamente
- [ ] Toast aparece y desaparece automáticamente
- [ ] QuoteForm valida campos
- [ ] Hero anima al cargar
- [ ] Testimonials slider navega correctamente

---

## 📝 NOTAS IMPORTANTES

### Directiva client: en Astro

Todos los componentes React deben usar directivas client:

```astro
<!-- client:load - Carga inmediatamente (para componentes críticos) -->
<QuoteForm client:load />

<!-- client:idle - Carga cuando el navegador está idle (recomendado) -->
<TestimonialsSlider client:idle testimonials={data} />

<!-- client:visible - Carga cuando es visible (lazy loading) -->
<ContactForm client:visible />

<!-- client:only - Solo en cliente (no SSR) -->
<ComplexComponent client:only="react" />
```

### Props en componentes Astro → React

```astro
---
// Obtener datos en Astro (servidor)
const testimonials = await getTestimonials();
---

<!-- Pasar a React -->
<TestimonialsSlider 
  client:load 
  testimonials={testimonials} 
/>
```

---

## 🔜 CONTINÚA CON

**→ Archivo 05: Páginas Principales del Sitio**
- Página Home completa
- Página Servicios
- Página Portafolio
- Página Nosotros
- Página Contacto

---

**© 2025 La Reserva. Documentación técnica del proyecto.**