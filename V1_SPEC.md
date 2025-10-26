# Vista Fire District Website - V1 Simplified Specification

## Overview

A simple, static website for Vista Fire District. Easy to maintain, fast to load, no database or complex CMS.

## Technology Stack

- **Plain HTML/CSS/JavaScript** - Simple and straightforward
- **Tailwind CSS** - For quick, professional styling
- **GitHub Pages or Netlify** - Free hosting
- **No build process** - Or minimal (just for Tailwind)

## Site Structure (Simplified)

```
Vista Fire District
├── Home
├── About
│   ├── Commissioners
│   └── Contact
├── Safety Tips
├── Meetings
│   ├── Schedule
│   └── Minutes Archive
└── Transparency
    ├── Budgets
    └── Documents
```

## Pages

### Home Page (index.html)
- Hero section with logo and welcome
- Emergency contact (911) prominently displayed
- Quick info boxes:
  - Next meeting date/time
  - Contact information
  - Safety resources link
- Brief description of district
- Link to other pages

### About Section

**about.html** - Single page with:
- Mission statement
- Services provided
- Coverage area description
- Link to commissioners and contact

**commissioners.html**:
- List of current commissioners
- Name, position, term dates
- Photos (optional for v1)
- Contact email if applicable

**contact.html**:
- Office address and hours
- Phone numbers
- Email addresses
- Simple contact form (or just email links)
- Google Maps embed

### Safety Tips (safety.html)
- Single page with sections:
  - Fire safety tips (collapsible sections)
  - Wildfire preparedness
  - Emergency procedures
- Link to downloadable PDF guides (if available)

### Meetings Section

**meetings.html**:
- Upcoming meeting schedule
- Simple table or list format
- How to attend information

**minutes.html**:
- List of meeting minutes by year
- Links to PDF files
- Organized by date (newest first)

### Transparency Section

**transparency.html** - Single page with:
- Links to current and historical budgets (PDFs)
- Links to other governance documents
- Election information (when applicable)

## File Structure

```
vistafd/
├── index.html              # Home page
├── about.html              # About page
├── commissioners.html      # Board info
├── contact.html           # Contact page
├── safety.html            # Safety tips
├── meetings.html          # Meeting schedule
├── minutes.html           # Minutes archive
├── transparency.html      # Budgets & documents
├── css/
│   └── styles.css         # Custom styles
├── js/
│   └── main.js            # Simple interactions
├── images/
│   ├── logo.svg
│   └── commissioners/
├── documents/
│   ├── minutes/
│   │   ├── 2025/
│   │   └── 2024/
│   └── budgets/
└── README.md
```

## Design

- Clean, professional government website aesthetic
- Blue/red color scheme (typical for fire districts)
- Mobile responsive
- Simple navigation bar
- Footer with quick links and contact

## Features

### Must Have (V1)
- ✅ Responsive design
- ✅ Clear navigation
- ✅ Contact information
- ✅ Meeting schedule
- ✅ Links to documents (PDFs)
- ✅ Basic accessibility (semantic HTML, alt text)

### Nice to Have (V1)
- Simple mobile menu (hamburger)
- Smooth scrolling
- Basic print styles
- Contact form

### Future (V2)
- Search functionality
- Interactive calendar
- CMS for easy updates
- News/announcements system
- Document management

## Content Needed (Minimal)

1. **Text Content:**
   - Mission statement (1 paragraph)
   - Services description (1 paragraph)
   - Contact information
   - Commissioner names and positions
   - Meeting schedule

2. **Files:**
   - Logo (SVG or PNG)
   - District map (image or PDF)
   - Recent meeting minutes (PDFs)
   - Current budget (PDF)

3. **Optional:**
   - Commissioner photos
   - Safety tip documents

## Development Steps

1. Create basic HTML structure for all pages
2. Add Tailwind CSS (via CDN for simplicity)
3. Create navigation and footer components
4. Style each page
5. Add content
6. Test on mobile devices
7. Deploy to GitHub Pages or Netlify

## Maintenance

To update content:
1. Edit HTML files directly
2. Upload new PDFs to documents folder
3. Update links in HTML
4. Commit and push to GitHub
5. Site automatically updates

Simple and straightforward!

## Estimated Timeline

- **Day 1**: Set up structure, create templates
- **Day 2**: Build and style all pages
- **Day 3**: Add content, test, deploy

Total: 2-3 days of work

## Cost

**$0-12/year**
- GitHub Pages: Free
- Or custom domain: ~$12/year
- Everything else: Free

---

This is a **realistic v1** that can be built quickly and maintained easily!
