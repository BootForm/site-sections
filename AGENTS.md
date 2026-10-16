# Working in this repo

A gallery of copy-paste page sections. GitHub Pages serves this repo straight from `main` (see
`.nojekyll`); there is no build step for readers.

## Where things live

- **`sections/<category>/<id>.html`**: one section per file. **These are the source of truth.**
  The gallery pages, the copy button, and the `add-section` skill in `BootForm/site-skills` all
  read these files.
- **`sections.json`**: the order, titles, descriptions and notes for every category and section.
- **`build.mjs`**: generates `index.html` and one page per category from the two above. Plain
  Node, no dependencies. **Never edit the generated `*.html` pages at the repo root by hand.**
  Edit a snippet or `sections.json`, run `node build.mjs`, and commit both. CI
  (`.github/workflows/check.yml`) fails if the generated pages are stale.

## Adding a section

1. Write `sections/<category>/<id>.html`, starting from an existing one in the same category.
2. Add an entry to that category in `sections.json` (`id`, `title`, `description`, optional
   `notes`).
3. `node build.mjs`, then look at it: desktop, tablet and phone width, light and dark.
4. Paste it into a `layout: home` page of a real VitePress template and build that too (see
   "Checking a section" below). A section that looks right in the gallery can still break there.

## The rules every snippet follows

These exist because a snippet is pasted into a VitePress markdown page far more often than
anywhere else. Breaking one produces a green build and a broken page, with no error.

- **No blank lines inside a snippet.** In markdown, a blank line ends an HTML block, and whatever
  follows is parsed as markdown: an indented line becomes a code block, a bare line becomes a
  paragraph.
- **No `{{ }}`.** VitePress compiles every page as a Vue template, so double braces are an
  interpolation.
- **No `<script>`.** Interactive sections use CSS only: the tabs are hidden radio buttons plus
  `has-[]`/`group-has-[]` variants, the FAQ is `<details name="faq">`.
- **Only `brand-50`, `brand-500` and `brand-600`.** Those are the only brand tokens the BootForm
  templates define. Anything else (`brand-400`, `brand-700`) silently generates no CSS there.
- **`!` on whatever `.vp-doc` or VitePress's `base.css` sets, and nothing else.** That means:
  - `h1`-`h3`: size, weight, line height, margin. `h2` also needs `border-t-0! pt-0!` (`.vp-doc`
    gives every `h2` a top border and padding).
  - `p`, `summary`, `figure`, `blockquote`: margin, and line height where it matters.
    `blockquote` also needs `border-l-0! pl-0!`.
  - `a`: colour and `no-underline!`, on every link, including button-styled ones.
  - `ul`/`ol`: `list-none! pl-0!` plus margins; `li`: `mt-0!` (`.vp-doc` adds space between
    list items).
  - `table`, `tr`, `th`, `td`: `table!`, `my-0!`, borders, backgrounds, padding, and on `th` the
    text alignment, size, weight and colour. See `sections/pricing/comparison-table.html`.
  - Form controls: border, background and padding, the same trick the templates' own contact
    forms use.
- **Buttons stack full-width on a phone** (`flex-col` below `sm`, capped at `max-w-xs`) and sit
  side by side from `sm` up.
- **Placeholders, not real data.** Links are `#`, photos come from Picsum, people are initials
  avatars, logos are invented names. Forms post to `https://f.bootform.com/__YOUR_FORM_ID__` with
  a hidden `bform_website` input. Never put a real form ID in a snippet: whoever claims it first owns
  every submission to it.
- **Dark mode uses the `dark:` variant on a `.dark` ancestor**, which is how VitePress toggles it.
  Small brand-coloured text uses `dark:text-brand-50` in dark mode, because `brand-500` on a
  near-black background is too low contrast to read.
- **Every section is original.** Inspired by the usual section types, never copied from a
  component library (CodyHouse, Tailwind UI, Flowbite or any other).

## Checking a section

A build that succeeds says nothing about whether a section looks right. Before publishing:

- Open the gallery page and switch the preview between Desktop, Tablet and Mobile, in light and
  dark mode.
- Paste the snippet into a `layout: home` page of one of the VitePress templates (a scratch copy
  of `vitepress-villa` works), `npm run build`, and look at the built page. This is how the
  comparison table's `th` background, colour and alignment problems were found: they only happen
  under `.vp-doc`.

## Writing style

- Second person, present tense, short sentences.
- **No em dashes or en dashes**, in docs or in snippet copy. Use a comma, a colon, a full stop, or
  brackets. For "not included" in a table, use the line icon the comparison table already uses.
- No AI attribution in commits or pull requests, here or anywhere else in this organisation.
