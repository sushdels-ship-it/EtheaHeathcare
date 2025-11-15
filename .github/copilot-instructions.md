# Copilot Instructions for EtheaHeathcare

## Project Overview
EtheaHeathcare is a static website for **REVALON Biocare**, a pharmaceutical company established in 2025. The site showcases the company, founders, and 5 pharmaceutical products using the HTML5 UP "Hyperspace" template with custom modifications.

**Key Pages:**
- `index.html` - Main landing page with slideshow, company info, founder spotlights, product listings, and contact form
- `generic.html` - Template page for additional content
- `elements.html` - UI elements reference page
- `Etheahealthcare.html` - Alternative layout demo (not currently integrated)

## Architecture & Tech Stack

### Frontend Structure
- **HTML5 Framework:** HTML5 UP Hyperspace template (customized for company branding)
- **Styling:** SASS/SCSS compiled to CSS, organized modularly in `assets/sass/`
- **JavaScript:** jQuery-based, minimal custom logic in `assets/js/main.js`
- **Responsive Design:** Mobile-first breakpoints defined in `assets/sass/libs/_breakpoints.scss` (xxsmall to xlarge)
- **Icons:** FontAwesome 5 (loaded via CDN in `assets/css/fontawesome-all.min.css`)

### SASS Organization Pattern
```
assets/sass/
├── libs/              # Shared utilities (vars, mixins, breakpoints, grid)
├── base/              # Reset, page defaults, typography
├── components/        # Individual UI elements (button, form, contact, etc.)
└── layout/            # Page sections (header, footer, sidebar, wrapper)
```
Key pattern: Each component/layout has its own `_*.scss` file, imported in `main.scss`.

### Email Integration
- **Service:** SMTP.js library (smtpjs.com) for client-side email via Gmail
- **Configuration:** Contact form in index.html sends to `revelonbiocare@gmail.com`
- **Gmail Setup:** Uses Gmail App Password (stored as plain text in HTML - **security concern for production**)
- **Credentials file:** `README.txt` contains EmailJS dashboard reference and Gmail credentials

## Key Customizations

### 1. Image Slideshow
Inline JavaScript in `index.html` (lines ~195-205) rotates 3 founder images every 3 seconds using vanilla JS, not jQuery.

### 2. Contact Form
- Email submission via SMTP.js library (inline script ~lines 210-235)
- Form fields: Name, Email, Message
- Button disables/shows "Sending..." state during submission
- Success/failure alerts for user feedback

### 3. Company Information Section
Six-icon grid showing: GST Number, Business Type, Year of Establishment, Employee count, Product count, and placeholder for future products.

### 4. Product Grid
Five pharmaceutical products listed with icons and descriptions:
- Esogred DSR (GERD treatment)
- Fluqik (Flu treatment)
- Vitri D3 (Vitamin D supplement)
- Argivion (Cardiovascular health)
- Luprest (Gynecological/fertility support)

## Development Conventions

### CSS/SCSS Updates
1. **Component styling:** Add new component files to `assets/sass/components/` and import in `main.scss`
2. **Responsive rules:** Use mixin `@include breakpoints((size: rule))` for media queries (defined in `_breakpoints.scss`)
3. **Color variables:** Update in `assets/sass/libs/_vars.scss` (referenced as CSS variables via `:root` in compiled CSS)

### HTML Updates
- Use semantic HTML5 elements (`<section>`, `<nav>`, `<header>`, `<footer>`)
- Maintain id-based navigation linking (e.g., `href="#intro"`, `href="#one"`)
- FontAwesome classes: `fa-code`, `fa-lock`, `fa-cog`, `fa-desktop` (examples in products/info sections)

### JavaScript Patterns
- jQuery is loaded first, utility scripts (`util.js`, `breakpoints.min.js`) run before `main.js`
- jQuery form submit prevention: Use `.submit()` event with `event.preventDefault()`
- Window load event: `$window.on('load', fn)` for post-render initialization

## Important Build & Deployment Notes

### No Build Process
This is a static HTML/CSS/JS site with **no build step**. SASS files are not compiled during deployment—CSS is pre-compiled and checked into version control at `assets/css/main.css`. If modifying SASS:
- Compile locally with a SASS compiler (e.g., `sass assets/sass/main.scss assets/css/main.css`)
- Commit compiled `main.css` to Git

### External Dependencies
- jQuery 3.x (minified from `assets/js/jquery.min.js`)
- FontAwesome 5 (CSS-only, no JS)
- SMTP.js library from CDN (`https://smtpjs.com/v3/smtp.js`)
- Google Fonts/system fonts via CSS

### Credentials & Security
**⚠️ Critical:** Gmail credentials are hard-coded in `index.html` (lines ~218-219). For production:
1. Move email service to backend API endpoint
2. Use environment variables or secure credential storage
3. Replace SMTP.js client-side approach with server-side email service (SendGrid, AWS SES, etc.)

## Common Tasks

### Add a New Product
1. Add `<section>` element to the features grid in `index.html` (copy structure from existing products)
2. Update icon class (FontAwesome icon), product name, and description
3. No CSS changes needed (grid layout is responsive by default)

### Modify Company Info
Edit the `<section>` elements in the "Company Information" div (index.html ~lines 80-85). Update text and icon classes as needed.

### Update Navigation Links
- Sidebar links: Update `<ul>` in `#sidebar` section (index.html ~lines 49-54)
- Ensure `href` values match section `id` attributes for smooth scrolling

### Change Color Scheme
1. Update SASS variables in `assets/sass/libs/_vars.scss`
2. Recompile SASS to `assets/css/main.css`
3. Test responsive breakpoints (xxsmall through xlarge)

## File Reference Guide
| File | Purpose |
|------|---------|
| `index.html` | Main landing page (primary focus) |
| `assets/js/main.js` | jQuery initialization, sidebar/menu logic |
| `assets/sass/main.scss` | SASS entry point (imports all modules) |
| `assets/css/main.css` | Compiled CSS (pre-generated, do not edit directly) |
| `README.txt` | Credentials reference (move to `.env` or remove) |

## Version Control Notes
- Template source: HTML5 UP Hyperspace (free license - CCA 3.0)
- No node_modules or package.json (static site only)
- `.gitignore` should exclude any environment-specific files or credential files
