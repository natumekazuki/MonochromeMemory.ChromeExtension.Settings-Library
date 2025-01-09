# MonochromeMemory Chrome Extension Settings Library

A reusable Svelte-based settings library designed for Chrome extensions and other projects. This library provides a dynamic settings UI and integrates with Chrome's `chrome.storage.sync` API for data persistence.

## Features

- **Dynamic Settings UI**: Generate forms dynamically based on a JSON configuration.
- **Chrome Storage Integration**: Save and retrieve settings using Chrome's `chrome.storage.sync`.
- **Customizable**: Supports toggles, text inputs, and dropdowns, with support for defaults.

## Installation

Clone the repository or install via npm (coming soon):

```bash
npm install monochrome-memory-chrome-extension-settings-library
```

## Usage

1. **Add the Library to Your Project**

Import the `Settings` component into your Svelte application:

```javascript
import Settings from "monochrome-memory-chrome-extension-settings-library";
```

2. **Provide a Configuration File**

Create a `settings.json` file in your project directory. Example:

```json
[
  {
    "key": "theme",
    "type": "select",
    "label": "テーマ",
    "options": ["light", "dark"],
    "default": "light"
  },
  {
    "key": "notifications",
    "type": "toggle",
    "label": "通知を有効にする",
    "default": true
  },
  {
    "key": "username",
    "type": "text",
    "label": "ユーザー名",
    "default": ""
  }
]
```

3. **Embed the Component**

Embed the `Settings` component in your Svelte application and pass the `configUrl` if needed:

```svelte
<script>
  import Settings from "monochrome-memory-chrome-extension-settings-library";
</script>

<main>
  <h1>設定</h1>
  <Settings configUrl="./settings.json" />
</main>

<style>
  h1 {
    text-align: center;
  }
</style>
```

4. **Build Your Application**

Ensure you build your Svelte application using a tool like Vite or Rollup.

## Configuration Options

- **`key`**: A unique identifier for the setting.
- **`type`**: The input type. Supports `toggle`, `text`, and `select`.
- **`label`**: The label displayed in the UI.
- **`options`** (for `select`): Array of selectable values.
- **`default`**: The default value.

## File Structure

```plaintext
monochrome-memory-chrome-extension-settings/
├── src/
│   ├── components/
│   │   └── Settings.svelte  # Main component
│   ├── utils/
│   │   └── storage.js       # Chrome Storage helper
├── package.json             # npm package metadata
├── README.md                # Usage documentation
├── LICENSE                  # License information
```

## Example Configuration

This example configuration creates a settings UI with:

- A dropdown for selecting a theme.
- A toggle for enabling notifications.
- A text input for a username.

```json
[
  {
    "key": "theme",
    "type": "select",
    "label": "テーマ",
    "options": ["light", "dark"],
    "default": "light"
  },
  {
    "key": "notifications",
    "type": "toggle",
    "label": "通知を有効にする",
    "default": true
  },
  {
    "key": "username",
    "type": "text",
    "label": "ユーザー名",
    "default": ""
  }
]
```

## License

This project is licensed under the MIT License. See the [LICENSE](./LICENSE) file for details.
