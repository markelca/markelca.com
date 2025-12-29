# markelca.com

Personal website and blog of Markel Cuesta — software engineering, automation, and tech notes.

Built with [Hugo](https://gohugo.io/) using the [hello-friend-ng](https://github.com/rhazdon/hugo-theme-hello-friend-ng) theme.

🌐 **Live site:** [https://markelca.com](https://markelca.com)

## Prerequisites

- [Hugo](https://gohugo.io/installation/) (Extended version recommended)
- Git

## Getting Started

### Clone the repository

```bash
git clone https://github.com/markelca/markelca.com.git
cd markelca.com
```

### Initialize theme submodule

```bash
git submodule update --init --recursive
```

### Run locally

```bash
hugo server -D
```

The site will be available at `http://localhost:1313`

## Project Structure

```
.
├── archetypes/       # Content templates
├── assets/           # Asset files (images, etc.)
├── content/          # Site content
│   ├── about/        # About page
│   └── posts/        # Blog posts
├── data/             # Data files
├── i18n/             # Internationalization
├── layouts/          # Custom layouts and shortcodes
│   └── shortcodes/   # Custom Hugo shortcodes
├── public/           # Generated site (gitignored)
├── resources/        # Hugo resources cache
├── static/           # Static files (copied as-is)
└── themes/           # Theme files
```

## Creating Content

### New blog post

```bash
hugo new posts/my-new-post/index.md
```

### New page

```bash
hugo new about/my-page.md
```

## Custom Shortcodes

This site includes custom shortcodes for enhanced content formatting.

### Available Shortcodes

- **`layout`** - Multi-column layout container
- **`column`** - Individual columns with alignment control
- **`figure`** - Enhanced image display with captions

**📖 For complete documentation, usage examples, and parameters, see [SHORTCODES.md](SHORTCODES.md)**

## Building for Production

```bash
hugo --minify
```

The site will be generated in the `public/` directory.

## Configuration

Site configuration is in `hugo.toml`. Key settings:

- **baseURL**: Site URL
- **title**: Site title
- **theme**: Hugo theme name
- **params**: Theme-specific parameters
- **menu**: Navigation menu items
- **social**: Social media links

## Deployment

The site can be deployed to any static hosting service:

- [Netlify](https://www.netlify.com/)
- [Vercel](https://vercel.com/)
- [GitHub Pages](https://pages.github.com/)
- [Cloudflare Pages](https://pages.cloudflare.com/)

## License

Content is licensed under [CC BY-NC 4.0](https://creativecommons.org/licenses/by-nc/4.0/).

Theme by [Djordje Atlialp](https://github.com/rhazdon).

## Contact

- **Email:** cuesta.markel@proton.me
- **GitHub:** [@markelca](https://github.com/markelca)
- **LinkedIn:** [markel-cuesta](https://linkedin.com/in/markel-cuesta)

---

© 2025 Markel Cuesta
