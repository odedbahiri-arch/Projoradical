# 📸 Image Replacement Guide

## 🎯 **BEST METHOD: Replace Files (Safest)**

### **Option 1: Same Filenames (Recommended - Zero Code Changes)**

**Steps:**
1. **Prepare your new images** - Make sure they're `.avif` format (or convert them)
2. **Keep the same dimensions** - Try to match aspect ratios to avoid layout shifts
3. **Replace files directly** in the `images/` folder:
   - Keep the **exact same filename**
   - Place new image in `images/` folder
   - Overwrite the old file

**Example:**
```
Old: images/family_1family.avif
New: images/family_1family.avif (same name, different image)
```

**✅ Advantages:**
- No HTML changes needed
- Animations preserved automatically
- Sizes maintained
- Zero risk of breaking GSAP

---

## 📋 **Gallery Images List (AI Images Section)**

These are the images in the scrollable gallery:

### **Row 1 Images:**
1. `family_1family.avif`
2. `3_13.avif`
3. `lobster_1lobster.avif`
4. `9999_19999.avif`
5. `99_199.avif`
6. `999999_1999999.avif`
7. `1_11.avif`
8. `woman-portal_1woman portal.avif`
9. `9_19.avif`

### **Row 2 Images:**
1. `8_18.avif`
2. `gentleman_1gentleman.avif`
3. `kitchen_1kitchen.avif`
4. `6_16.avif`
5. `strawberries_1strawberries.avif`
6. `cat_1cat.avif`
7. `5_15.avif`
8. `99999_199999.avif`

---

## 🔄 **Option 2: Update HTML (If You Want Different Filenames)**

If you want to use different filenames, I can update the HTML for you. Just tell me:
- Which image to replace
- What the new filename is

**Example:**
- "Replace `family_1family.avif` with `my-new-image.avif`"

---

## ⚠️ **Important Notes:**

### **Image Format:**
- ✅ **Preferred:** `.avif` (best compression)
- ✅ **Also works:** `.webp`, `.jpg`, `.png`
- ⚠️ If using different format, I'll need to update the HTML

### **Image Dimensions:**
- Try to match **aspect ratios** to avoid layout shifts
- Recommended sizes:
  - **Portrait images:** ~768px width
  - **Landscape images:** ~1104px width
  - **Square images:** ~768x768px

### **What's Preserved:**
- ✅ All `ai-image-wrapper` classes
- ✅ All `ai-image` classes
- ✅ GSAP scroll animations
- ✅ Layout structure (`row-1`, `row-2`)
- ✅ Responsive `srcset` attributes (if applicable)

---

## 🛠️ **Quick Steps:**

1. **Prepare your images:**
   - Convert to `.avif` format (or keep original format)
   - Optimize file sizes
   - Match aspect ratios

2. **Replace files:**
   - Copy new images to `images/` folder
   - Use same filenames OR tell me new filenames

3. **Test:**
   - Refresh browser (live-server will auto-reload)
   - Check animations still work
   - Verify sizes look good

---

## 💡 **Need Help?**

Just tell me:
- "Replace all gallery images with new ones named: image1.avif, image2.avif..."
- "Replace `family_1family.avif` with `my-photo.avif`"
- "I've replaced the files, can you verify?"

---

**🎯 Recommended: Use Option 1 (same filenames) - it's the safest!**




