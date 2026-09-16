# 365 Bites — Restaurant Website

A single-page, no-build website for **365 Bites**, Kolkata.
Everything is plain HTML, CSS and JavaScript — open `index.html` in a browser,
or upload the folder to any host. No frameworks, no npm, no server needed.

```
index.html          the entire site (markup, styles, script, menu data)
assets/logo.png     logo, transparent — for light backgrounds
assets/logo-light.png  logo recoloured for dark backgrounds (used in the footer)
assets/hero-food.jpg   hero photograph
assets/icon.png        browser tab / home-screen icon
365 bites menue card 12 pages - Copy.pdf   the source menu card
```

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

**Any other host** — upload `index.html` and the `assets/` folder.

## Possible next steps

- Add opening hours to the contact section and to the structured data.
- Add photographs of your own dishes to the menu sections.
- Register a domain and point it at GitHub Pages.
