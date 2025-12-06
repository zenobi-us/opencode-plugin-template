# OpenCode Plugin Template Generator

🎉 Generate a new OpenCode plugin in seconds!

This is a generator repository for creating new [OpenCode](https://opencode.ai) plugins. It provides a starter template with all the scaffolding you need to build powerful OpenCode plugins.

## Quick Start

### 1. Use this template

Click "Use this template" on GitHub or clone it:

```bash
git clone https://github.com/zenobi-us/opencode-plugin-template.git my-plugin
cd my-plugin
```

### 2. Run the generator

```bash
./setup.sh
```

### 3. Answer the prompts

The generator will ask for:

- **Plugin name** - kebab-case identifier (e.g., `my-awesome-plugin`)
- **Description** - What your plugin does
- **Author name** - Your name
- **Author email** - Your email
- **Repository URL** - GitHub repo URL
- **GitHub org/username** - For workflow configuration

### 4. Start developing!

```bash
cd my-plugin
bun install
mise run build
```

## What You Get

After running the generator, you'll have:

- ✅ TypeScript setup with modern tooling
- ✅ ESLint + Prettier configuration
- ✅ GitHub Actions workflows (build, lint, release)
- ✅ OpenCode plugin scaffolding
- ✅ Ready-to-use test setup
- ✅ Clean git history with initial commit

The generator cleans itself up - no template files or setup script left behind!

## Usage

```bash
# Generate a new plugin (interactive prompts)
./setup.sh generate

# Show help
./setup.sh help

# Show version
./setup.sh version
```

## Project Structure

Generated plugins have this structure:

```
my-plugin/
├── src/
│   ├── index.ts          # Plugin entry point
│   ├── version.ts        # Version info
│   └── commands/         # Your plugin commands
├── .github/
│   └── workflows/        # CI/CD workflows
├── package.json          # Dependencies and scripts
├── tsconfig.json         # TypeScript config
└── README.md             # Your plugin's documentation
```

## Development

### Available Scripts

```bash
bun install          # Install dependencies
mise run setup       # Initial setup
mise run build       # Build the plugin
mise run test        # Run tests
mise run lint        # Lint code
mise run lint:fix    # Fix linting issues
mise run format      # Format code with Prettier
mise run pkgjsonlint # Lint package.json
mise run prepare     # Prepare for release
mise run publish     # Publish the plugin
mise run version     # Manage version
```

### Publishing

See [RELEASE.md](template/RELEASE.md) for publishing and release management details.

**TL;DR:** Push single commits to main with [conventional commit format](https://www.conventionalcommits.org/). Release-please will accumulate changes in a release PR. When this release PR is merged, a new minor version is released. Until then, all other commits on main result in patch builds being published.

## Learn More

- [OpenCode Documentation](https://opencode.ai/docs)
- [Plugin Development Guide](https://opencode.ai/docs/plugins)
- [OpenCode GitHub](https://github.com/opencode-ai/opencode)

## License

MIT

## Support

Need help?

- Check the [OpenCode docs](https://opencode.ai/docs)
- Open an issue on [GitHub](https://github.com/zenobi-us/opencode-plugin-template/issues)
- Report bugs at https://github.com/sst/opencode
