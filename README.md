# NYT Best Sellers for TRMNL

This plugin displays the latest New York Times Best Seller lists on your TRMNL e-ink display. It fetches data directly from the NYT Books API and provides a clean, easy-to-read presentation of the current best sellers.

## Features

- Display the top books from any NYT Best Seller list
- Two display options: Book covers or detailed list view
- Configure how many books to display
- Full support for all TRMNL display layouts (full, half horizontal, half vertical, quadrant)
- Proper error handling if API is unavailable or key is invalid
- Clean e-ink optimized design

## Installation

### Prerequisites

1. A [TRMNL BYOS](https://usetrmnl.com/byos) server
2. A free NYT Developer API key with Books API access

### How to Install

1. Download the latest release .zip file from the releases page
2. Log in to your TRMNL BYOS server
3. Go to Plugins > Add Plugin
4. Upload the .zip file
5. Configure with your NYT API key

## Configuration

### Required Settings

- **API Key**: Get a free API key from [NYT Developer Portal](https://developer.nytimes.com/)
  - Create an account
  - Create a new app (any name is fine)
  - Enable the "Books API" for your app
  - Copy the API key

### Optional Settings

- **Book List**: Choose which NYT Best Seller list to display (Fiction, Non-Fiction, etc.)
- **Display**: Choose between "Book Covers" or "Full List" views
- **Number of Books**: Choose how many top books to display (5, 10, or 15)
- **Show Debug Information**: Toggle to enable detailed debugging information (only use when troubleshooting)

## Display Modes

### Book Covers Mode

Displays a grid of book covers with rank indicators. This is ideal for a quick visual overview of what's popular.

### Full List Mode

Displays a more detailed list with book title, author, and description. This provides more context about each book.

## Troubleshooting

### No Data Showing

If no data appears on your display:

1. Verify your API key is correct in the plugin settings
2. Ensure the Books API is enabled for your NYT Developer account
3. Check that you've selected a valid book list category
4. The NYT API may be temporarily unavailable - try again later
5. Enable the debug mode in plugin settings to see detailed API response information

### Debug Mode

The plugin includes a debugging feature that can be enabled through the plugin settings:

1. Go to the plugin configuration page
2. Set "Show Debug Information" to "Yes"
3. Save settings and reload the display

When debug mode is enabled, the plugin will show:

- API response status
- Number of books received
- Current display mode settings
- Raw API response data (truncated)
- Other useful diagnostic information

This information can help identify issues with the API connection, data structure, or plugin configuration. Remember to disable debug mode when finished troubleshooting.

### Missing Book Covers

Some books in the NYT API may not have cover images. In these cases, the plugin will display a fallback with just the book title.

## Development

This plugin was created to provide a reliable, customizable way to display NYT Best Seller data on TRMNL e-ink displays.

### Local Development

For local development:

```bash
# Clone the repository
git clone https://github.com/yourusername/nyt_best_sellers.git

# Install dependencies
cd nyt_best_sellers
bundle install

# Create a .env file with your API key
cp .env.example .env
# Edit the .env file to add your NYT API Key
# The API key is stored in the .env file which is gitignored
# and not checked into source control for security

# Run the development server
./bin/dev
```

### Local Development and Testing

For testing with a local BYOS instance, you can use the packaging script:

```bash
# Create a deployable build artifact for local testing
bin/build
```

This will:

1. Create a build artifact in the `build` directory with the correct structure
2. Include only the necessary files (settings.yml and liquid templates)
3. Name the file according to the current version

You can then upload this zip directly to your BYOS instance without going through the GitHub release process.

**Note:** The local `build` directory is used for development testing, while the GitHub Actions workflow uses a `dist` directory for official releases. This separation helps distinguish between testing builds and official distribution packages.

### Release Process

This plugin uses an automated release process:

1. Make your changes in a feature branch
2. Merge your changes to main
3. Run the version bump script:

```bash
# To increment the patch version (0.0.1 -> 0.0.2)
bin/bump-version patch

# To increment the minor version (0.0.1 -> 0.1.0)
bin/bump-version minor

# To increment the major version (0.0.1 -> 1.0.0)
bin/bump-version major
```

4. Push the changes and tag:

```bash
git push origin main && git push origin v[VERSION]
```

The GitHub Actions workflow will automatically:

- Create a release on GitHub
- Package the plugin (only including necessary files) into the `dist` directory
- Attach the zip file to the release

The resulting .zip file can be downloaded from GitHub Releases and uploaded to your TRMNL BYOS server.

## Environment Variables

For local development, this plugin uses environment variables to store sensitive information like API keys:

1. The `.env` file contains your NYT API key (this file is gitignored)
2. The `.trmnlp.yml` file references this environment variable with `{{ env.NYT_API_KEY }}`
3. When deployed to TRMNL, you'll enter your API key in the plugin settings UI

This approach keeps sensitive data out of source control while making local development easy.

## Acknowledgments

This project was inspired by and borrows concepts from:

- [Stephen Yeargin's NYT Best Sellers plugin](https://github.com/stephenyeargin/trmnl-nyt-best-sellers) - For NYT API implementation approaches and plugin structure
- [Andi4000's Open Meteo Weather plugin](https://github.com/andi4000/trmnl-open-meteo-weather-forecast) - For GitHub Actions release workflow concepts

### AI Assistance

Parts of this project were developed with assistance from AI tools:

- Code structure and debugging support from Anthropic's Claude Sonnet 3.7
- Development workflow optimization and template design

## License

MIT License
