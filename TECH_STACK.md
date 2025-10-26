# Vista Fire District - Recommended Technical Stack

## Recommended Solution: Next.js + Sanity CMS

This combination provides the best balance of performance, cost, maintainability, and ease of use for a government website.

---

## Technology Stack Details

### Frontend Framework: Next.js 14+
**Why Next.js:**
- Static Site Generation (SSG) for fast performance
- Server-Side Rendering (SSR) when needed
- Built-in image optimization
- File-based routing (intuitive URL structure)
- Excellent SEO support
- Great developer experience
- Large community and extensive documentation

**Key Features Used:**
- App Router for modern routing
- Static generation for most pages
- Dynamic routes for minutes/budgets
- Image optimization for photos
- Metadata API for SEO

### Styling: Tailwind CSS
**Why Tailwind:**
- Utility-first approach for rapid development
- Highly customizable
- Small production bundle (only used classes)
- Excellent documentation
- Mobile-first responsive design
- Consistent design system

**Additional UI Libraries:**
- **Headless UI**: Accessible components (dropdowns, modals)
- **Radix UI**: Additional accessible primitives
- **Lucide Icons**: Open-source icon set

### Content Management: Sanity CMS
**Why Sanity:**
- Free tier (generous limits, perfect for fire district)
- Real-time collaborative editing
- Structured content (better than markdown)
- Built-in image optimization and CDN
- Excellent developer experience
- Customizable Studio interface
- Version history and drafts
- Scheduled publishing
- Portable text for rich content

**Sanity Free Tier Limits:**
- 3 users
- 10,000 documents
- 5GB assets
- 500GB CDN bandwidth
- More than sufficient for fire district needs

### Hosting: Vercel
**Why Vercel:**
- Free tier for personal/small projects
- Created by Next.js team (perfect integration)
- Automatic deployments from Git
- Global CDN
- Automatic HTTPS
- Excellent performance
- Zero configuration
- Preview deployments for testing

**Vercel Free Tier Limits:**
- 100GB bandwidth/month
- Unlimited sites
- Automatic SSL
- More than sufficient for fire district traffic

### Additional Services

#### Forms: Formspree or Web3Forms
**For contact forms and feedback:**
- **Formspree**: 50 submissions/month (free tier)
- **Web3Forms**: 250 submissions/month (free tier)
- No backend code required
- Spam protection included
- Email notifications

#### Calendar: FullCalendar or React Big Calendar
**For events and meetings:**
- **FullCalendar**: Feature-rich, professional
- **React Big Calendar**: Open-source, flexible
- Data stored in Sanity CMS
- Export to Google Calendar, iCal

#### Analytics: Vercel Analytics or Plausible
**For understanding usage:**
- **Vercel Analytics**: Built-in, privacy-friendly
- **Plausible**: Privacy-focused, GDPR compliant
- No cookies required
- Lightweight tracking

#### Search: Algolia or Pagefind
**For site search:**
- **Algolia**: Free tier (10k searches/month)
- **Pagefind**: Static search, completely free
- Fast, relevant results
- Recommended: Start with Pagefind

---

## Project Structure

```
vistafd/
├── src/
│   ├── app/                          # Next.js app directory
│   │   ├── page.tsx                  # Home page
│   │   ├── layout.tsx                # Root layout
│   │   ├── about/
│   │   │   ├── page.tsx             # About main page
│   │   │   ├── commissioners/
│   │   │   ├── contact/
│   │   │   └── district-map/
│   │   ├── safety/
│   │   │   ├── page.tsx
│   │   │   ├── fire-safety/
│   │   │   ├── wildfire/
│   │   │   ├── emergency/
│   │   │   └── resources/
│   │   ├── meetings/
│   │   │   ├── page.tsx
│   │   │   ├── upcoming/
│   │   │   ├── calendar/
│   │   │   └── participate/
│   │   ├── transparency/
│   │   │   ├── page.tsx
│   │   │   ├── minutes/
│   │   │   │   ├── page.tsx
│   │   │   │   └── [year]/
│   │   │   │       └── [month]/
│   │   │   ├── budgets/
│   │   │   └── governance/
│   │   └── resources/
│   │       ├── page.tsx
│   │       ├── downloads/
│   │       ├── forms/
│   │       └── agencies/
│   ├── components/
│   │   ├── layout/
│   │   │   ├── Header.tsx
│   │   │   ├── Footer.tsx
│   │   │   ├── Navigation.tsx
│   │   │   └── MobileMenu.tsx
│   │   ├── home/
│   │   │   ├── Hero.tsx
│   │   │   ├── QuickLinks.tsx
│   │   │   ├── UpcomingEvents.tsx
│   │   │   └── NewsAnnouncements.tsx
│   │   ├── shared/
│   │   │   ├── Button.tsx
│   │   │   ├── Card.tsx
│   │   │   ├── DocumentList.tsx
│   │   │   └── EventCard.tsx
│   │   └── ui/                      # Reusable UI components
│   ├── lib/
│   │   ├── sanity/
│   │   │   ├── client.ts           # Sanity client config
│   │   │   ├── queries.ts          # GROQ queries
│   │   │   └── schemas/            # Content schemas
│   │   │       ├── commissioner.ts
│   │   │       ├── meetingMinute.ts
│   │   │       ├── event.ts
│   │   │       ├── budget.ts
│   │   │       ├── safetyTip.ts
│   │   │       └── announcement.ts
│   │   └── utils.ts                # Utility functions
│   ├── styles/
│   │   └── globals.css             # Global styles
│   └── types/
│       └── index.ts                # TypeScript types
├── studio/                          # Sanity Studio
│   ├── schemas/
│   ├── sanity.config.ts
│   └── sanity.cli.ts
├── public/
│   ├── images/
│   │   ├── logo.svg
│   │   └── og-image.jpg
│   ├── documents/                   # Static documents (if needed)
│   └── favicon.ico
├── .env.local                       # Environment variables
├── next.config.js
├── tailwind.config.js
├── tsconfig.json
├── package.json
└── README.md
```

