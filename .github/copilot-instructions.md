# JRMS Izstādes - Copilot Instructions

## Project Overview

This is a **static HTML-based virtual exhibition platform** for Jaņa Rozentāla Mākslas Skola (Jāņa Rozentāla Rīgas Art School) student artwork. No build tools or package managers are used—files are served directly.

## Architecture

```
index.html                     # Main entry - links to yearly exhibitions
2025/
  2025fotovideo3k.html         # Gallery index with iframe-based navigation
  [StudentName]/               # Individual student galleries
    index.html                 # A-Frame VR gallery
    atteli/ | att/ | bildes/   # Images (webp, jpg, png, avif)
2025kosmoss/
  index.html                   # Alternative assignment format (PDF + video)
  mikrokosmoss/                # 3D models (.glb files)
```

## Technology Stack

- **A-Frame 1.7.0** (`https://aframe.io/releases/1.7.0/aframe.min.js`) for 3D/VR galleries
- **Pure HTML/CSS/JS** - no frameworks, no build process
- **Language**: Latvian (lang="lv") for UI text

## A-Frame Gallery Pattern

Student galleries use this standard structure:

```html
<a-scene>
  <a-entity camera look-controls wasd-controls="acceleration: 10" position="0 1.6 0"></a-entity>
  <a-sky src="atteli/background.webp"></a-sky>
  
  <!-- Artwork planes -->
  <a-plane position="x y z" src="atteli/image.webp" material="shader: flat"></a-plane>
  
  <!-- Decorative elements with transparency -->
  <a-plane src="atteli/element.png" transparent="true" material="side: double"></a-plane>
  
  <!-- Lighting -->
  <a-entity light="type: spot; intensity: 5; angle: 45"></a-entity>
</a-scene>
```

## Key Conventions

1. **Image assets**: Prefer `.webp` format; also support `.jpg`, `.png`, `.avif`
2. **Asset folders**: Named `atteli/`, `att/`, `bildes/`, or `Attēli/` (inconsistent - match existing folder)
3. **Student folder naming**: `FirstNameLastName/` (CamelCase, no spaces, Latvian chars removed)
4. **Nested assignments**: Some students use `1uzd/`, `1_uzd/`, or other subfolder structures
5. **Floor planes**: Use `rotation="-90 0 0"` with `width="4" height="4"`

## Navigation System (2025fotovideo3k.html)

- **Iframe embedding**: Galleries load inside `#galleryFrame`
- **Keyboard shortcuts**: `R` = random gallery, `H` = home, `←/→` = prev/next
- **Bottom nav bar**: Appears when viewing embedded gallery
- **Author display**: Fixed header shows current student name

## When Adding New Students

1. Create folder: `2025/StudentName/`
2. Add `index.html` with A-Frame scene
3. Add images to `atteli/` subfolder
4. Update `2025fotovideo3k.html`:
   - Add to `galleries` array in JavaScript
   - Add to `authorNames` object mapping
   - Add buttons to both `#galleryGrid` and `#bottomNav`

## File Naming

- Avoid spaces in paths (use `1uzd` not `1 uzd`) - some legacy paths have spaces
- Use lowercase for new folders
- Images: descriptive names like `glezna_1.webp`, `background.webp`

## Testing

Open `index.html` directly in browser or use local server:
```bash
python3 -m http.server 8000
```
