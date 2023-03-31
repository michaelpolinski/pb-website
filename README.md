# Privacy Backplane project website

## Contributing

### Content changes

- Fork this repository and make changes.
  - Add names with web links to `content/home/team.md` when necessary. Student name lists should maintain ascending alphabetical order by last name.
  - Add papers to `content/home/publications.md` (with PDFs in `static/pdf/`). The list should maintain descending order by date.
  - Fix typos.
- [Create a GitHub pull request](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request) with the changes.
  - [This](https://docs.github.com/en/get-started/quickstart/contributing-to-projects) is a more complete tutorial.

### Development

- This site is built with [Hugo](https://gohugo.io/). Use `hugo server` to run the development server. Use `hugo` to render the complete site with a root of `./public/` (this should be done automatically by CI).
- Content lives in `content/`. Specifically, files in `content/home/` are rendered as sections of the home page. Edit directly. Create a new section called NAME with `hugo new home/NAME.{md,html}`, then edit `content/home/NAME.{md,html}`. The parameter `weight` in the frontmatter controls the section order. 

### Images

Thanks to a little template sorcery, _query strings_ can be used like this to set the width and height of images in `*.md` content:

```markdown
![My picture](/image.png?width=100&height=100)
```

Paths are relative to `static/`.

#### Next-gen image formats (WebP/AVIF)

To create {WebP, AVIF} copies of `*.{jpg,png}` images, run
  
```bash
find ./static/img/ -type f -name '*.png' -exec sh -c 'avifenc --min 10 --max 30 $1 "${1%.png}.avif"' _ {} \;
find ./static/img/ -type f -name '*.jpg' -exec sh -c 'cwebp $1 -o "${1%.jpg}.webp"' _ {} \;
```

with `libavif` and `libwebp` installed.

(source: <https://pawelgrzybek.com/webp-and-avif-images-on-a-hugo-website/>)

This will cause all images to be included in a `<picture>` to improve performance in modern browsers.
See the aforementioned template, `layouts/_default/_markup/render-image.html`, for details.

## Favicons

- Start with an SVG favicon `favicon.svg`.
  - This should be a logo designed for the project.
  - To make a temporary one:
    - create one on an app like <https://formito.com/tools/favicon> from text/emoji
    - vectorize a raster image using something like <https://vectorizer.ai/>.
- Optimize it using <https://jakearchibald.github.io/svgomg/>. Optional, but a good idea.
- Use <https://realfavicongenerator.net/> to get `android-chrome-192x192.png`, `android-chrome-512x512.png`, `apple-touch-icon.png`, `favicon.ico`, and `safari-pinned-tab.svg`. Put these, along with `favicon.svg`, in `static/`. Don't forget to check `assets/site.webmanifest`.
  - Build scripts that automate this step are welcome.

This is one of the ever-moving targets of web development. For more complete advice, see
- <https://caniuse.com/link-icon-svg>
- <https://dev.to/masakudamatsu/favicon-nightmare-how-to-maintain-sanity-3al7>
- <https://web.dev/building-an-adaptive-favicon/> .
