# Odin Project JavaScript Setup

You are helping set up a JavaScript project following The Odin Project curriculum requirements and 2025 best practices.

## Your Task

Set up a complete JavaScript project with:
1. npm initialization
2. Webpack 5 bundler configuration
3. ESLint with modern flat config
4. Prettier code formatter
5. Jest testing framework with Babel for ES modules
6. Proper project structure
7. Starter template files

## Step 1: Verify Environment

First, check that the user is in the correct directory and has Node.js installed:

```bash
node --version
npm --version
pwd
```

Ask the user for the project name if not already provided.

## Step 2: Initialize npm

Create package.json with proper metadata:

```bash
npm init -y
```

## Step 3: Install Dependencies

Install all required packages in one command:

```bash
npm install --save-dev webpack webpack-cli webpack-dev-server webpack-merge html-webpack-plugin style-loader css-loader html-loader eslint @eslint/js globals prettier eslint-config-prettier jest babel-jest @babel/core @babel/preset-env
```

Explain to the user:
- **webpack ecosystem**: Core bundler, CLI, dev server, config merger
- **webpack loaders**: html-webpack-plugin (inject bundles), style-loader & css-loader (CSS), html-loader (HTML templates)
- **eslint ecosystem**: Core linter, recommended config, globals definitions
- **prettier**: Code formatter with ESLint integration
- **jest ecosystem**: Testing framework with Babel for ES module support

## Step 4: Update package.json

Add the following scripts to package.json:

```json
{
  "scripts": {
    "test": "jest",
    "test:watch": "jest --watch",
    "build": "webpack --mode production",
    "dev": "webpack serve --mode development",
    "lint": "eslint .",
    "lint:fix": "eslint . --fix",
    "format": "prettier . --write",
    "format:check": "prettier . --check",
    "deploy": "git subtree push --prefix dist origin gh-pages"
  }
}
```

Use the Edit tool to update the package.json file with these scripts.

## Step 5: Create webpack.config.js

Create a comprehensive Webpack configuration following Odin Project requirements:

```javascript
const path = require("path");
const HtmlWebpackPlugin = require("html-webpack-plugin");

module.exports = {
  mode: "development",
  entry: "./src/index.js",
  output: {
    filename: "main.js",
    path: path.resolve(__dirname, "dist"),
    clean: true,
  },
  devtool: "eval-source-map",
  devServer: {
    watchFiles: ["./src/template.html"],
  },
  plugins: [
    new HtmlWebpackPlugin({
      template: "./src/template.html",
    }),
  ],
  module: {
    rules: [
      {
        test: /\.css$/i,
        use: ["style-loader", "css-loader"],
      },
      {
        test: /\.html$/i,
        loader: "html-loader",
      },
      {
        test: /\.(png|svg|jpg|jpeg|gif)$/i,
        type: "asset/resource",
      },
    ],
  },
};
```

Key features explained:
- **mode**: Set to "development" for better debugging (change to "production" for deployment)
- **entry**: Starting point at `src/index.js`
- **output**: Bundles to `dist/main.js`, cleans dist folder before each build
- **devtool**: Source maps for debugging bundled code
- **devServer**: Watches HTML template for changes
- **HtmlWebpackPlugin**: Auto-injects bundle into HTML
- **Loaders**: Process CSS (order matters: style-loader, then css-loader), HTML templates, and images

## Step 6: Create eslint.config.js

Create modern ESLint flat config (v9+ format):

```javascript
import js from "@eslint/js";
import globals from "globals";

export default [
  js.configs.recommended,
  {
    languageOptions: {
      globals: {
        ...globals.browser,
        ...globals.node,
      },
    },
    rules: {
      "no-unused-vars": "warn",
      "no-undef": "error",
    },
  },
];
```

Features:
- Uses ESLint's recommended rules
- Configured for both browser and Node.js globals
- Custom rules for unused variables (warn) and undefined variables (error)

## Step 7: Create .prettierrc

Create Prettier configuration (using defaults):

```json
{}
```

This empty object uses Prettier's opinionated defaults.

## Step 8: Create .prettierignore

```
# Ignore artifacts:
build
coverage
node_modules
dist
```

## Step 9: Create babel.config.js

Required for Jest to work with ES modules:

```javascript
module.exports = {
  presets: [['@babel/preset-env', { targets: { node: 'current' } }]],
};
```

## Step 10: Create .gitignore

```
node_modules
dist
```

Explanation: These directories are generated and should not be version controlled. Anyone cloning the repo can run `npm install` to restore dependencies and `npm run build` to generate the dist folder.

## Step 11: Create Project Structure

Create the following directory structure:

```
mkdir -p src/modules tests
```

**Note on Test Organization:**

- The `tests/` directory is for unit and integration tests
- You can also place tests alongside source files (e.g., `greeting.test.js` next to `greeting.js`) - common in smaller projects
- The Odin Project uses both approaches
- We'll demonstrate the co-located approach in the example, but you can move tests to the `tests/` directory and mirror the `src/` structure for larger projects

