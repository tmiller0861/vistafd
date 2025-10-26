# Vista Fire District Website - Implementation Checklist

This checklist provides a step-by-step guide for implementing the Vista Fire District website.

## Phase 1: Project Setup (Week 1)

### 1.1 Repository & Environment
- [ ] Review all specification documents
- [ ] Set up project management tools (GitHub Projects, Trello, etc.)
- [ ] Create development branch strategy
- [ ] Set up issue tracking

### 1.2 Domain & Hosting
- [ ] Register domain name
  - [ ] Option A: Apply for .gov domain (requires government verification)
  - [ ] Option B: Register .org or other TLD
- [ ] Set up DNS management
- [ ] Create Vercel account
- [ ] Link domain to Vercel

### 1.3 Development Environment
- [ ] Install Node.js (v18+ recommended)
- [ ] Install Git
- [ ] Install code editor (VS Code recommended)
- [ ] Install browser dev tools extensions
  - [ ] React DevTools
  - [ ] Lighthouse
  - [ ] axe DevTools (accessibility)

### 1.4 Initialize Next.js Project
```bash
# Run this command
npx create-next-app@latest vistafd-website --typescript --tailwind --app --src-dir --import-alias "@/*"

# Answer prompts:
# ✔ Would you like to use TypeScript? Yes
# ✔ Would you like to use ESLint? Yes
# ✔ Would you like to use Tailwind CSS? Yes
# ✔ Would you like to use `src/` directory? Yes
# ✔ Would you like to use App Router? Yes
# ✔ Would you like to customize the default import alias? Yes (@/*)
```

- [ ] Initialize Git repository
- [ ] Create initial commit
- [ ] Push to GitHub

### 1.5 Install Dependencies
```bash
# Core dependencies
npm install next-sanity @sanity/image-url @sanity/vision @portabletext/react

# UI Components
npm install @headlessui/react @heroicons/react clsx tailwind-merge

# Calendar
npm install react-big-calendar date-fns

# Forms
npm install @formspree/react

# Utils
npm install @vercel/analytics

# Dev dependencies
npm install -D @types/react-big-calendar
```

- [ ] Run `npm install` to install all dependencies
- [ ] Verify project runs: `npm run dev`
- [ ] Access http://localhost:3000 to confirm

### 1.6 Set Up Sanity CMS
```bash
# Create Sanity project
npm create sanity@latest

# Follow prompts:
# - Login with Google/GitHub
# - Create new project
# - Project name: Vista Fire District CMS
# - Dataset: production
# - Output path: ./studio
# - Template: Clean project
```

- [ ] Create Sanity project
- [ ] Configure Sanity Studio
- [ ] Deploy Studio: `cd studio && npm run deploy`
- [ ] Save Studio URL for later

### 1.7 Environment Variables
Create `.env.local` file:
```env
# Sanity
NEXT_PUBLIC_SANITY_PROJECT_ID=your_project_id
NEXT_PUBLIC_SANITY_DATASET=production
SANITY_API_TOKEN=your_token

# Site
NEXT_PUBLIC_SITE_URL=http://localhost:3000

# Forms (add later)
NEXT_PUBLIC_FORMSPREE_ID=your_form_id
```

- [ ] Create `.env.local` file
- [ ] Add environment variables
- [ ] Add `.env.local` to `.gitignore`
- [ ] Create `.env.example` for documentation

---

## Phase 2: Design & Branding (Week 1-2)

### 2.1 Brand Assets
- [ ] Obtain high-resolution logo (SVG preferred)
- [ ] Define color palette
  - [ ] Primary color (blues/reds typical for fire districts)
  - [ ] Accent colors
  - [ ] Neutral colors
  - [ ] Emergency/alert colors
- [ ] Choose typography
  - [ ] Heading font
  - [ ] Body font
  - [ ] Ensure both are web-safe or have license

