# Liberty Foods – ordering website (demo)

Single-page, mobile-first ordering site for **Liberty Foods** (Liberty Hostel, near Canam Premium, KNUST area). Built by SyberCodes as a **sales demo**. Same engine as the Adams Kitchen demo (see its README for the long version).

## Files
```
index.html   # whole site: markup, CSS, menu data, logic
img/         # hero.jpg, jollof.jpg, fried.jpg, fries.jpg (stand-in photos)
```
Deploy with `index.html` at the folder root. No build step, no backend. Only external request: Google Fonts (Archivo for headings, DM Sans for body).

## Brand
From their packaging: coral/orange-red `#e4573a` on white, red-and-white stripe band (the `.stripes` element copies the bag's bottom stripes), chef-hat "LB" badge.
CSS variables are at the top of `<style>` (`--coral`, `--coral2`, `--ink`, `--blush`...).
**Logo:** `img/logo.png` is traced from the bag photo (`img/bag.jpg`, a packaging mock-up the owner supplied), so edges are slightly soft. It is used in the header (`.mark`) and as the favicon. Ask the business for their original logo file and replace `img/logo.png`. The "LB" tile for items without photos is still a CSS placeholder.

## Sections
Demo bar → stripe → sticky header (logo, Order button) → coral hero with round plate photo → stripe → menu (`#sections`, generated from `MENU`) → "Find us" (bag photo + `tel:` links) → stripe footer. Item sheet (`#sheet`), cart drawer (`#drawer`), demo modal (`#modal`), mobile cart bar (`#bar`).

## Menu data
Edit the `MENU` array in the script:
```js
{ id:'jollof', name:'Jollof Rice', desc:'...', img:'jollof',   // img optional: shows the LB tile if missing
  sizes:[['Regular',35],['Large',50]],                          // or price:30 for a single price
  groups:[{n:'Protein', c:[['Chicken',0],['Sausage',3],['Fish',8]]}] }  // [label, extra cost]
```
Price = size price (or `price`) + extra cost of each chosen option. Items with `sizes`/`groups` open the sheet; plain items (the "Extras & drinks" section, `small:1`) add straight to the cart. An option labelled `None` is left out of the order text.

## Placeholders to confirm
- **All prices and items beyond the five dishes** are samples (GH₵).
- **WhatsApp number** `WA='233248724634'` is from their packaging (024 872 4634; second number 050 316 7431). Confirm which takes orders.
- **Photos:** jollof, fried rice and hero are stand-ins from other demos; loaded fries is cropped from another restaurant's flyer; spaghetti and indomie have no photo yet. Replace all with Liberty Foods' own photos (keep filenames or edit `img:`) before showing it as theirs.
- Opening hours and delivery area/fee are not shown (unknown).

## Demo vs live
Demo mode shows the WhatsApp message in a modal and sends nothing. To go live, in the `#send` handler replace
`$('#mmsg').textContent=msg;closeAll();$('#modal').classList.add('on')` with
`window.open('https://wa.me/'+WA+'?text='+encodeURIComponent(msg),'_blank','noopener');closeAll();`
then remove the `.demo` bar, the `noindex` meta tag and the modal.

## Hosting note
Vercel's free Hobby plan is non-commercial; a client's live site needs a paid plan or another host (check its terms).