## Step 12: Create src/template.html

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Odin Project</title>
  </head>
  <body>
    <header>
      <h1>My Odin Project</h1>
      <nav>
        <button id="home">Home</button>
        <button id="menu">Menu</button>
        <button id="about">About</button>
      </nav>
    </header>
    <div id="content"></div>
  </body>
</html>
```

## Step 13: Create src/style.css

```css
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: Arial, sans-serif;
  line-height: 1.6;
}

header {
  background-color: #333;
  color: #fff;
  padding: 1rem;
  text-align: center;
}

nav {
  margin-top: 1rem;
}

button {
  margin: 0 0.5rem;
  padding: 0.5rem 1rem;
  cursor: pointer;
  background-color: #555;
  color: #fff;
  border: none;
  border-radius: 4px;
}

button:hover {
  background-color: #777;
}

#content {
  padding: 2rem;
  max-width: 800px;
  margin: 0 auto;
}
```

## Step 14: Create src/modules/greeting.js

Example module demonstrating ES6 exports:

```javascript
export function getGreeting() {
  return "Hello from The Odin Project!";
}

export function createWelcomeMessage() {
  const message = document.createElement("p");
  message.textContent = getGreeting();
  message.style.fontSize = "1.5rem";
  message.style.marginTop = "2rem";
  return message;
}
```

## Step 15: Create src/index.js

Main entry point with ES6 module imports:

```javascript
import "./style.css";
import { createWelcomeMessage } from "./modules/greeting.js";

console.log("Webpack is working!");

// Get the content div
const content = document.getElementById("content");

// Add welcome message
content.appendChild(createWelcomeMessage());

// Add event listeners to navigation buttons
document.getElementById("home").addEventListener("click", () => {
  content.innerHTML = "";
  content.appendChild(createWelcomeMessage());
});

document.getElementById("menu").addEventListener("click", () => {
  content.innerHTML = "<h2>Menu Page</h2><p>Add your menu content here.</p>";
});

document.getElementById("about").addEventListener("click", () => {
  content.innerHTML =
    "<h2>About Page</h2><p>Add your about content here.</p>";
});
```

## Step 16: Create Example Test File

Create `src/modules/greeting.test.js`:

```javascript
import { getGreeting } from "./greeting.js";

test("getGreeting returns correct message", () => {
  expect(getGreeting()).toBe("Hello from The Odin Project!");
});
```

## Step 17: Final Instructions to User

After all files are created, provide these instructions:

---

## Your Odin Project JavaScript setup is complete!

### Project Structure:
```
project-root/
├── src/
│   ├── index.js              # Entry point
│   ├── template.html         # HTML template
│   ├── style.css            # Styles
│   └── modules/
│       ├── greeting.js      # Example module
│       └── greeting.test.js # Example test (co-located)
├── tests/                   # Alternative test location for larger projects
├── node_modules/            # Dependencies (gitignored)
├── dist/                    # Build output (gitignored)
├── package.json
├── webpack.config.js
├── eslint.config.js
├── babel.config.js
├── .prettierrc
├── .prettierignore
└── .gitignore
```

### Available Commands:

- `npm run dev` - Start development server at http://localhost:8080
- `npm run build` - Build for production (outputs to dist/)
- `npm test` - Run Jest tests
- `npm run test:watch` - Run tests in watch mode
- `npm run lint` - Check for linting errors
- `npm run lint:fix` - Auto-fix linting errors
- `npm run format` - Format all files with Prettier
- `npm run format:check` - Check formatting without modifying files
- `npm run deploy` - Deploy to GitHub Pages (requires git repo)

### Next Steps:

1. **Start development server**: Run `npm run dev` and open http://localhost:8080
2. **Try the example**: Click the navigation buttons to see dynamic content loading
3. **Run tests**: Execute `npm test` to see the example test pass
4. **Start building**: Edit files in `src/` - changes will auto-reload in the browser
5. **Add more modules**: Create new files in `src/modules/` and import them

### Key Concepts Demonstrated:

- **ES6 Modules**: Import/export syntax in `greeting.js` and `index.js`
- **Webpack Bundling**: CSS imports, automatic HTML injection
- **DOM Manipulation**: Dynamic content updates on button clicks
- **Testing**: Jest test example for the greeting module
- **Code Quality**: ESLint and Prettier configured and ready

### Odin Project Tips:

- Keep logic separate from DOM manipulation (see how `getGreeting()` is pure)
- Use modules to organize your code
- Test your pure functions (functions that don't interact with the DOM)
- Commit your changes regularly
- Don't commit `node_modules/` or `dist/` folders

Happy coding! 🚀

---

## Important Notes for You (Claude):

- Always create ALL files listed above
- Use the Write tool for each configuration and source file
- Use the Edit tool to update package.json with scripts
- Verify each file is created successfully before moving to the next
- At the end, summarize what was created and provide the "Final Instructions to User" section above
- If the user already has some files (like package.json), read them first and update rather than overwrite
- Be encouraging and educational in your responses
