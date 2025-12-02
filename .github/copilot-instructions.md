# Copilot Instructions for 3D Portfolio

## Project Overview
A React-based 3D portfolio website using Three.js for 3D graphics, Framer Motion & GSAP for animations, and Tailwind CSS for styling. Built with Vite.

## Architecture

### Key Directories
- `src/components/` - Page sections (Hero, About, Works, etc.) and reusable components
- `src/components/canvas/` - Three.js 3D components (Computers, Earth, Stars)
- `src/constants/index.js` - **All content data** (experiences, projects, testimonials, technologies)
- `src/assets/` - Images and icons with centralized exports in `index.js`
- `src/hoc/SectionWrapper.jsx` - Higher-order component wrapping all sections
- `src/utils/motion.js` - Framer Motion animation variants
- `public/` - 3D model files (GLTF) for Three.js

### Component Pattern
All major sections follow this pattern:
```jsx
import { SectionWrapper } from "../hoc";
import { styles } from "../styles";
import { fadeIn, textVariant } from "../utils/motion";

const MySection = () => { /* component logic */ };
export default SectionWrapper(MySection, "section-id");
```

## Critical Conventions

### Styling System
- Use classes from `src/styles.js` for typography: `styles.sectionHeadText`, `styles.heroSubText`, etc.
- Custom Tailwind colors defined in `tailwind.config.cjs`: `primary`, `secondary`, `tertiary`, `black-100`, `black-200`
- Responsive breakpoints: `xs:450px` (custom), `sm`, `md`, `lg`, `xl`

### Animation Patterns
- **Framer Motion**: Use `motion.div` with variants from `src/utils/motion.js` (`textVariant`, `fadeIn`, `slideIn`, `zoomIn`)
- **GSAP ScrollTrigger**: Used in `Works.jsx` for scroll-based animations
- All sections use `staggerContainer` via `SectionWrapper` HOC

### Adding Content
To add projects, experiences, or testimonials, edit `src/constants/index.js`:
- `projects` array for portfolio items
- `experiences` array for work timeline
- `testimonials` array for feedback section
- `technologies` array for tech stack icons

### Asset Management
1. Add image to `src/assets/` (or subfolder like `tech/`, `company/`)
2. Import and export in `src/assets/index.js`
3. Import from `../assets` where needed

### 3D Components
- 3D models loaded from `public/` using `useGLTF` hook
- Canvas components handle mobile responsiveness internally (hide on small screens)
- Use `<Suspense fallback={<CanvasLoader />}>` for loading states

## Environment Variables
Contact form requires EmailJS configuration in `.env`:
```
VITE_APP_EMAILJS_SERVICE_ID=
VITE_APP_EMAILJS_TEMPLATE_ID=
VITE_APP_EMAILJS_PUBLIC_KEY=
```

## Commands
- `npm run dev` - Start development server
- `npm run build` - Production build
- `npm run preview` - Preview production build
