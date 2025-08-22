# Kiosk Presentation DPR RI

This project is a modern, web-based presentation system designed for a kiosk environment at the DPR RI. It's built as a single-page application (SPA) using a combination of HTML, Tailwind CSS, and JavaScript, with HTMX handling the dynamic content loading for a smooth, app-like experience.

## ✨ Key Features

- **Seamless Slide Navigation**: Utilizes HTMX to load presentation slides dynamically without requiring a full page reload, providing a fast and fluid user experience.

- **Multilingual Support**: A robust, built-in translation system allows users to switch between Indonesian, English, and Japanese on the fly. The selected language is saved in the browser's local storage for persistence.

- **Immersive Fullscreen Mode**: Includes a fullscreen toggle to allow the presentation to occupy the entire screen, perfect for a kiosk setting.

- **Modern & Responsive UI**: Styled with Tailwind CSS for a clean, professional, and responsive interface that adapts well to different screen sizes.

## 🛠️ Tech Stack

- **Frontend**: HTML5, Tailwind CSS, JavaScript (ES6+)

- **Dynamic Content**: HTMX

## 🚀 How It Works

The application is architected as a single `index.html` file to keep it simple and portable.

1. **Content Loading**: All slide content is stored in a hidden `<div>` within the `index.html` file. The sidebar navigation links use HTMX attributes (hx-get, hx-select, hx-target) to fetch the corresponding slide's HTML from this hidden container and inject it into the main content area.

2. **URL & State Management**: HTMX's hx-push-url="true" attribute updates the URL hash (e.g., #slide-2) whenever a new slide is loaded. A `hashchange` event listener in the JavaScript code detects this change and calls the setActiveLink() function to update the visual focus in the sidebar navigation.

3. **Translation System**:

- All translatable text is stored in a translations object in the main script.

- HTML elements that need translation are marked with a data-translate-key attribute.

- The `changeLanguage(lang)` function iterates through these elements and updates their content based on the selected language.

## 📂 Setup and Usage

No complex build process is required.

1. Clone or download the repository.

2. Serve the `index.html` file. You can use a simple local server for this. If you have Python installed, you can run:

```bash
python -m http.server
```

or if you have Node.js installed, you can use a package like `http-server`:

```bash
npx http-server
```

Open the provided URL (e.g., `http://localhost:8000`) in your web browser.
