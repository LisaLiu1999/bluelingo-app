
# Bluelingo Translation Buddy Web App

Bluelingo Translation Buddy is a web-based language translator widget that utilizes Microsoft Azure Cognitive Services to translate text. The project includes a Node.js backend (server.js) and a frontend composed of index.html, style.css, and script.js. The backend provides RESTful endpoints for text translation and language listing, while the frontend offers a user-friendly interface featuring translation history and multi-language support. 

## Implemented Features 
-	Translates text into one or multiple languages (25+ supported) using Azure Cognitive Services.
-	Frontend can be run locally or via the deployed version on the Render cloud platform, allowing seamless integration.
-	Backend runs on the Render cloud platform but can also be run locally.
-	Maintains translation history with options to view, reuse, and clear previous translations.
-	Offers a responsive design for desktop, tablet, and mobile, with an accessible user interface.
-	Implement robust error handling and user feedback.
-	Includes a Light/Dark mode toggle.
-	Enforces character count and limit.
-	Support accessible tooltips and keyboard navigation.

## Technologies Used
- HTML5, CSS3 (Flexbox, Grid, CSS Variables)
- JavaScript (ES6+)
- [Font Awesome](https://fontawesome.com/) for icons
- Backend API (Node.js/Express, not included in this repo)

## Getting Started

### Prerequisites
- [Node.js](https://nodejs.org/) (for backend API, if running locally)
- Modern web browser


## Setup and Deployment

### Frontend (bluelingo-app)


1. **Clone the repository:**
   ```sh
   git clone https://github.com/LisaLiu1999/bluelingo-app.git
   cd bluelingo-app
   ```

2. **Open `index.html` in a web browser**
   - No build step is required for the frontend.
   - For full translation functionality, ensure the backend API is running and accessible at `https://backend-translator.onrender.com/translate` (or update the API URL in `script.js`).

3. **Deploy the frontend on Render**
   - The static files can be deployed to [Render](https://render.com/) as a static site:
     1. Navigate to the [Render Dashboard](https://dashboard.render.com/) and select **New Static Site**.
     2. Connect the appropriate GitHub repository and select the frontend folder.
     3. Set the build command to `null` (no build needed) and the publish directory to `.` (the root folder).
     4. Deploy the site. After deployment, note the public URL.
   - Ensure the deployed frontend can reach the backend API URL (e.g., `https://backend-translator.onrender.com/translate`).

---

### Backend (backend-translator)


1. **Clone or create the backend repository**
   - Place `server.js` and `package.json` in a separate folder (e.g., `backend_translator`).

2. **Install dependencies:**
   ```sh
   npm install
   ```

3. **Set up environment variables:**
   - Create a `.env` file or set environment variables in the deployment platform:
     ```env
     AZURE_SUBSCRIPTION_KEY=your_azure_subscription_key
     AZURE_REGION=your_azure_region
     AZURE_ENDPOINT=https://api.cognitive.microsofttranslator.com
     PORT=3000
     ```

4. **Run locally:**
   ```sh
   node server.js
   ```
   - The backend will be available at `http://localhost:3000/translate`.

5. **Deploy the backend on Render:**
   - Push the backend code to a GitHub repository.
   - Navigate to the [Render Dashboard](https://dashboard.render.com/) and select **New Web Service**.
   - Connect the GitHub repository and select the backend folder.
   - Set the build command to `npm install` and the start command to `node server.js`.
   - Add the environment variables above in the Render dashboard under **Environment**.
   - Deploy the service. After deployment, note the public URL (e.g., `https://backend-translator.onrender.com`).
   - Update the frontend `API_URL` in `script.js` if needed.

---

## Backend: Microsoft Azure Translator API (Node.js)

This application uses a custom Node.js backend (`backend-translator`) that acts as a proxy to the Microsoft Azure Translator service. The backend is deployed on [Render](https://render.com/).

### Backend Features
- Proxies translation requests to Microsoft Azure Translator
- Supports multiple target languages in a single request
- Exposes `/translate` and `/languages` endpoints

### Environment Variables
The following environment variables must be set in the Render service (or `.env` file for local development):

```
AZURE_SUBSCRIPTION_KEY=your_azure_subscription_key
AZURE_REGION=your_azure_region
AZURE_ENDPOINT=https://api.cognitive.microsofttranslator.com
PORT=3000
```

### Deploying to Render
1. Push the backend code (e.g., `server.js`) to a GitHub repository.
2. Go to [Render Dashboard](https://dashboard.render.com/) and click **New Web Service**.
3. Connect the GitHub repository and select the backend folder.
4. Set the build and start commands (for Node.js):
   - **Build Command:** `npm install`
   - **Start Command:** `node server.js`
5. Add the environment variables above in the Render dashboard under **Environment**.
6. Deploy the service. After deployment, note the public URL (e.g., `https://backend-translator.onrender.com`).
7. Update the frontend `API_URL` in `script.js` if needed.


### Backend API Endpoints

- `POST /translate`
  - Request body:
    ```json
    {
      "text": "Hello world",
      "from": "en",
      "to": ["es", "fr"]
    }
    ```
  - Response (multiple languages):
    ```json
    {
      "translations": [
        { "language": "es", "text": "Hola mundo" },
        { "language": "fr", "text": "Bonjour le monde" }
      ]
    }
    ```
  - Response (single language):
    ```json
    {
      "translation": "Hola mundo",
      "language": "es"
    }
    ```

- `GET /languages`
  - Returns the list of supported languages from Azure.

## Project Structure

```
bluelingo-app/
├── bluelingo.svg      # App logo (SVG)
├── favicon.svg        # Favicon for browser tab (SVG)
├── index.html         # Main HTML file
├── style.css          # App styling (light/dark mode, responsive, custom dropdowns)
├── script.js          # App logic (translation, dropdowns, history, theme)
└── README.md          # Project documentation
```

## Usage

1. **Select the source language** using the custom dropdown on the left.
2. **Select one or more target languages** using the custom dropdown on the right.
3. **Enter text** in the input box.
4. Click the **Translate** button.
5. View translations, copy results, or clear input as needed.
6. Access **translation history** via the history button.
7. Toggle **dark mode** using the sun/moon button in the header.

## Customization

- **Add/Remove Languages:**
  - To add or remove languages, update the `languageNames` object and dropdown options in `script.js` and `index.html`.
- **Change API Endpoint:**
  - To change the API endpoint, edit the `API_URL` variable in `script.js`.
- **Styling:**
  - To modify the appearance, update `style.css` for colors, layout, or component styles.

## Accessibility

- All interactive elements are keyboard accessible.
- Tooltips are provided for action buttons.
- High-contrast dark mode is available for low-light environments.


## Attributions

- Font Awesome. (n.d.). Font Awesome. https://fontawesome.com/
- Microsoft. (n.d.). Translator Text API. https://azure.microsoft.com/en-us/products/ai-services/translator/
- Microsoft. (n.d.). Translator Text API Documentation. Microsoft Azure Cognitive Services. https://learn.microsoft.com/en-us/azure/ai-services/translator/
- Express. (n.d.). Express - Node.js web application framework. https://expressjs.com/
- Dotenv. (n.d.). Dotenv - Loads environment variables from .env. https://github.com/motdotla/dotenv
- Node-fetch. (n.d.). node-fetch - A light-weight module that brings window.fetch to Node.js. https://github.com/node-fetch/node-fetch
- CORS. (n.d.). cors - Node.js CORS middleware. https://github.com/expressjs/cors
- Body-Parser. (n.d.). body-parser - Node.js body parsing middleware. https://github.com/expressjs/body-parser
