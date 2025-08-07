# DocuAPI Documentation

Official documentation site for [DocuAPI](https://docuapi.io) - Turn any fillable PDF into a REST API with AI-powered field mapping.

## 🚀 Overview

This repository contains the documentation website for DocuAPI, built with [Docusaurus 3](https://docusaurus.io/). The documentation provides comprehensive guides and API references for integrating DocuAPI into your applications.

## 📚 Documentation

Visit the live documentation at: [https://docuapi.io](https://docuapi.io)

### Key Features Documented

- **Getting Started** - Quick setup and first API call
- **AI Field Mapping** - How DocuAPI automatically maps PDF fields
- **REST API Reference** - Complete endpoint documentation
- **Authentication** - API key management and security
- **Error Handling** - Response codes and troubleshooting
- **Code Examples** - Multiple language implementations

## 🛠️ Development

### Prerequisites

- Node.js 18.0 or higher
- pnpm package manager

### Installation

```bash
# Clone the repository
git clone https://github.com/orhanbiler/pdf-api-docu.git
cd pdf-api-docu

# Install dependencies with pnpm
pnpm install
```

### Local Development

```bash
# Start the development server
pnpm start
```

This command starts a local development server at `http://localhost:3000`. Most changes are reflected live without having to restart the server.

### Build

```bash
# Create production build
pnpm build
```

This command generates static content into the `build` directory that can be served using any static hosting service.

### Serve Production Build

```bash
# Test production build locally
pnpm serve
```

## 📁 Project Structure

```
pdf-api-docu/
├── docs/                 # Documentation markdown files
│   └── intro.md         # Getting Started guide
├── src/
│   ├── components/      # React components
│   ├── css/            # Custom styles
│   └── pages/          # Custom pages (homepage)
├── static/             # Static assets
├── docusaurus.config.ts # Site configuration
├── sidebars.ts         # Sidebar navigation
└── package.json        # Dependencies
```

## 🤝 Contributing

We welcome contributions to improve our documentation! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/improvement`)
3. Make your changes
4. Commit with clear messages (`git commit -m 'Add new API examples'`)
5. Push to your branch (`git push origin feature/improvement`)
6. Open a Pull Request

### Documentation Guidelines

- Use clear, concise language
- Include code examples where applicable
- Test all code samples
- Follow the existing markdown structure
- Update navigation in `sidebars.ts` if adding new pages

## 🚀 Deployment

The documentation site can be deployed to various platforms:

- **GitHub Pages**
- **Vercel**
- **Netlify**
- **Custom hosting**

Build command: `pnpm build`  
Output directory: `build/`

## 📝 License

This documentation is proprietary to DocuAPI. All rights reserved.

## 🔗 Links

- **Main Website**: [https://docuapi.io](https://docuapi.io)
- **API Dashboard**: [https://docuapi.io/dashboard](https://docuapi.io/dashboard)
- **API Status**: [https://status.docuapi.io](https://status.docuapi.io)
- **Support**: [https://docuapi.io/contact](https://docuapi.io/contact)

## 💻 Tech Stack

- **Framework**: [Docusaurus 3.8.1](https://docusaurus.io/)
- **Language**: TypeScript
- **Package Manager**: pnpm
- **Styling**: CSS Modules
- **Theme**: Docusaurus Classic

---

Built with ❤️ by the DocuAPI team