### 2.2 Tailwind Configuration
Edit `tailwind.config.js`:
```javascript
module.exports = {
  theme: {
    extend: {
      colors: {
        primary: {
          50: '#...',
          // ... color scale
          900: '#...',
        },
        accent: {...},
      },
      fontFamily: {
        sans: ['Your Font', 'system-ui', ...],
      },
    },
  },
}
```

- [ ] Configure custom colors
- [ ] Configure custom fonts
- [ ] Test color contrast ratios (WCAG AA minimum)

### 2.3 Wireframes & Mockups
- [ ] Create low-fidelity wireframes for key pages
  - [ ] Home page
  - [ ] About page
  - [ ] Safety page
  - [ ] Transparency page
- [ ] Get stakeholder approval on layout
- [ ] Create high-fidelity mockups (optional but recommended)

### 2.4 Component Library Setup
- [ ] Create base component structure
- [ ] Set up component documentation (Storybook optional)
- [ ] Create design system documentation

---

## Phase 3: Core Development (Week 3-5)

### 3.1 Layout Components

#### 3.1.1 Header
File: `src/components/layout/Header.tsx`
- [ ] Create Header component
- [ ] Add logo
- [ ] Add navigation menu
- [ ] Add emergency contact display
- [ ] Implement mobile hamburger menu
- [ ] Test keyboard navigation
- [ ] Test screen reader compatibility

#### 3.1.2 Footer
File: `src/components/layout/Footer.tsx`
- [ ] Create Footer component
- [ ] Add quick links
- [ ] Add contact information
- [ ] Add legal links
- [ ] Add copyright notice
- [ ] Test responsive layout

#### 3.1.3 Navigation
File: `src/components/layout/Navigation.tsx`
- [ ] Create Navigation component
- [ ] Implement desktop menu
- [ ] Implement mobile menu
- [ ] Add active state styling
- [ ] Add hover states
- [ ] Ensure accessibility (ARIA labels)

#### 3.1.4 Root Layout
File: `src/app/layout.tsx`
- [ ] Configure metadata
- [ ] Add Header and Footer
- [ ] Add global styles
- [ ] Configure fonts
- [ ] Add analytics
- [ ] Test on multiple devices

### 3.2 Sanity Schemas

#### 3.2.1 Commissioner Schema
File: `studio/schemas/commissioner.ts`
```typescript
export default {
  name: 'commissioner',
  title: 'Board Commissioner',
  type: 'document',
  fields: [
    // See TECH_STACK.md for complete schema
  ]
}
```
- [ ] Create commissioner schema
- [ ] Add validation rules
- [ ] Test in Sanity Studio

#### 3.2.2 Meeting Minutes Schema
File: `studio/schemas/meetingMinutes.ts`
- [ ] Create meeting minutes schema
- [ ] Add file upload for PDFs
- [ ] Add date fields
- [ ] Add status field (draft/approved)

#### 3.2.3 Event Schema
File: `studio/schemas/event.ts`
- [ ] Create event schema
- [ ] Add date/time fields
- [ ] Add location field
- [ ] Add optional virtual meeting link

#### 3.2.4 Budget Schema
File: `studio/schemas/budget.ts`
- [ ] Create budget schema
- [ ] Add fiscal year field
- [ ] Add file upload for PDF
- [ ] Add status field

#### 3.2.5 Safety Content Schema
File: `studio/schemas/safetyContent.ts`
- [ ] Create safety content schema
- [ ] Add category field
- [ ] Add portable text for rich content
- [ ] Add related resources

#### 3.2.6 Announcement Schema
File: `studio/schemas/announcement.ts`
- [ ] Create announcement schema
- [ ] Add priority/urgency field
- [ ] Add date range for display
- [ ] Add rich text editor

### 3.3 Sanity Configuration
File: `src/lib/sanity/client.ts`
```typescript
import { createClient } from 'next-sanity'

export const client = createClient({
  projectId: process.env.NEXT_PUBLIC_SANITY_PROJECT_ID,
  dataset: process.env.NEXT_PUBLIC_SANITY_DATASET,
  apiVersion: '2024-01-01',
  useCdn: true,
})
```
- [ ] Create Sanity client
- [ ] Create query helper functions
- [ ] Test API connection