---

## Sanity Schema Examples

### Commissioner Schema
```typescript
{
  name: 'commissioner',
  title: 'Commissioner',
  type: 'document',
  fields: [
    { name: 'name', type: 'string', title: 'Name' },
    { name: 'position', type: 'string', title: 'Position' },
    { name: 'termStart', type: 'date', title: 'Term Start Date' },
    { name: 'termEnd', type: 'date', title: 'Term End Date' },
    { name: 'photo', type: 'image', title: 'Photo' },
    { name: 'bio', type: 'text', title: 'Biography' },
    { name: 'email', type: 'string', title: 'Email' },
    { name: 'order', type: 'number', title: 'Display Order' }
  ]
}
```

### Meeting Minutes Schema
```typescript
{
  name: 'meetingMinutes',
  title: 'Meeting Minutes',
  type: 'document',
  fields: [
    { name: 'title', type: 'string', title: 'Title' },
    { name: 'meetingDate', type: 'datetime', title: 'Meeting Date' },
    { name: 'meetingType', type: 'string', title: 'Meeting Type',
      options: { list: ['Regular', 'Special', 'Emergency', 'Budget'] }
    },
    { name: 'status', type: 'string', title: 'Status',
      options: { list: ['Draft', 'Approved'] }
    },
    { name: 'document', type: 'file', title: 'PDF Document' },
    { name: 'summary', type: 'text', title: 'Summary' }
  ]
}
```

### Event Schema
```typescript
{
  name: 'event',
  title: 'Event',
  type: 'document',
  fields: [
    { name: 'title', type: 'string', title: 'Event Title' },
    { name: 'eventType', type: 'string', title: 'Event Type',
      options: { list: ['Board Meeting', 'Community Event', 'Training', 'Public Hearing'] }
    },
    { name: 'startDate', type: 'datetime', title: 'Start Date & Time' },
    { name: 'endDate', type: 'datetime', title: 'End Date & Time' },
    { name: 'location', type: 'string', title: 'Location' },
    { name: 'description', type: 'text', title: 'Description' },
    { name: 'agenda', type: 'file', title: 'Agenda (PDF)' },
    { name: 'virtualLink', type: 'url', title: 'Virtual Meeting Link' }
  ]
}
```

---

## Development Workflow

### Initial Setup (One-time)
```bash
# 1. Create Next.js project
npx create-next-app@latest vistafd-website --typescript --tailwind --app

# 2. Install Sanity
npm install next-sanity @sanity/image-url @sanity/vision

# 3. Initialize Sanity Studio
npm create sanity@latest -- --project vistafd-studio

# 4. Install additional dependencies
npm install @headlessui/react @radix-ui/react-icons
npm install react-big-calendar date-fns
npm install clsx tailwind-merge
```

### Development Process
```bash
# Terminal 1: Run Next.js dev server
npm run dev

# Terminal 2: Run Sanity Studio
cd studio && npm run dev
```

### Deployment Process
```bash
# Automatic deployment via Git
git add .
git commit -m "Update content"
git push origin main

# Vercel automatically deploys on push to main
# Preview deployments for other branches
```

---

## Cost Breakdown

