# Webflow + GSAP Editing Guidelines

This document outlines safe editing practices for this Webflow-exported project that uses GSAP animations, Webflow IX3, and custom fonts.

---

## 🎯 Quick Reference: Safe vs. Unsafe Edits

### ✅ **SAFE TO EDIT**

- **Text content** inside existing elements (e.g., changing "Portal" to "שיקוף דפוסים")
- **Inline styles** like `color`, `font-family`, `font-size`, `text-align` (as long as you don't remove `class` or `id` attributes)
- **Image/video sources** (`src` attributes) - see [Media Replacement](#media-replacement) section
- **Adding new elements** inside existing containers (but test carefully with animations)
- **Custom CSS** in the `<style>` tag or external CSS files (avoid overriding Webflow-generated classes)

### ❌ **DO NOT EDIT**

- **GSAP animation attributes:**
  - `data-w-id` attributes (used by Webflow IX3 for scroll animations)
  - `ai-desn-wrapper`, `ai-img`, `ar` attributes (custom animation markers)
  - Classes like `gsap_split_letter`, `gsap_split_word` (GSAP SplitText generates these)
- **Container structure** of animated sections:
  - `.hero_sub-heading-container`
  - `.ai-img_artwork-wrapper` and `.ai-img_artwork-inner-wrapper`
  - `.ai-desn_wrapper-*` containers
  - `.row-1`, `.row-2` in image galleries
- **Script includes** or GSAP initialization code in `index.html`
- **Webflow-generated CSS** in `css/odeds-dynamite-site-4daf96.webflow.css` (use custom CSS instead)

---

## 🎨 Layout & Animation Cautions

### Positioning Elements

- **Avoid** adding `position: absolute` to elements inside animated containers unless you test thoroughly
- **Avoid** changing flex/grid parent containers in animated sections
- **Prefer** wrapping new text inside existing containers rather than adding new siblings that might interfere with animations

### Example: Safe Text Addition

```html
<!-- ✅ GOOD: Adding text inside existing container -->
<div class="hero_sub-heading-container">
  <p class="paragraph-16 txt-white">Scroll to explore</p>
  <p class="paragraph-16 txt-white" dir="rtl">גללו למטה</p>
</div>

<!-- ❌ BAD: Adding sibling that might break animation -->
<div class="hero_sub-heading-container">...</div>
<div class="new-text">New text</div> <!-- This might interfere -->
```

### Centering Text Precisely

When you need to center text without disrupting other elements:

```html
<p style="position: absolute; left: 50%; transform: translateX(-50%); white-space: nowrap;">
  Centered text
</p>
```

---

## 🔤 Fonts & Typography

### Using Ploni Font

The Ploni font family is available in 5 weights via `fonts/custom-fonts.css`:

- **Ultralight (200)**
- **Regular (400)**
- **Medium (500)**
- **Demibold (600)**
- **Bold (700)**

**To apply Ploni:**

```html
<!-- Inline style -->
<p style="font-family: 'Ploni', sans-serif; font-weight: 700;">Bold Text</p>

<!-- Or via class (add to custom CSS) -->
.ploni-bold {
  font-family: 'Ploni', sans-serif;
  font-weight: 700;
}
```

**Note:** The font file is already loaded via `fonts/custom-fonts.css` in `index.html`.

---

## 🌐 RTL (Right-to-Left) Support for Hebrew

When adding Hebrew text:

1. **Add `dir="rtl"`** to the element
2. **Set text alignment** appropriately:
   ```html
   <p dir="rtl" style="text-align: right;">Hebrew text here</p>
   <p dir="rtl" style="text-align: center;">Centered Hebrew</p>
   ```

3. **For centered Hebrew** that needs precise alignment:
   ```html
   <p dir="rtl" style="text-align: center; position: absolute; left: 50%; transform: translateX(-50%);">
     שינוי תפיסה דרך משחק
   </p>
   ```

---

## 🖼️ Media Replacement

### Images

**Option 1: Same filename (Safest)**
- Replace the image file in `images/` folder with the same filename
- No HTML changes needed
- Animations preserved automatically

**Option 2: Update HTML `src`**
- Change the `src` attribute to point to new file
- Keep all `class` and `id` attributes intact
- Match aspect ratios to avoid layout shifts

**Example:**
```html
<!-- Before -->
<img src="images/family_1family.avif" class="ai-image">

<!-- After -->
<img src="new-images/my-image.jpg" class="ai-image">
```

### Videos

Replace images with videos by changing the tag:

```html
<!-- Before: Image -->
<img src="images/woman-portal_1woman-portal.avif" class="ai-desn_img-1">

<!-- After: Video -->
<video src="new-images/reveal2.mp4" autoplay loop muted playsinline class="ai-desn_img-1" style="width: 100%; height: 100%; object-fit: cover;"></video>
```

**Video attributes:**
- `autoplay` - plays automatically
- `loop` - repeats continuously
- `muted` - required for autoplay
- `playsinline` - plays inline on mobile
- `object-fit: cover` - fills container like image did

---

## 🎬 GSAP Animation Preservation

### Understanding GSAP SplitText

GSAP SplitText automatically splits text into letters/words at runtime. The classes `gsap_split_letter`, `gsap_split_word` are generated dynamically - **do not add these manually**.

**Safe text editing:**
```html
<!-- ✅ GOOD: Just change the text content -->
<p class="ai-desn_title">שיקוף דפוסים</p>

<!-- GSAP will automatically split this into letters -->
```

### Preserving Animation Structure

When editing animated sections, maintain:

1. **Container hierarchy** - don't remove wrapper divs
2. **Class names** - keep animation-related classes
3. **ID attributes** - preserve IDs used by GSAP selectors
4. **Data attributes** - never remove `data-w-id`, `ai-desn-wrapper`, etc.

---

## 🛠️ How to Work in This Repo

### Development Server

Run the local development server:
```bash
npm run dev
```

This starts `live-server` on port 8000 with auto-reload.

### Code Formatting (Optional)

**Prettier** is configured but not enforced. To format files:

```bash
# Format all files (if Prettier is installed)
npx prettier --write .

# Format specific file
npx prettier --write index.html
```

**Note:** Prettier is configured to ignore Webflow-generated CSS files.

### Linting (Optional)

**ESLint** is configured but warnings won't block development. To check:

```bash
# Lint JavaScript files (if ESLint is installed)
npx eslint *.js

# Or use your editor's ESLint integration
```

---

## ⚠️ Common Pitfalls

### 1. Breaking GSAP Animations

**Problem:** Text changes cause animations to break or elements disappear.

**Solution:** Always preserve `class` and `id` attributes. Only change text content or add inline styles.

### 2. Layout Shifts

**Problem:** Adding new elements causes other elements to move unexpectedly.

**Solution:** Use `position: absolute` with careful positioning, or add elements inside existing containers.

### 3. Hebrew Text Alignment

**Problem:** Hebrew text doesn't align correctly.

**Solution:** Always add `dir="rtl"` and appropriate `text-align` values.

### 4. Font Not Loading

**Problem:** Ploni font doesn't appear.

**Solution:** Ensure `fonts/custom-fonts.css` is linked in `index.html` (it already is). Use `font-family: 'Ploni', sans-serif;` with correct `font-weight`.

---

## 📝 Best Practices Summary

1. **Test after every change** - Refresh browser and scroll through animations
2. **Preserve structure** - Keep container divs and animation attributes intact
3. **Use inline styles** - For quick changes without affecting global styles
4. **Match aspect ratios** - When replacing images/videos to avoid layout shifts
5. **Document custom changes** - Note any significant structural changes for future reference

---

## 🔍 Finding Elements Safely

When you need to edit an element:

1. **Inspect in browser** - Use DevTools to find the exact element
2. **Check for animation attributes** - Look for `data-w-id`, `ai-desn-wrapper`, etc.
3. **Identify the container** - Understand the parent structure
4. **Make minimal changes** - Only change what's necessary
5. **Test immediately** - Refresh and verify animations still work

---

## 📚 Additional Resources

- **GSAP Documentation:** https://greensock.com/docs/
- **Webflow Export Guide:** https://webflow.com/export
- **RTL Support:** https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/dir

---

**Remember:** When in doubt, test in the browser. Animations are complex - small changes can have big effects!




