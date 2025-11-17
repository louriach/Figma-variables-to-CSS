# Figma variables to CSS

A Figma plugin that enables bidirectional conversion between Figma design tokens (variables) and CSS variables. Export your Figma variables to CSS or import CSS variables back into Figma with support for nested aliases, multiple modes, and collections.

![Plugin Banner](https://img.shields.io/badge/Figma-Plugin-F24E1E?style=for-the-badge&logo=figma&logoColor=white)
![TypeScript](https://img.shields.io/badge/TypeScript-007ACC?style=for-the-badge&logo=typescript&logoColor=white)

---

## ✨ Features

### 🎨 Export to CSS
- **Convert all variables**: Export all Figma variables from every collection
- **Cherry pick collections**: Select specific primitive and semantic collections for targeted exports
- **View all collections**: Browse all local variables in organised tables with visual colour swatches
- **Code syntax support**: Option to use Figma's code syntax for variable names
- **Nested alias support**: Correctly handles multi-level variable aliasing (variables that reference other variables)
- **Multiple export formats**: Copy to clipboard or download as `.css` file

### 📥 Import from CSS
- **Paste CSS**: Import CSS variables from your clipboard
- **Upload CSS files**: Drag and drop or browse for `.css` files
- **Smart type detection**: Automatically determines variable types (COLOR, FLOAT, STRING, BOOLEAN)
- **Alias preservation**: Maintains variable references using `var(--name)` syntax
- **Collection management**: Organises variables into collections based on CSS comments
- **Mode support**: Creates multiple modes within collections for theming

### 🎯 Advanced capabilities
- **Multi-level aliasing**: Handles variables that reference other aliased variables without errors
- **RGB/RGBA support**: Converts colours with alpha transparency
- **Hex colour conversion**: Automatically converts between hex and RGB formats
- **Value type inference**: Detection of variable types from names and values
- **Error handling**: Clear error messages and validation feedback

---

## 🛠️ Tech stack

### Core technologies
- **TypeScript**
- **Figma Plugin API** 
- **HTML/CSS** 
- **JavaScript (ES6+)** 

### Build tools
- **TypeScript Compiler (tsc)** - Compiles TypeScript to JavaScript
- **npm** - Package management and scripts
- **ESLint** - Code quality and consistency

### Key APIs used
- Figma Variables API
- Figma Collections API
- Web File API (for file uploads)
- Clipboard API (for copy functionality)

---

## 📦 Installation

### Option 1: Install from Figma Community (recommended)
1. Visit the [Figma Community page](#) <!-- Add your plugin URL here -->
2. Click "Install"
3. Access via **Plugins → Copy Variables to CSS variables** in Figma

### Option 2: Run locally for development

#### Prerequisites
- [Node.js](https://nodejs.org/) (v14 or higher)
- [npm](https://www.npmjs.com/) (comes with Node.js)
- [Figma Desktop App](https://www.figma.com/downloads/)

#### Setup steps

1. **Clone the repository**
```bash
git clone https://github.com/yourusername/Figma-variables-to-CSS.git
cd Figma-variables-to-CSS
```

2. **Install dependencies**
```bash
npm install
```

3. **Build the plugin**
```bash
npm run build
```

4. **Watch mode for development** (auto-recompile on changes)
```bash
npm run watch
```

5. **Load in Figma**
   - Open Figma Desktop
   - Go to **Plugins → Development → Import plugin from manifest**
   - Browse to the plugin folder and select `manifest.json`
   - The plugin will appear under **Plugins → Development**

---

## 🚀 Usage

### Exporting variables to CSS

#### Method 1: Convert all variables
1. Open the plugin in your Figma file
2. Click the **"Export to CSS"** tab
3. Select **"Convert all variables"**
4. Your collections will be listed automatically
5. *(Optional)* Check **"Use code syntax"** to use Figma's code syntax names
6. Click **"Convert to CSS"**
7. Choose to **Copy CSS** or **Export CSS** as a file

**Output example:**
```css
/* Collection name: Primitives */
/* Mode: Light */
:root {
  --color-primary: #18a0fb;
  --spacing-sm: 8px;
}

/* Collection name: Semantic */
/* Mode: Light */
:root {
  --button-bg: var(--color-primary);
  --card-padding: var(--spacing-sm);
}
```

#### Method 2: Cherry pick collections
1. Navigate to the **"Cherry pick"** tab
2. Select a **Primitive collection** (base design tokens)
3. Select a **Semantic collection** (contextual tokens)
4. Click **"Convert to CSS"**
5. The output will include both collections with proper structure

**Use case:** Perfect for exporting a design system where primitives define base values and semantics reference them.

#### Method 3: View all collections
1. Go to the **"All local collections"** tab
2. Browse tables showing all variables organised by collection
3. Visual colour swatches for colour values
4. View variable aliases and code syntax

### Importing CSS variables to Figma

#### Required CSS format
Your CSS must include special comments to define collections and modes:

```css
/* Collection name: [Your Collection Name] */
/* Mode: [Your Mode Name] */
:root {
  --variable-name: value;
}
```

#### Method 1: Paste CSS
1. Click the **"Import from CSS"** tab
2. Select the **"Paste CSS"** tab
3. Paste your CSS into the textarea
4. Click **"Create Variables"**
5. Variables will be created in your Figma file

#### Method 2: Upload CSS file
1. Click the **"Import from CSS"** tab
2. Select the **"Upload File"** tab
3. Drag and drop a `.css` file or click to browse
4. File validation happens automatically
5. Click **"Create Variables"**

**Example with aliases:**
```css
/* Collection name: Colors */
/* Mode: Light */
:root {
  --red: #ff0000;
  --green: #00ff00;
}

/* Collection name: Theme */
/* Mode: Light */
:root {
  --error-color: var(--red);
  --success-color: var(--green);
}
```

This creates two collections where Theme variables reference Colors variables.

### Working with nested aliases

The plugin fully supports multi-level variable aliasing:

```css
/* Collection name: Level 1 */
/* Mode: Mode 1 */
:root {
  --red: #ff6969;
}

/* Collection name: Second level */
/* Mode: Mode 1 */
:root {
  --color-1: var(--red);           /* First-level alias */
  --color-4: var(--color-1);       /* Second-level alias (nested) */
}
```

Both aliases will be correctly created and maintained in Figma.

---

## 🎨 Features in detail

### Alias handling
- **Single-level aliases**: `--button-color: var(--primary)`
- **Multi-level aliases**: `--btn: var(--button-color)` where `--button-color` itself is an alias
- Prevents `[object Object]` errors in nested references
- Maintains referential integrity across collections

### Colour support
- **Hex colours**: `#ff0000` or `#f00`
- **RGB/RGBA**: `rgb(255, 0, 0)` or `rgba(255, 0, 0, 0.5)`
- **Automatic conversion**: Opaque colours convert to hex, transparent colours remain as `rgba()`

### Type detection
The plugin intelligently determines variable types based on:
- **Variable names**: `color`, `background`, `spacing`, `size`, etc.
- **Value patterns**: Hex codes, numbers with units, plain strings
- **Referenced variables**: Inherits type from the variable being referenced

### Multiple modes
Export and import variables with multiple modes for:
- Light/Dark themes
- Brand variations
- Responsive breakpoints
- Seasonal themes

---

## 🤝 Contributing

Contributions are welcome! Here's how you can help:

1. **Fork the repository**
2. **Create a feature branch**: `git checkout -b feature/amazing-feature`
3. **Make your changes** and commit: `git commit -m 'Add amazing feature'`
4. **Push to the branch**: `git push origin feature/amazing-feature`
5. **Open a pull request**

### Development guidelines
- Write TypeScript with proper type annotations
- Follow existing code style (ESLint configured)
- Test thoroughly in Figma before submitting
- Update documentation for new features

---

## 📝 Scripts

| Command | Description |
|---------|-------------|
| `npm run build` | Compile TypeScript to JavaScript once |
| `npm run watch` | Watch mode - auto-recompile on file changes |
| `npm run lint` | Run ESLint to check code quality |
| `npm run lint:fix` | Automatically fix linting issues |

---

## 🐛 Known issues & limitations

- Variables must use standard naming conventions for accurate type detection
- Very large files (1000+ variables) may take a few seconds to process
- Import feature requires edit permissions (cannot run in Dev Mode)

---

## 📄 License

This project is open source. Feel free to use, modify, and distribute as needed.

---

## 🙏 Acknowledgements

- Built with the [Figma Plugin API](https://www.figma.com/plugin-docs/)
- Inspired by the design systems community
- Thanks to all contributors and users

---

## 📞 Support

- **Issues**: [GitHub Issues](https://github.com/yourusername/Figma-variables-to-CSS/issues)
- **Discussions**: [GitHub Discussions](https://github.com/yourusername/Figma-variables-to-CSS/discussions)

---

## 🔄 Changelog

### Version 1.0.0
- Initial release
- Export variables to CSS
- Import CSS variables to Figma
- Support for nested aliases
- Multiple modes and collections
- Code syntax option
- File upload and paste functionality

---