### 3.4 Reusable Components

#### UI Components
- [ ] Button component (`src/components/ui/Button.tsx`)
- [ ] Card component (`src/components/ui/Card.tsx`)
- [ ] Alert component (`src/components/ui/Alert.tsx`)
- [ ] Modal component (`src/components/ui/Modal.tsx`)
- [ ] Breadcrumb component (`src/components/ui/Breadcrumb.tsx`)

#### Feature Components
- [ ] Document list component
- [ ] Event card component
- [ ] Commissioner card component
- [ ] Quick links panel
- [ ] Calendar widget

### 3.5 Home Page
File: `src/app/page.tsx`

Components to create:
- [ ] `src/components/home/Hero.tsx` - Hero section
- [ ] `src/components/home/QuickLinks.tsx` - Quick access panel
- [ ] `src/components/home/UpcomingEvents.tsx` - Event widget
- [ ] `src/components/home/Announcements.tsx` - News section

Tasks:
- [ ] Create home page layout
- [ ] Implement hero section
- [ ] Add quick links panel
- [ ] Add upcoming events widget (fetch from Sanity)
- [ ] Add announcements section (fetch from Sanity)
- [ ] Add call-to-action sections
- [ ] Optimize images
- [ ] Test mobile responsiveness
- [ ] Test accessibility

---

## Phase 4: Content Pages (Week 6-7)

### 4.1 About Section

#### 4.1.1 About Main Page
File: `src/app/about/page.tsx`
- [ ] Create page layout
- [ ] Add mission statement
- [ ] Add services description
- [ ] Add coverage area info
- [ ] Add history section
- [ ] Fetch content from Sanity
- [ ] Test and optimize

#### 4.1.2 Commissioners Page
File: `src/app/about/commissioners/page.tsx`
- [ ] Create commissioners grid layout
- [ ] Create commissioner card component
- [ ] Fetch commissioners from Sanity
- [ ] Display photos, names, positions, terms
- [ ] Add contact information
- [ ] Sort by display order
- [ ] Test responsive layout

#### 4.1.3 Contact Page
File: `src/app/about/contact/page.tsx`
- [ ] Create contact information layout
- [ ] Add office hours
- [ ] Add phone directory
- [ ] Add email contacts
- [ ] Add mailing address
- [ ] Embed Google Maps
- [ ] Add contact form
- [ ] Test form submissions

#### 4.1.4 District Map Page
File: `src/app/about/district-map/page.tsx`
- [ ] Create map display
- [ ] Add district boundary map
- [ ] Add station markers (if applicable)
- [ ] Provide PDF download
- [ ] Add map legend
- [ ] Test on mobile

### 4.2 Safety & Preparedness Section

#### 4.2.1 Safety Hub Page
File: `src/app/safety/page.tsx`
- [ ] Create overview page
- [ ] Add category cards
- [ ] Link to subsections
- [ ] Add featured tips
- [ ] Fetch content from Sanity

#### 4.2.2 Fire Safety Tips
File: `src/app/safety/fire-safety/page.tsx`
- [ ] Create content layout
- [ ] Add safety tips sections
- [ ] Add illustrations/icons
- [ ] Make content scannable
- [ ] Add downloadable guides

#### 4.2.3 Wildfire Preparedness
File: `src/app/safety/wildfire/page.tsx`
- [ ] Create preparedness guide
- [ ] Add defensible space info
- [ ] Add evacuation checklist
- [ ] Add go-bag checklist
- [ ] Add local resources

#### 4.2.4 Emergency Procedures
File: `src/app/safety/emergency/page.tsx`
- [ ] Create emergency procedures guide
- [ ] Add step-by-step instructions
- [ ] Add emergency contacts
- [ ] Make content clear and urgent
- [ ] Test readability

#### 4.2.5 Resources
File: `src/app/safety/resources/page.tsx`
- [ ] List training opportunities
- [ ] Add educational program info
- [ ] Link to external resources
- [ ] Add downloadable materials