### Development Phase
| Item | Cost | Notes |
|------|------|-------|
| Development | $0 - $15,000 | DIY free, professional dev varies |
| Design/Wireframes | $0 - $2,000 | Can use free tools or hire designer |

### Annual Operating Costs
| Service | Cost | Tier |
|---------|------|------|
| Domain Name | $12/year | .gov domain (special process) or .org |
| Vercel Hosting | $0/year | Free tier sufficient |
| Sanity CMS | $0/year | Free tier sufficient |
| Formspree (forms) | $0/year | Free tier (50/month) |
| SSL Certificate | $0/year | Included with Vercel |
| **TOTAL** | **~$12/year** | Plus optional services |

### Optional Upgrades
- **Sanity Grow** ($99/month): More users, documents if needed in future
- **Vercel Pro** ($20/month): More bandwidth if traffic grows significantly
- **Custom domain email** ($6/month): Professional email addresses

---

## Alternative Stacks (For Comparison)

### Option 2: WordPress
**Pros**: User-friendly, familiar
**Cons**: Security concerns, slower, hosting costs
**Annual Cost**: ~$200-500 (hosting + security)

### Option 3: Astro + Decap CMS
**Pros**: Very fast, Git-based CMS
**Cons**: Less dynamic, Git learning curve
**Annual Cost**: ~$12 (domain only)

### Option 4: Hugo + Netlify CMS
**Pros**: Extremely fast build times
**Cons**: Limited dynamic features, steeper learning curve
**Annual Cost**: ~$12 (domain only)

---

## Recommended Stack Summary

**For Vista Fire District, I recommend:**

✅ **Next.js 14** - Frontend framework
✅ **Sanity CMS** - Content management
✅ **Tailwind CSS** - Styling
✅ **Vercel** - Hosting
✅ **Formspree** - Forms
✅ **React Big Calendar** - Event calendar
✅ **Pagefind** - Site search

**Total annual cost: ~$12**
**Development time: 8-10 weeks** (see roadmap in PROJECT_SPEC.md)
**Maintenance: Minimal** - mostly content updates

---

## Getting Started

### Phase 1: Setup (Week 1)
1. ✅ Create GitHub repository
2. ⬜ Set up Next.js project
3. ⬜ Configure Sanity CMS
4. ⬜ Set up Vercel hosting
5. ⬜ Configure domain

### Phase 2: Design (Week 1-2)
1. ⬜ Create color scheme
2. ⬜ Design logo treatment
3. ⬜ Create component library
4. ⬜ Build layout templates

### Phase 3: Development (Week 3-8)
1. ⬜ Implement core pages
2. ⬜ Build CMS schemas
3. ⬜ Create reusable components
4. ⬜ Add calendar functionality
5. ⬜ Implement document management

### Phase 4: Content & Launch (Week 9-10)
1. ⬜ Populate content
2. ⬜ Test accessibility
3. ⬜ Performance optimization
4. ⬜ Deploy to production

---

## Support & Documentation

### Official Documentation
- Next.js: https://nextjs.org/docs
- Sanity: https://www.sanity.io/docs
- Tailwind CSS: https://tailwindcss.com/docs
- Vercel: https://vercel.com/docs

### Community Resources
- Next.js Discord
- Sanity Slack
- Stack Overflow
- GitHub Discussions

### Training Materials
- Next.js Learn Course (free)
- Sanity Schema Workshop (free)
- Tailwind CSS Screencasts (free)

---

## Security Considerations

### Built-in Security
- ✅ HTTPS by default (Vercel)
- ✅ No SQL injection (no database queries)
- ✅ No server to hack (static files + API routes)
- ✅ Sanity handles authentication
- ✅ Environment variables for secrets

### Best Practices
- ⚠️ Keep dependencies updated
- ⚠️ Use environment variables for API keys
- ⚠️ Implement CSP headers
- ⚠️ Sanitize form inputs
- ⚠️ Regular security audits

---

## Accessibility Features

### Built-in
- Semantic HTML from Next.js
- Keyboard navigation support
- Screen reader compatibility
- Focus management
- ARIA labels

### Testing Tools
- Lighthouse (Chrome DevTools)
- axe DevTools browser extension
- WAVE browser extension
- Screen reader testing (NVDA/JAWS)

---

## Performance Targets

### Core Web Vitals
- **LCP** (Largest Contentful Paint): < 2.5s
- **FID** (First Input Delay): < 100ms
- **CLS** (Cumulative Layout Shift): < 0.1

### Additional Metrics
- **Time to Interactive**: < 3.5s
- **Lighthouse Score**: 90+
- **Page Size**: < 1MB per page
- **Image Optimization**: WebP format, lazy loading

---

**Document Version**: 1.0
**Last Updated**: 2025-10-26
