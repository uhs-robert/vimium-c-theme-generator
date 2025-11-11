<p align="center">
  <img
    src="https://cdn.jsdelivr.net/gh/twitter/twemoji@14.0.2/assets/svg/1f3a8.svg"
    width="128" height="128" alt="Oasis emoji" />
</p>
<h1 align="center">Vimium-C Theme Generator</h1>

<p align="center">
  <a href="https://github.com/uhs-robert/vimium-c-theme-generator/stargazers"><img src="https://img.shields.io/github/stars/uhs-robert/vimium-c-theme-generator?colorA=192330&colorB=skyblue&style=for-the-badge"></a>
  <a href="https://github.com/uhs-robert/vimium-c-theme-generator/issues"><img src="https://img.shields.io/github/issues/uhs-robert/vimium-c-theme-generator?colorA=192330&colorB=khaki&style=for-the-badge"></a>
  <a href="https://github.com/uhs-robert/vimium-c-theme-generator/contributors"><img src="https://img.shields.io/github/contributors/uhs-robert/vimium-c-theme-generator?colorA=192330&colorB=8FD1C7&style=for-the-badge"></a>
  <a href="https://github.com/uhs-robert/vimium-c-theme-generator/network/members"><img src="https://img.shields.io/github/forks/uhs-robert/vimium-c-theme-generator?colorA=192330&colorB=C28EFF&style=for-the-badge"></a>
</p>

<p align="center">
A simple Ruby-based CLI tool to generate custom CSS themes for the <a href="https://github.com/gdh1995/vimium-c">Vimium-C browser extension</a>.
</p>

## ✅ Requirements

- **Ruby** (pre-installed on macOS and most Linux distributions)
  - **Check:** `ruby --version`
  - **Install if needed:**
    - Windows: [rubyinstaller.org](https://rubyinstaller.org/)
    - macOS: `brew install ruby`
    - Linux: `sudo apt/dnf/pacman install ruby`

## 🚀 Usage

### 🤖 Interactive Mode (Recommended)

```bash
ruby generate_theme.rb
```

You'll be prompted to select:

1. A day theme (light themes shown first)
2. A night theme (dark themes shown first)

> [!TIP]
> Each selection includes a final option to "Use a dark/light theme instead" to bypass the day/night recommendations.
> (e.g., use dark themes for both day and night or vice-versa).

### ⌨️ CLI Mode

```bash
ruby generate_theme.rb --day <day_theme> --night <night_theme>
```

**Options:**

- `-d, --day THEME` - Day theme name
- `-n, --night THEME` - Night theme name
- `-l, --list` - List all available themes
- `-h, --help` - Show help

> [!TIP]
> Run `ruby generate_theme.rb --list` to see all available theme names.

## 📄 Output

Generated CSS files are saved to `output/vimiumc-{night}-{day}.css`

Example: If you select "lagoon" for night and "day" for day, the output will be `output/vimiumc-lagoon-day.css`

## 📥 Importing into Vimium-C

1. Generate your theme using the steps above
2. Copy the entire CSS content from the generated file
3. Open Vimium-C settings in your browser:
   - **Chrome/Edge**: `chrome://extensions/` → Vimium C → Options
   - **Firefox**: `about:addons` → Vimium C → Preferences
4. Paste the CSS into the `Custom CSS for Vimium C UI` section
5. Save settings

> [!TIP]
> The extension will automatically parse and apply all sections (HUD, Vomnibar, Find Mode).

## ✏️ Customizing the CSS Template

Feel free to [edit the template here](./vimium-c.css.erb), it's just CSS.

### 💡 Tips and Tricks

1. Use the [Vimium-C Wiki](https://github.com/gdh1995/vimium-c/wiki/Style-the-UI-of-Vimium-C-using-custom-CSS) to learn how CSS is applied in sections
2. You can view the html and elements of `vimium-c` by running commands from the settings page of the extension and using your browser's inspect window
3. Have fun!

## ✨ Adding Your Own Themes

You can easily create custom themes by adding your own color palettes! The included themes are from the [oasis neovim theme pack](https://github.com/uhs-robert/oasis.nvim) and serve as great references.

### 📋 Steps to Add a Theme

1. **Create a theme file**: Add a new `.json` file to the [mappings](./mappings/) directory
   - Use any existing theme (e.g., [oasis_lagoon.json](./mappings/oasis_lagoon.json)) as a template
   - Define all required color keys (see Color Key Reference below)
   - Set `name`, `display_name`, and `is_light` metadata

2. **Register the theme**: Update [index.json](./mappings/index.json)
   - Add your theme to either `light_themes` or `dark_themes` array
   - Include the `id` (filename without `.json`) and `name` (display name)

3. **Use your theme**: Run the generator and your new theme will appear in the selection menu!

### 📦 Theme File Structure

```json
{
  "name": "my_theme",
  "display_name": "My Custom Theme",
  "is_light": false,
  "bg_core": "#1a1b26",
  "bg_mantle": "#16161e",
  "bg_surface": "#24283b",
  "fg": "#c0caf5",
  "link": "#7aa2f7",
  "border": "#3b4261",
  "primary": "#bb9af7",
  "hover_primary": "#c0aff7",
  "secondary": "#7dcfff",
  "title_match": "#ff9e64",
  "link_match": "#f7768e"
}
```

### 🔑 Color Key Reference

**Background Hierarchy** (darkest → lightest for dark themes, lightest → darkest for light themes):

- `bg_core` - Base background (deepest layer)
- `bg_mantle` - Secondary background (middle layer)
- `bg_surface` - Surface background (top layer, for elevated elements)

**Foreground Colors**:

- `fg` - Primary text color
- `link` - Link text color
- `border` - Border and divider color

**Accent Colors**:

- `primary` - Primary accent color
- `hover_primary` - Hover color for primary accent
- `secondary` - Secondary accent color

**Match Highlighting**:

- `title_match` - Color for matched text in titles
- `link_match` - Color for matched text in links

**Metadata**:

- `name` - Internal theme identifier (e.g., "my_theme")
- `display_name` - User-facing name (e.g., "My Custom Theme")
- `is_light` - Boolean indicating if this is a light theme