### 4.3 Meetings & Events Section

#### 4.3.1 Meetings Hub
File: `src/app/meetings/page.tsx`
- [ ] Create overview page
- [ ] Show next meeting prominently
- [ ] Link to subsections
- [ ] Add quick calendar preview

#### 4.3.2 Upcoming Meetings
File: `src/app/meetings/upcoming/page.tsx`
- [ ] List upcoming meetings
- [ ] Show next 3-6 months
- [ ] Fetch from Sanity events
- [ ] Display date, time, location
- [ ] Add agenda links (when available)
- [ ] Add virtual meeting links

#### 4.3.3 Calendar Page
File: `src/app/meetings/calendar/page.tsx`
- [ ] Integrate React Big Calendar
- [ ] Fetch events from Sanity
- [ ] Style calendar to match design
- [ ] Add event type filtering
- [ ] Add month/week/day views
- [ ] Make mobile-friendly
- [ ] Add export to iCal/Google Calendar

#### 4.3.4 Public Participation
File: `src/app/meetings/participate/page.tsx`
- [ ] Explain meeting procedures
- [ ] Explain public comment rules
- [ ] List participation options
- [ ] Add ADA accommodation info
- [ ] Add virtual participation guide

### 4.4 Transparency Section

#### 4.4.1 Transparency Hub
File: `src/app/transparency/page.tsx`
- [ ] Create overview page
- [ ] Add section cards
- [ ] Highlight commitment to transparency
- [ ] Link to subsections

#### 4.4.2 Meeting Minutes
File: `src/app/transparency/minutes/page.tsx`
- [ ] Create minutes listing page
- [ ] Fetch minutes from Sanity
- [ ] Group by year
- [ ] Show draft vs approved status
- [ ] Add PDF download links
- [ ] Add pagination or infinite scroll
- [ ] Add search/filter functionality

Dynamic route for archives:
File: `src/app/transparency/minutes/[year]/page.tsx`
- [ ] Create dynamic year route
- [ ] List minutes for specific year
- [ ] Add breadcrumb navigation

#### 4.4.3 Budgets & Finance
File: `src/app/transparency/budgets/page.tsx`
- [ ] Create budgets listing page
- [ ] Fetch budgets from Sanity
- [ ] Show current adopted budget prominently
- [ ] List historical budgets
- [ ] Add financial reports
- [ ] Provide PDF downloads
- [ ] Add budget summary (citizen-friendly)

#### 4.4.4 Elections & Governance
File: `src/app/transparency/governance/page.tsx`
- [ ] Create governance information page
- [ ] Add election calendar
- [ ] Add candidate filing info
- [ ] List bylaws and policies
- [ ] Add district formation documents
- [ ] Provide downloads

### 4.5 Resources Section

#### 4.5.1 Resources Hub
File: `src/app/resources/page.tsx`
- [ ] Create overview page
- [ ] Add resource categories
- [ ] Link to subsections

#### 4.5.2 Downloads
File: `src/app/resources/downloads/page.tsx`
- [ ] List downloadable resources
- [ ] Organize by category
- [ ] Add file size indicators
- [ ] Ensure PDFs are accessible

#### 4.5.3 Forms
File: `src/app/resources/forms/page.tsx`
- [ ] List available forms
- [ ] Provide PDF downloads
- [ ] Add fillable online forms (if applicable)
- [ ] Add submission instructions

#### 4.5.4 Related Agencies
File: `src/app/resources/agencies/page.tsx`
- [ ] List related agencies
- [ ] Provide descriptions
- [ ] Add external links
- [ ] Organize by category

---

## Phase 5: Polish & Testing (Week 8)

### 5.1 Accessibility Audit
- [ ] Run automated accessibility tests
  - [ ] Lighthouse
  - [ ] axe DevTools
  - [ ] WAVE
- [ ] Manual keyboard navigation testing
- [ ] Screen reader testing (NVDA/JAWS)
- [ ] Color contrast verification
- [ ] Form accessibility testing
- [ ] Fix all issues found
- [ ] Achieve WCAG 2.1 AA compliance

