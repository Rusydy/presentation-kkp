# KKP Presentation Kiosk

This is a single-page, multi-language presentation website designed to function as an interactive kiosk. It's built with modern, lightweight web technologies to create a smooth, app-like experience without requiring a backend. The project uses **HTMX** for dynamic content loading, **Alpine.js** for simple interactivity, and **Tailwind CSS** for styling.

## ✨ Features

- **Dynamic Slide Loading**: Navigates between presentation slides without full page reloads, thanks to HTMX.
- **Multi-Language Support**: Easily switch between Indonesian (ID), English (EN), and Japanese (JA). The content is managed from a single JavaScript object.
- **Persistent Language Choice**: Remembers the user's selected language using the browser's `localStorage`.
- **Active State Navigation**: The sidebar automatically highlights the currently active slide.
- **URL Hash Routing**: The browser's URL hash updates on navigation (e.g., `#slide-2`), allowing slides to be bookmarked and shared.
- **Fullscreen Mode**: A simple toggle to enter and exit fullscreen mode, perfect for a kiosk display.
- **Fully Static**: No backend or build process required. The entire presentation runs directly in the browser.
- **Modern UI**: Clean and professional design using Tailwind CSS and the Inter font.

---

## 🛠️ Tech Stack

- **HTML5**: The core structure of the presentation.
- **Tailwind CSS**: A utility-first CSS framework for rapid UI development.
- **HTMX**: Enables dynamic content loading directly from HTML attributes.
- **Alpine.js**: A rugged, minimal framework for composing JavaScript behavior in your markup. Used here for the fullscreen toggle.
- **Vanilla JavaScript**: Handles the translation logic and application initialization.

---

## 🚀 Getting Started

This project is a static website. No complex setup is needed.

1. **Clone the repository or download the files.**
2. **Ensure you have an `assets` folder** in the same directory as your `index.html` file, containing the required images:
   - `RAD-mermaid.png`
   - `App-Navigation-mermaid.png`
   - `User-Admin-Flow-mermaid.png`
   - `Class-mermaid.png`
3. **Open the `index.html` file** in any modern web browser.

That's it! The presentation should now be running.

---

## ⚙️ How It Works

### Slide Loading with HTMX

The presentation avoids full page reloads by using HTMX. All slide content is pre-written in hidden `<div>` elements at the bottom of the `index.html` file.

- Each navigation link in the sidebar has `hx-` attributes:

  ```html
  <a
    href="#slide-2"
    hx-get=""
    hx-select="#slide-2"
    hx-target="#slide-content"
    hx-swap="innerHTML"
    hx-push-url="true"
  >
    ...
  </a>
  ```

- **`hx-get`**: When a link is clicked, HTMX makes a GET request to the current page URL (since `hx-get` is empty).
- **`hx-select`**: From the response (the full HTML page), it selects only the content inside the `#slide-2` div.
- **`hx-target`**: It then places this selected content into the `#slide-content` div in the main view.
- **`hx-push-url="true"`**: It updates the browser's URL hash to match the link's `href`.

### Multi-Language Translation

The translation system is powered by a simple JavaScript function.

1. A `translations` object in the `<script>` tag holds all the text content for each language.

   ```javascript
   const translations = {
     en: {
       pageTitle: "Presentation Title",
       // ...
     },
     id: {
       pageTitle: "Judul Presentasi",
       // ...
     },
   };
   ```

2. HTML elements that need translation are tagged with a `data-translate-key` attribute.

   ```html
   <h1 data-translate-key="presentationTitle"></h1>
   ```

3. The `changeLanguage(lang)` function iterates through all elements with this attribute and sets their `innerHTML` to the corresponding value from the `translations` object.
4. This function is called on page load and whenever a language button is clicked. It also runs after every HTMX content swap to ensure new content is translated correctly.
