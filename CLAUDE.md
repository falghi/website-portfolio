# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a static personal portfolio website built with vanilla HTML, CSS, and JavaScript. The site showcases professional experience, education, projects, portfolio items, services, and contact information. It uses a single-page application (SPA) architecture with smooth scrolling navigation between sections.

## Development Workflow

### Local Development
1. Clone the repository
2. Open `index.html` directly in a browser (no build step required)

### Deployment
The site uses automated deployment via GitHub Actions:
- Pushes to `master` branch trigger automatic deployment
- GitHub Actions workflow (`.github/workflows/main.yml`) uses SSH to deploy to production server at `/home/falghifa/public_html/`
- Deployment simply runs `git pull` on the remote server

### Manual Testing
To test changes locally, simply open `index.html` in a web browser. No local server is required, though one can be used for more realistic testing.

## Architecture

### File Structure
- `index.html` - Single-page application containing all sections (intro, about, resume, portfolio, services, contact)
- `css/` - Stylesheets
  - `base.css` - Base styles and resets
  - `main.css` - Primary styling for all sections (largest file at ~51KB)
  - `vendor.css` - Third-party library styles
  - `fonts.css` - Font definitions
  - `font-awesome/` - Icon font library
  - `micons/` - Custom icon font
- `js/` - JavaScript files
  - `main.js` - Core functionality (smooth scrolling, modal popups, navigation, contact form, animations)
  - `jquery-2.1.3.min.js` - jQuery library
  - `plugins.js` - Third-party plugins (Magnific Popup, Owl Carousel, Masonry, Waypoints, FitText, FitVids, jQuery Validate)
  - `modernizr.js` - Feature detection
  - `pace.min.js` - Page load progress bar
- `images/` - Image assets
  - `portfolio/` - Portfolio item thumbnails and modal images
  - Profile pictures and background images
- `fonts/` - Font files
- `.htaccess` - Apache server configuration

### Key Sections in index.html
The HTML is structured as semantic sections with smooth scrolling navigation:
1. **Header** (`<header>`) - Navigation menu with smooth scroll links
2. **Intro** (`#intro`) - Hero section with name, title, and social links
3. **About** (`#about`) - Profile information and skills
4. **Resume** (`#resume`) - Work experience, education, and projects timelines
5. **Portfolio** (`#portfolio`) - Portfolio items in masonry grid layout with modal popups
6. **Services** (`#services`) - Services offered (IT consultation, web development, API design, algorithm design)
7. **Contact** (`#contact`) - Contact form and contact information
8. **Footer** (`<footer>`) - Social links and copyright

### JavaScript Functionality (js/main.js)
- **Preloader**: Fades out loading animation on page load
- **FitText**: Responsive typography for the intro heading
- **Owl Carousel**: Services section carousel with responsive breakpoints
- **Masonry**: Portfolio grid layout using `imagesLoaded` for proper initialization
- **Magnific Popup**: Modal overlays for portfolio items
- **Navigation**:
  - Mobile menu toggle
  - Smooth scrolling to sections
  - Auto-highlighting current section in nav using Waypoints
- **Contact Form**: AJAX submission to Heroku endpoint (`https://dry-cove-17776.herokuapp.com/mail`) with validation
- **Stat Counter**: Animated counting (via Waypoints, though stats section appears commented out in HTML)
- **Back to Top**: Scroll-to-top button that appears after scrolling 300px

### External Dependencies
All third-party libraries are included locally (no CDN usage):
- jQuery 2.1.3
- jQuery Validate
- Owl Carousel
- Magnific Popup
- Masonry
- imagesLoaded
- Waypoints
- FitText
- FitVids
- Modernizr
- Pace.js
- Font Awesome

## Content Updates

### Adding Work Experience
Edit the work experience timeline in `index.html` around lines 227-333. Each experience follows this structure:
```html
<div class="timeline-block">
  <div class="timeline-ico"><i class="fa fa-briefcase"></i></div>
  <div class="timeline-header">
    <h3>Job Title</h3>
    <p>Date Range</p>
  </div>
  <div class="timeline-content">
    <h4>Company Name</h4>
    <ul><li>Responsibility/Achievement</li></ul>
  </div>
</div>
```

### Adding Portfolio Items
Portfolio items require two additions in `index.html`:
1. **Grid item** (lines 488-630): Thumbnail with overlay showing title and tools used
2. **Modal popup** (lines 635-810): Detailed view with full image, description, and link

Portfolio images go in:
- `images/portfolio/` - Grid thumbnails
- `images/portfolio/modals/` - Full-size modal images

### Updating Skills
Skills are in the about section (lines 164-189). Each skill uses a progress bar:
```html
<li>
  <div class="progress percent100"></div>
  <strong>Skill Name</strong>
</li>
```

### Contact Form Endpoint
Contact form submits to external Heroku endpoint: `https://dry-cove-17776.herokuapp.com/mail`
If this endpoint changes, update the URL in `js/main.js` line 230.

## Important Notes

- This is a purely static site with no build process
- All content is in `index.html` - update it directly to change content
- Portfolio modal IDs must match between grid items (`href="#modal-XX"`) and modal definitions (`id="modal-XX"`)
- The site uses smooth scrolling with anchor links to section IDs
- Mobile responsiveness is handled entirely through CSS (check `css/main.css`)
- Images should be optimized before adding to keep page load times reasonable