### 5.2 Performance Optimization
- [ ] Run Lighthouse performance audit
- [ ] Optimize images
  - [ ] Convert to WebP
  - [ ] Add responsive images
  - [ ] Lazy load images
- [ ] Minimize JavaScript bundle
- [ ] Enable compression
- [ ] Optimize fonts
- [ ] Test on slow 3G connection
- [ ] Achieve Lighthouse score >90

### 5.3 SEO Optimization
- [ ] Add metadata to all pages
- [ ] Create sitemap.xml
- [ ] Create robots.txt
- [ ] Add structured data (JSON-LD)
- [ ] Add Open Graph tags
- [ ] Test with Google Rich Results Test
- [ ] Submit sitemap to Google Search Console

### 5.4 Cross-Browser Testing
Test on:
- [ ] Chrome (latest)
- [ ] Firefox (latest)
- [ ] Safari (latest)
- [ ] Edge (latest)
- [ ] Mobile Safari (iOS)
- [ ] Chrome Mobile (Android)

### 5.5 Mobile Testing
- [ ] Test on various screen sizes
- [ ] Test touch interactions
- [ ] Test mobile navigation
- [ ] Verify click targets are large enough
- [ ] Test forms on mobile
- [ ] Test calendar on mobile

### 5.6 Content Review
- [ ] Proofread all text content
- [ ] Verify all links work
- [ ] Check phone numbers are correct
- [ ] Verify email addresses
- [ ] Check all PDFs open correctly
- [ ] Verify dates and times
- [ ] Check for typos and grammar

### 5.7 Security Review
- [ ] Ensure HTTPS is enforced
- [ ] Verify environment variables are secure
- [ ] Test form security
- [ ] Check for exposed API keys
- [ ] Review Content Security Policy
- [ ] Test for XSS vulnerabilities

---

## Phase 6: Launch Preparation (Week 9)

### 6.1 Content Migration
- [ ] Upload all commissioner information
- [ ] Upload meeting minutes (current year minimum)
- [ ] Upload budgets
- [ ] Upload district map
- [ ] Create initial events in calendar
- [ ] Add safety content
- [ ] Create announcements
- [ ] Upload forms and documents

### 6.2 Legal Pages
- [ ] Create Privacy Policy page
- [ ] Create Accessibility Statement
- [ ] Create Public Records Request page
- [ ] Add Copyright Notice
- [ ] Review with legal counsel (if applicable)

### 6.3 Vercel Deployment Setup
- [ ] Connect GitHub repository to Vercel
- [ ] Configure environment variables in Vercel
- [ ] Set up production domain
- [ ] Configure SSL certificate
- [ ] Test deployment
- [ ] Set up preview deployments

### 6.4 Documentation
- [ ] Create content editor guide
- [ ] Document how to:
  - [ ] Add meeting minutes
  - [ ] Update events
  - [ ] Add announcements
  - [ ] Update commissioner info
  - [ ] Upload documents
- [ ] Create troubleshooting guide
- [ ] Document maintenance procedures

### 6.5 Staff Training
- [ ] Schedule training session
- [ ] Walk through Sanity Studio
- [ ] Demonstrate adding/editing content
- [ ] Practice uploading documents
- [ ] Practice creating events
- [ ] Answer questions
- [ ] Provide written documentation

### 6.6 Backup Strategy
- [ ] Set up automated Sanity backups
- [ ] Document backup restoration process
- [ ] Test backup and restore
- [ ] Set up monitoring and alerts

### 6.7 Analytics Setup
- [ ] Set up Vercel Analytics
- [ ] Configure Google Analytics (optional)
- [ ] Set up goals and events
- [ ] Create dashboard for stakeholders
- [ ] Document how to access analytics

### 6.8 Final Review
- [ ] Stakeholder review of complete site
- [ ] Make final adjustments
- [ ] Get sign-off from all parties
- [ ] Prepare launch announcement
- [ ] Schedule launch date and time

