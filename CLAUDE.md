# DocuAPI Documentation - Development Instructions

## Project Overview
This is the official documentation site for DocuAPI (docuapi.io), a SaaS platform that turns any fillable PDF into a REST API with AI-powered field mapping. Built with Docusaurus classic theme and TypeScript support.

**Site URL**: https://docuapi.io  
**Purpose**: Documentation-only site (no blog) for the DocuAPI SaaS platform

## Tech Stack
- **Framework**: Docusaurus 3.8.1 (React-based documentation framework)
- **Package Manager**: pnpm
- **Language**: TypeScript
- **Theme**: Classic Docusaurus theme

## Project Structure
```
documentation/
└── pdf-api-docu/            # Main Docusaurus project
    ├── docs/                # Documentation pages
    │   └── intro.md        # Getting Started guide
    ├── src/                 # React components and pages
    │   ├── components/      # Custom React components
    │   ├── css/            # Custom styles
    │   └── pages/          # Homepage only
    ├── static/             # Static assets (images, etc.)
    ├── docusaurus.config.ts # Main configuration
    ├── sidebars.ts         # Sidebar navigation config
    └── package.json        # Dependencies
```

## Development Commands

All commands should be run from the `pdf-api-docu` directory:

```bash
cd pdf-api-docu
```

### Start Development Server
```bash
pnpm start
```
- Runs on http://localhost:3000
- Hot reloading enabled
- User is running this separately

### Build for Production
```bash
pnpm build
```
- Creates optimized static build in `build/` directory

### Serve Production Build Locally
```bash
pnpm serve
```
- Serves the built website locally for testing

### Type Checking
```bash
pnpm typecheck
```

## Key Files to Edit

### Documentation Content
- **docs/**: Add new documentation pages here as `.md` or `.mdx` files
- **sidebars.ts**: Configure sidebar navigation structure
- **docusaurus.config.ts**: Site metadata, navigation, theme settings

### Customization
- **src/css/custom.css**: Global styles and theme variables
- **src/pages/**: Custom pages outside of docs
- **src/components/**: Reusable React components

## Adding Documentation

### Create a New Doc Page
1. Add a `.md` or `.mdx` file in `docs/` directory
2. Include front matter for metadata:
```markdown
---
sidebar_position: 1
title: "Page Title"
---
```

### Organize with Categories
Create `_category_.json` files in subdirectories:
```json
{
  "label": "Category Name",
  "position": 2,
  "link": {
    "type": "generated-index"
  }
}
```

## Deployment Notes
- Build command: `pnpm build`
- Output directory: `build/`
- Can deploy to GitHub Pages, Vercel, Netlify, etc.

## Current Status
✅ Docusaurus project created with classic theme
✅ Configured with pnpm package manager
✅ TypeScript support enabled
✅ Project renamed from `pdf-api` to `pdf-api-docu`
✅ DocuAPI branding applied throughout the site
✅ Getting Started documentation added with code examples
✅ Homepage updated with DocuAPI features
✅ Default tutorial content removed
✅ Blog functionality completely removed
✅ GitHub links removed from navigation
✅ Site configured as documentation-only for docuapi.io
✅ Footer updated with relevant links to main site
✅ Development server running (managed by user)

## Next Steps Suggestions
1. Add more API documentation pages:
   - Authentication & API Keys
   - Field Types & Validation
   - Webhooks Configuration
   - Rate Limiting
   - Error Codes Reference
2. Customize color scheme in `src/css/custom.css` to match DocuAPI branding
3. Add comprehensive API reference with all endpoints
4. Add SDKs and code examples for popular languages
5. Consider adding search functionality (Algolia DocSearch or local search)
6. Configure deployment (e.g., subdomain like docs.docuapi.io)
7. Add custom logo and favicon to match main site branding
