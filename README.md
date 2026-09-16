# 365 Bites — Restaurant Website

A single-file, no-build website for **365 Bites**, Kolkata.
Everything (HTML, CSS, JavaScript) lives in `index.html` — just open it in a
browser, or upload it to any host. No frameworks, no npm, no server needed.

---

## ⚠️ The menu items are placeholders

The dishes, descriptions and prices currently on the site were made up so the
page had something to display. **Replace them with the real 365 Bites menu
before sharing the site publicly.**

## How to update the menu

1. Open `index.html` in any text editor.
2. Scroll to the bottom and find the block marked:

   ```
   ★★★  THE MENU LIVES HERE — THIS IS THE ONLY PART YOU NEED TO EDIT  ★★★
   ```

3. Edit the `MENU` list. Each dish looks like this:

   ```js
   { name: "Chicken Biryani",
     desc: "Long-grain rice, tender chicken, potato and boiled egg.",
     price: 260,
     veg: false,
     tag: "Chef's Pick" }
   ```

   | Field   | Required | Notes                                                        |
   |---------|----------|--------------------------------------------------------------|
   | `name`  | yes      | Dish name. Use `&amp;` instead of a plain `&`.               |
   | `price` | yes      | A number only — the `₹` is added automatically.              |
   | `veg`   | yes      | `true` = green veg dot, `false` = red non-veg dot.           |
   | `desc`  | no       | One short line. Use `""` or delete the line to skip it.      |
   | `tag`   | no       | Small gold badge, e.g. `"Bestseller"`, `"Chef's Pick"`.      |

4. To add a whole new section (Desserts, Beverages, Breads…), copy one of the
   `{ id: ..., label: ..., dishes: [...] }` blocks and give it a new `id`.
   The filter tabs at the top of the menu build themselves — nothing else to change.

5. Save and refresh the browser.

## What's on the page

Sticky navigation · hero with tap-to-call / WhatsApp ordering card · about
section · filterable menu with veg / non-veg indicators · occasions (takeaway,
family, office parties) · call-to-action band · contact details with an
embedded Google map · footer · floating WhatsApp button.

Also included: responsive layout down to small phones, keyboard-accessible
navigation, `prefers-reduced-motion` support, a print stylesheet that prints a
clean two-column menu, social share tags, and `Restaurant` structured data so
Google can pick up the address and phone numbers.

## Contact details used on the site

- **Phone:** 9804990098 / 9007753099
- **WhatsApp:** 9804990098
- **Address:** 253/C/1, Netaji Subhash Road, Kolkata 700047

These appear in several places (nav, hero, contact section, footer, and the
structured-data block in `<head>`). If a number changes, search the file for
the old number and replace every occurrence.

## Publishing it

**GitHub Pages** — push this repo, then in Settings → Pages choose the branch
and `/ (root)`. The site goes live at `https://<user>.github.io/<repo>/`.

**Any other host** — upload `index.html`. That's the whole site.

## Nice next steps

- Swap the placeholder menu for the real one.
- Add real food photography (the hero and about section are currently
  typographic, which keeps the page fast and avoids stock-photo look).
- Add opening hours to the contact section and to the structured data.
