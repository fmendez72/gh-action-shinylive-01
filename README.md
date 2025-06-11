# Quarto + Shinylive + GitHub Pages Template

A minimal, working template for creating interactive Python dashboards using Quarto, Shinylive, and automated GitHub Pages deployment.

## 🎯 What This Template Provides

- **Interactive Python widgets** running in the browser (no server required)
- **Automated deployment** to GitHub Pages via GitHub Actions
- **Local development** with Quarto preview
- **Zero server costs** - everything runs client-side using WebAssembly
- **Professional dashboard layout** with Quarto theming

## 🚀 Live Demo
See the template in action: **[Live Dashboard](https://fmendez72.github.io/gh-action-shinylive-01)**

## 📋 Prerequisites

### Local Development Requirements
- **RStudio** (recommended) or any text editor
- **Quarto CLI** installed ([Download](https://quarto.org/docs/get-started/))
- **Python environment** with shinylive, matplotlib, pandas, numpy packages
- **Git** for version control

### GitHub Requirements
- **GitHub account**
- **Personal Access Token** with `repo` and `workflow` scopes

## 🛠️ Quick Start: Using This Template

### Step 1: Create Repository from Template

1. **Click "Use this template"** button at the top of this repository
2. **Choose "Create a new repository"**
3. **Name your repository** (e.g., `my-dashboard`)
4. **Make it Public** (required for free GitHub Pages)
5. **Click "Create repository"**

### Step 2: Clone to Your Local Machine

```bash
# Replace YOUR-USERNAME and REPO-NAME with your details
git clone https://github.com/YOUR-USERNAME/REPO-NAME.git
cd REPO-NAME
```

### Step 3: Enable GitHub Pages

1. **Go to your repository** on GitHub
2. **Click Settings** → **Pages**
3. **Under "Source"** select **"GitHub Actions"**
4. **Save** the settings

### Step 4: Test Deployment

```bash
# Make a small change to index.qmd
# Commit and push
git add .
git commit -m "Initial setup"
git push origin main
```

**Your site will be live at:** `https://YOUR-USERNAME.github.io/REPO-NAME`

## 💻 Local Development

### Important: No Real Preview Available

**Key Point:** You cannot truly preview Shinylive dashboards locally. The interactive Python widgets only work on the deployed GitHub Pages site.

### The Reality of Local Development

**Local "preview" limitations:**
- ❌ **No Shinylive interactivity** (sliders, buttons won't work)
- ❌ **No real Python execution** (requires WebAssembly runtime)
- ❌ **No widget functionality** (plots may not display correctly)

**What you can check locally:**
- ✅ Markdown rendering and basic layout
- ✅ Quarto syntax and structure
- ✅ General page organization

### Recommended Development Workflow: Build → Push → Test

**This is the only reliable way to test your changes:**

1. **Edit files** in RStudio or your preferred editor
2. **Build and deploy** immediately:
   ```bash
   git add .
   git commit -m "Describe your changes"
   git push origin main
   ```
3. **Wait 3-5 minutes** for GitHub Actions to complete
4. **Test full functionality** on your live site: `https://YOUR-USERNAME.github.io/REPO-NAME`

### Optional: Local Layout Check Only

If you want to check basic layout and Quarto syntax:

```bash
# Replace /path/to/your/python-env with your actual path
PATH="/path/to/your/python-env/bin:$PATH" quarto render index.qmd
# Actual example:
PATH="/home/fernando/python-env/bin:$PATH" quarto render index.qmd
```

**But remember:** This will show broken widgets and non-functional Python code. Use it only for checking markdown formatting and basic structure.

### Why Preview Doesn't Work

- **Shinylive requires WebAssembly runtime** that's only available in the full deployment
- **Local Quarto preview** doesn't include the complete Shinylive infrastructure
- **Python execution** needs the browser-based Pyodide environment

**Bottom line:** Treat local development as text editing only. Real testing happens on the deployed site.

## 📁 Project Structure

```
your-repo/
├── _quarto.yml                    # Quarto project configuration
├── index.qmd                      # Main dashboard page with Python app
├── .github/workflows/
│   └── publish.yml               # GitHub Actions deployment workflow
├── _extensions/                   # Shinylive extension (auto-generated)
│   └── quarto-ext/shinylive/
├── .gitignore                    # Git exclusions
└── README.md                     # This file
```

## 🔧 Customizing Your Dashboard

### Adding New Python Widgets

Edit `index.qmd` and add new Shinylive code blocks:

````markdown
```{shinylive-python}
#| standalone: true
#| viewerHeight: 400

from shiny import App, render, ui
import matplotlib.pyplot as plt

# Your Python app code here
app_ui = ui.page_fluid(
    ui.h2("My New Widget"),
    # Add UI elements
)

def server(input, output, session):
    # Add server logic
    pass

app = App(app_ui, server)
```
````

### Multiple Pages

Create additional `.qmd` files and update `_quarto.yml`:

```yaml
website:
  navbar:
    left:
      - href: index.qmd
        text: "Dashboard"
      - href: analysis.qmd  
        text: "Analysis"
      - href: about.qmd
        text: "About"
```

### Styling and Themes

Modify `_quarto.yml`:

```yaml
format:
  html:
    theme: [cosmo, custom.scss]  # Add custom styling
    css: styles.css
```

## 🚨 Common Issues and Solutions

### Issue: "Error running 'shinylive' command"

**Solution:** Ensure Python environment is correctly configured and PATH is set:

```bash
# Verify shinylive is installed in your environment
/path/to/your/python-env/bin/shinylive --version

# Use full PATH when running quarto
PATH="/path/to/your/python-env/bin:$PATH" quarto preview index.qmd
```

### Issue: GitHub Actions failing with artifact errors

**Solution:** Ensure you're using the latest action versions in `.github/workflows/publish.yml`:

```yaml
- uses: actions/upload-pages-artifact@v3
- uses: actions/deploy-pages@v4
```

### Issue: Local preview URL not clickable

**Solution:** Manually copy and paste the URL (usually `http://localhost:4019/`) into your browser.

### Issue: Widgets not working locally

**Expected behavior:** Shinylive widgets only work on the deployed site, not in local preview.

## 🔐 Authentication Notes

If you encounter authentication issues when pushing:

1. **Use Personal Access Token** instead of password
2. **Ensure token has `repo` and `workflow` scopes**
3. **Alternative:** Set up SSH keys or use GitHub CLI

## 📚 What's Included in This Template

### Working Python Dashboard
- Interactive sliders and dropdowns
- Real-time plot generation with matplotlib
- Statistical calculations with numpy
- Multiple distribution options

### Automated Deployment
- GitHub Actions workflow
- Automatic Python environment setup
- Quarto rendering and deployment
- No manual server configuration

### Development Ready
- Pre-configured Quarto project
- Shinylive extension installed
- Proper .gitignore settings
- Example styling

## 🎯 Next Steps

### Easy Enhancements
- **Add more plots:** Box plots, scatter plots, heatmaps
- **File upload:** Let users analyze their own CSV files
- **More statistics:** Regression, correlation analysis
- **Professional styling:** Custom themes and layouts

### Advanced Features
- **Multiple pages:** Separate analysis sections
- **Data tables:** Interactive pandas DataFrames  
- **Export functionality:** Download plots and data
- **API integration:** Real-time data sources

## 🤝 Contributing

This template is designed to be:
- **Minimal but complete** - everything needed, nothing extra
- **Actually working** - no missing dependencies or configuration
- **Well-documented** - clear setup and troubleshooting

Feel free to submit issues or improvements!

## 📄 License

MIT License - feel free to use this template for any purpose.

---

## 🔍 Technical Details

### Why This Setup Works

1. **Shinylive** converts Python code to WebAssembly for browser execution
2. **Quarto** provides professional document generation and theming
3. **GitHub Actions** handles Python dependencies and deployment automatically
4. **GitHub Pages** serves the static site with client-side Python execution

### Browser Requirements

- **Modern browser** with WebAssembly support (Chrome, Firefox, Safari, Edge)
- **No plugins required** - everything runs natively in the browser
- **Works offline** after initial load

### Performance Notes

- **First load:** 3-5 seconds (downloads Python runtime)
- **Subsequent loads:** Instant (cached locally)
- **Python execution:** Near-native speed via WebAssembly

This template provides a complete, production-ready foundation for building sophisticated data science dashboards that work anywhere the web does.