# Vista Fire District Website - Deployment Guide

## Simple Static Website v1

This is a simple, static HTML website that can be deployed to any web hosting service.

## What You Have

- **8 HTML pages** - Complete, responsive pages with placeholder content
- **Tailwind CSS** - Loaded via CDN (no build process needed)
- **Custom CSS** - Additional styles in `css/styles.css`
- **JavaScript** - Simple interactivity in `js/main.js`
- **Directory structure** - For documents, images, and assets

## Before You Deploy

### 1. Replace Placeholder Content

Update the following in all HTML files:

- `[Address]` - Replace with actual district address
- `[City, State ZIP]` - Replace with actual location
- `(555) 123-4567` - Replace with actual phone number
- `info@vistafd.gov` - Replace with actual email
- `[Commissioner Name]` - Add actual commissioner names
- `[Date]` - Add actual meeting dates
- Office hours and meeting schedules
- Any text in `[brackets]`

### 2. Add Your Logo

Replace the placeholder "VFD" in the header with your actual logo:

```html
<!-- Find this in header of each page -->
<div class="w-16 h-16 bg-white rounded-full flex items-center justify-center">
    <span class="text-fire-700 font-bold text-2xl">VFD</span>
</div>

<!-- Replace with -->
<div class="w-16 h-16">
    <img src="images/logo.svg" alt="Vista Fire District Logo" class="w-full h-full">
</div>
```

Place your logo file in `images/logo.svg` (or logo.png)

### 3. Add Documents

Place PDF files in the appropriate folders:

```
documents/
├── minutes/
│   ├── 2025/
│   │   └── 2025-01-15-minutes.pdf
│   └── 2024/
│       └── 2024-12-10-minutes.pdf
└── budgets/
    ├── fy2025-adopted-budget.pdf
    └── fy2024-adopted-budget.pdf
```

Update links in HTML files to match your actual file names.

### 4. Add Commissioner Photos

Place photos in:
```
images/commissioners/
├── commissioner-name-1.jpg
├── commissioner-name-2.jpg
└── ...
```

## Deployment Options

### Option 1: GitHub Pages (FREE)

**Steps:**
1. Push all files to a GitHub repository
2. Go to repository Settings > Pages
3. Select branch (usually `main`) and root folder
4. Click Save
5. Your site will be live at `https://yourusername.github.io/vistafd`

**Custom Domain:**
- Add a `CNAME` file with your domain name
- Configure DNS to point to GitHub Pages
- Enable HTTPS in GitHub Pages settings

### Option 2: Netlify (FREE)

**Steps:**
1. Sign up at netlify.com
2. Drag and drop your project folder
3. Site is live instantly
4. Configure custom domain in settings

**Benefits:**
- Automatic HTTPS
- Easy custom domain setup
- Form handling available
- Continuous deployment from Git

### Option 3: Traditional Web Hosting

**Upload via FTP:**
1. Connect to your web host via FTP
2. Upload all files to `public_html` or `www` directory
3. Ensure file permissions are correct
4. Visit your domain to see the site

**Recommended hosts:**
- DreamHost
- Bluehost
- HostGator
- Any hosting provider with static file support

### Option 4: Vercel (FREE)

**Steps:**
1. Sign up at vercel.com
2. Import from Git repository
3. Deploy with one click
4. Configure custom domain

## File Structure

```
vistafd/
├── index.html              # Home page
├── about.html             # About page
├── commissioners.html     # Board info
├── contact.html          # Contact info
├── safety.html           # Safety tips
├── meetings.html         # Meeting schedule
├── minutes.html          # Minutes archive
├── transparency.html     # Budgets & documents
├── css/
│   └── styles.css       # Custom styles
├── js/
│   └── main.js          # JavaScript
├── images/
│   ├── logo.svg
│   └── commissioners/
└── documents/
    ├── minutes/
    │   ├── 2025/
    │   └── 2024/
    └── budgets/
```

## Updating Content

### To Add a New Meeting:

1. **Add to meetings.html:**
   ```html
   <div class="border-l-4 border-fire-600 pl-4 py-2">
       <p class="font-bold text-lg text-gray-800">March 12, 2025 - Regular Board Meeting</p>
       <p class="text-gray-700">6:00 PM - District Office</p>
       <a href="documents/agendas/2025-03-12-agenda.pdf" class="text-fire-600">View Agenda →</a>
   </div>
   ```

2. **Upload agenda PDF** to `documents/agendas/`

### To Add Meeting Minutes:

1. **Upload PDF** to `documents/minutes/2025/`

2. **Add to minutes.html:**
   ```html
   <div class="flex items-center justify-between p-4 border-l-4 border-fire-600 bg-gray-50">
       <div>
           <p class="font-bold text-gray-800">January 15, 2025 - Regular Board Meeting</p>
           <p class="text-sm text-gray-600">
               <span class="bg-green-100 text-green-800 px-2 py-1 rounded text-xs">APPROVED</span>
           </p>
       </div>
       <a href="documents/minutes/2025/2025-01-15-minutes.pdf" class="bg-fire-600 text-white px-4 py-2 rounded">
           Download PDF
       </a>
   </div>
   ```

3. **Update index.html** "Recent Minutes" section

### To Update Commissioner Information:

Edit `commissioners.html` - find the commissioner card and update:
- Name
- Position
- Term dates
- Email
- Biography
- Photo path

## Testing Before Deployment

1. **Open index.html** in a web browser
2. **Test all navigation** links work
3. **Test all PDF** links (add placeholder PDFs if needed)
4. **Check mobile view** - resize browser window
5. **Test on different browsers** (Chrome, Firefox, Safari, Edge)
6. **Verify contact information** is correct
7. **Check all pages** load properly

## Browser Compatibility

This site works in:
- Chrome (latest)
- Firefox (latest)
- Safari (latest)
- Edge (latest)
- Mobile browsers (iOS Safari, Chrome Mobile)

## Performance

- **Fast loading** - Tailwind CSS loaded from CDN
- **No build process** - Pure HTML/CSS/JS
- **Lightweight** - Minimal dependencies
- **SEO friendly** - Semantic HTML

## Maintenance

### Regular Updates:
- Meeting dates and agendas
- Meeting minutes (monthly)
- Commissioner information (as changes occur)
- Contact information (as changes occur)
- Safety information (quarterly review)

### Annual Updates:
- Budget documents
- Copyright year in footer
- Review all content for accuracy

## Cost

**$0-12 per year**

- **Domain name:** ~$12/year (optional .gov requires verification)
- **Hosting:** FREE (GitHub Pages, Netlify, Vercel)
- **SSL Certificate:** FREE (included with all recommended hosts)
- **Maintenance:** Can be done by staff with basic HTML knowledge

## Support

- **Tailwind CSS Docs:** https://tailwindcss.com/docs
- **HTML Reference:** https://developer.mozilla.org/en-US/docs/Web/HTML
- **Web Accessibility:** https://www.w3.org/WAI/WCAG21/quickref/

## Need Help?

- Check HTML file comments for guidance
- Tailwind classes documentation at tailwindcss.com
- Contact a web developer for custom modifications

## Next Steps

1. ✅ Replace all placeholder content
2. ✅ Add your logo and images
3. ✅ Upload your PDF documents
4. ✅ Test thoroughly locally
5. ✅ Choose a hosting provider
6. ✅ Deploy the site
7. ✅ Configure custom domain
8. ✅ Enable HTTPS
9. ✅ Test live site
10. ✅ Train staff on updates

**Congratulations! Your Vista Fire District website is ready to go live!**