---

## Phase 7: Launch (Week 10)

### 7.1 Pre-Launch
- [ ] Final content review
- [ ] Final testing in production environment
- [ ] Verify all links work
- [ ] Verify all forms work
- [ ] Confirm domain is configured correctly
- [ ] Confirm SSL certificate is active

### 7.2 Launch Day
- [ ] Deploy to production
- [ ] Monitor for errors
- [ ] Test critical user flows
- [ ] Verify analytics are tracking
- [ ] Send launch announcement
- [ ] Monitor server logs
- [ ] Be available for urgent issues

### 7.3 Post-Launch (Week 10+)
- [ ] Monitor analytics daily (first week)
- [ ] Check for broken links
- [ ] Monitor form submissions
- [ ] Gather user feedback
- [ ] Fix any reported issues
- [ ] Monitor site performance
- [ ] Check accessibility compliance

### 7.4 Ongoing Maintenance

#### Daily
- [ ] Monitor for critical errors
- [ ] Check contact form submissions

#### Weekly
- [ ] Update upcoming events
- [ ] Post announcements as needed
- [ ] Check for broken links

#### Monthly
- [ ] Upload meeting minutes
- [ ] Review analytics
- [ ] Update security patches
- [ ] Backup verification

#### Quarterly
- [ ] Content review and updates
- [ ] Performance audit
- [ ] Accessibility audit
- [ ] Security review

#### Annually
- [ ] Upload annual budget
- [ ] Review and update all content
- [ ] Design refresh evaluation
- [ ] Update copyright year
- [ ] Review and renew domain

---

## Success Criteria

### Technical
- ✅ Lighthouse score >90 for all metrics
- ✅ WCAG 2.1 AA compliance verified
- ✅ Page load time <3 seconds on 3G
- ✅ Mobile usability score >90
- ✅ No console errors
- ✅ No broken links

### Content
- ✅ All required pages published
- ✅ All content reviewed and approved
- ✅ All documents uploaded
- ✅ Calendar populated with events
- ✅ Contact information verified

### Functional
- ✅ Forms working correctly
- ✅ Calendar displaying events
- ✅ Document downloads working
- ✅ Mobile navigation working
- ✅ Search working (if implemented)

### Operational
- ✅ Staff trained on CMS
- ✅ Documentation complete
- ✅ Backup system working
- ✅ Analytics tracking
- ✅ Maintenance schedule established

---

## Troubleshooting

### Common Issues

**Issue: Build fails on Vercel**
- Check environment variables are set
- Verify all dependencies are in package.json
- Check for TypeScript errors
- Review build logs for specific errors

**Issue: Images not displaying**
- Verify image paths are correct
- Check Next.js image configuration
- Ensure images are in public folder or Sanity CDN
- Check image optimization settings

**Issue: Sanity content not showing**
- Verify API token is set
- Check CORS settings in Sanity
- Verify queries are correct
- Check network tab for API errors

**Issue: Slow performance**
- Run Lighthouse audit
- Check image sizes
- Verify lazy loading is working
- Check for large JavaScript bundles
- Review caching strategy

---

## Resources

### Documentation
- [Next.js Documentation](https://nextjs.org/docs)
- [Sanity Documentation](https://www.sanity.io/docs)
- [Tailwind CSS Documentation](https://tailwindcss.com/docs)
- [WCAG Guidelines](https://www.w3.org/WAI/WCAG21/quickref/)

### Tools
- [Lighthouse](https://developers.google.com/web/tools/lighthouse)
- [axe DevTools](https://www.deque.com/axe/devtools/)
- [WebAIM Contrast Checker](https://webaim.org/resources/contrastchecker/)
- [WAVE](https://wave.webaim.org/)

### Community
- [Next.js Discord](https://nextjs.org/discord)
- [Sanity Slack](https://slack.sanity.io/)
- [Tailwind Discord](https://tailwindcss.com/discord)

---

**Document Version**: 1.0
**Last Updated**: 2025-10-26

**Status**: Ready for implementation
