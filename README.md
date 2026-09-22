# 365 Bites — Restaurant Website

A single-page, no-build website for **365 Bites**, Kolkata.

**`index.html` is the entire website — one self-contained file.** The logo,
the hero photograph and the tab icon are embedded inside it, so it renders
correctly on its own: email it, send it over WhatsApp, open it from a USB
stick, or upload just that one file to any host. There is nothing else it
needs. No frameworks, no npm, no build step, no server.

```
index.html          the whole site — markup, styles, script, menu data, images
assets/             the source images, kept here so they stay editable
  logo.png            logo, transparent — used in the nav bar
  logo-light.png      logo recoloured for dark backgrounds (used in the footer)
  hero-food.jpg       hero photograph
  icon.png            browser tab / home-screen icon
assets/dishes/      the dish photographs — THESE ARE LOADED BY THE PAGE
365 bites menue card 12 pages - Copy.pdf   the source menu card
```

`assets/logo.png`, `logo-light.png`, `hero-food.jpg` and `icon.png` are **not**
loaded by the page — they're the originals to edit if you want to change one.
After editing, re-embed it (see *Replacing an image* below).

**`assets/dishes/` is different — the page does load those files.** The dish
photographs stay external on purpose: there are twenty of them, and embedding
them would add over a megabyte to the page and force every one to download
before anything appeared on screen. As separate files they load lazily, so a
visitor only downloads the photos they actually scroll to.

So when you publish, upload `index.html` **and** the `assets/dishes/` folder.
If the folder is missing the site still works perfectly — the photo cards
simply hide themselves and everything else is unaffected.

## Adding a dish photo

1. Put the photo in `assets/dishes/`. Square-ish crops look best; keep each
   file under about 80KB.
2. In `index.html`, find the block marked **DISH PHOTOS** and add a line:

   ```js
   { img:"assets/dishes/mutton-biryani.jpg", name:"Mutton Biryani",
     find:"Mutton Biriyani with Egg" }
   ```

   `find` must match a dish name in the menu exactly — the price is then read
   from the menu automatically, so prices never have to be typed twice. Omit
   `find` and the card shows the photo and caption with no price.

The brand colours, logo, hero photo and all menu items were taken from the
printed menu card PDF in this repo. Brand palette: maroon `#501316`,
orange `#F47216`, cream `#FFF7EE`.

## Updating the menu

1. Open `index.html` in any text editor.
2. Near the bottom, find the block marked:

   ```
   ★★★  THE MENU LIVES HERE — THIS IS THE ONLY PART YOU NEED TO EDIT  ★★★
   ```

3. The menu is a list of **groups** (the filter tabs), each holding
   **sections** (the headings), each holding **items**:

   ```js
   { id:"biryani", label:"Biryani", sections:[
     { title:"Biryani", items:[
       { n:"Chicken Biryani with Egg", p:120 },
       { n:"Alu Biryani", p:60, v:1 }
     ]}
   ]}
   ```

   | Field  | Required | Meaning                                                     |
   |--------|----------|-------------------------------------------------------------|
   | `n`    | yes      | Dish name. Write a literal `&` as `&amp;`.                  |
   | `p`    | yes      | Price as a number only — the `₹` is added automatically.    |
   | `v`    | no       | `v:1` marks it vegetarian (green dot). Omit for non-veg.    |
   | `d`    | no       | A description line under the name.                          |
   | `tag`  | no       | Small orange badge, e.g. `tag:"Special"`.                   |

4. To add a new tab, copy a whole `{ id:..., label:..., sections:[...] }` block
   and give it a new `id`. The tabs build themselves — nothing else to change.

5. Save and refresh.

### A note on menu spellings

The printed card spells some dishes two ways (Biryani / Biriyani, Chili /
Chilli, Moghlai / Mughlai). The site keeps each name exactly as printed, and
the search box folds the variants together so either spelling finds the dish.
If you add more variants, extend the `norm()` function just above the render
code.

### One item to confirm

The printed card lists **"Special Mutton Biryani without Egg"** twice, at ₹290
and ₹300. Every other biryani pair on the card is *with egg* priced ₹10 higher
than *without*, so the site shows ₹290 as **without egg** and ₹300 as
**with egg**. Please confirm this is right and correct it if not.

## Contact details used on the site

- **Phone:** 9804990098 / 9007753099
- **WhatsApp:** 9804990098
- **Address:** 253/C/1, Netaji Subhash Road, Kolkata 700047

These appear in the nav, hero, contact section, footer and in the structured
data in `<head>`. If a number changes, search the file for the old number and
replace every occurrence.

## What's on the page

Sticky navigation · hero with the food photo and a tap-to-call ordering card ·
about · searchable, filterable menu (214 dishes) with veg / non-veg indicators ·
occasions · call-to-action band · contact with an embedded map · footer ·
floating WhatsApp button.

Also included: responsive layout down to small phones, a sticky filter bar with
horizontally scrollable tabs on mobile, `prefers-reduced-motion` support, a
print stylesheet that prints just the menu in two columns, Open Graph tags for
link previews, and `Restaurant` structured data so Google can pick up the
address, phone numbers and cuisines.

## Publishing it

**GitHub Pages** — push the repo, then Settings → Pages → select the branch and
`/ (root)`. The site goes live at `https://<user>.github.io/<repo>/`.

**Any other host** — upload `index.html`. That single file is the whole site.

## Replacing an image

Because the images are embedded, swapping one is a two-step job. Put the new
image in `assets/` under the same name, then convert it to a data URI and
paste it over the old one in `index.html`:

```bash
# prints  data:image/png;base64,iVBOR...
python3 -c "import base64;print('data:image/png;base64,'+base64.b64encode(open('assets/logo.png','rb').read()).decode())"
```

In `index.html`, find the `src="data:image/png;base64,..."` you want to
replace and swap in the new string. Keep images small — under about 150KB
each — so the page stays quick to load.

## Possible next steps

- Add opening hours to the contact section and to the structured data.
- Add photographs of your own dishes to the menu sections.
- Register a domain and point it at GitHub Pages.

## The About-section collage

The About section shows a staggered collage of four dishes with a "365 days a
year" badge over it. The four are chosen in the markup — search `index.html`
for `class="collage"` and swap the filenames for any others in
`assets/dishes/`. Pick photos with dark or neutral backgrounds; they sit
better against the cream page than the bright turquoise ones.

Like the gallery, the collage hides itself if the photos aren't deployed, and
the About section falls back to a single column of text.
