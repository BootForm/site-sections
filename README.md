# site-sections

**[Browse them live: bootform.github.io/site-sections](https://bootform.github.io/site-sections/)**

Copy-paste page sections for a real website: heroes, feature grids, how it works, testimonials,
pricing, FAQs, calls to action, footers and content grids. 27 of them, each rendering live next to
its code, with a switch to see it at desktop, tablet or phone width, and a light/dark toggle.

Written in Tailwind CSS v4, and made to survive being pasted into a VitePress page, which most
section libraries don't (see [Why some classes end in `!`](#why-some-classes-end-in-)).

## What's in here

| Category | Sections |
|---|---|
| [Heroes](https://bootform.github.io/site-sections/heroes.html) | Centered, split with image, photo backdrop, with a form, announcement and screenshot |
| [Features](https://bootform.github.io/site-sections/features.html) | Icon grid, alternating image and text, tabs (no JavaScript), sticky heading, bento grid |
| [How it works](https://bootform.github.io/site-sections/steps.html) | Numbered steps, timeline |
| [Social proof](https://bootform.github.io/site-sections/social-proof.html) | Testimonial cards, quote banner, logo strip, stats row |
| [Pricing and FAQ](https://bootform.github.io/site-sections/pricing.html) | Two tiers, three tiers, comparison table, FAQ accordion |
| [Calls to action and footers](https://bootform.github.io/site-sections/cta-footers.html) | CTA band, newsletter band, simple footer, footer with columns |
| [Content](https://bootform.github.io/site-sections/content.html) | Card grid, team, photo gallery |

Each section is one plain HTML file under [`sections/`](sections/), so you can also copy it
straight from GitHub.

## Using one

1. **Tailwind CSS v4.** Your site needs it. Every
   [BootForm VitePress template](https://github.com/BootForm) already has it.
2. **Your brand colour.** Snippets use `brand-50`, `brand-500` and `brand-600`. Define those three
   in your `@theme` block (the BootForm templates already do), or find and replace `brand` with a
   Tailwind colour such as `indigo`.
3. **Paste it**, then swap the example text, the `#` links and the
   [Picsum](https://picsum.photos) placeholder photos for your own.

Using [Claude Code](https://claude.com/claude-code)? Install the `vitepress` plugin from
[`BootForm/site-skills`](https://github.com/BootForm/site-skills) and run
`/vitepress:add-section`. It picks the section, pastes it into your page, and adapts it.

### Why some classes end in `!`

Paste a normal Tailwind section into a VitePress page and it comes out wrong: headings the wrong
size, a stray border above every `<h2>`, links underlined, lists with bullets, tables striped.
VitePress's own content styles (`.vp-doc`) beat plain Tailwind classes. So every snippet here puts
`!` (Tailwind v4's important modifier) on exactly the classes those styles would otherwise
override. Outside VitePress the `!` does nothing harmful.

### Links and images on a VitePress site

On a VitePress site served from a subpath (GitHub Pages), an internal link written as
`href="/contact"` works in `npm run dev` and 404s once deployed. Write it as
`:href="withBase('/contact')"` and import `withBase` from `vitepress` in the page's
`<script setup>`. Same for a local image: `:src="withBase('/photos/pool.jpg')"`.

### Forms

The hero with a form and the newsletter band post to `https://f.bootform.com/__YOUR_FORM_ID__`.
Generate your own form ID at [bootform.com/uuidgenerator](https://bootform.com/uuidgenerator) and
claim it before the page goes live, or point `action` at any other form backend. Keep the hidden
`_honeypot` input.

## Every section is checked

Each one was rendered at 1280px and at a true 390px phone width, in light and dark mode, and also
pasted into a real VitePress template's `layout: home` page and built, before it was published.

## License

MIT. Use them on anything, commercial or not.
