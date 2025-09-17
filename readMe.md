# CoTeX

CoTeX is a developer-focused note-taking application that seamlessly integrates with GitHub repositories, featuring a powerful markdown editor with LaTeX math support, allowing developers to create, organize, and synchronize documentation directly within their project workflows.

## Key Features

- **GitHub Integration**: Real-time sync with GitHub repositories
- **Advanced Markdown Editor**: Full markdown support with mathematical notation using LaTeX/KaTeX
- **Local File Management**: Manage files locally with cloud synchronization capabilities
- **Desktop Application**: Built with Electron and React for cross-platform compatibility
- **Developer-Focused**: Specifically designed for developers who need to document code and technical concepts

## Technical Stack

- **Frontend**: React 19.1.1 with TypeScript
- **Desktop Framework**: Electron 37.2.4
- **Editor**: TipTap with markdown and math extensions
- **Styling**: Tailwind CSS
- **Math Rendering**: KaTeX
- **Database**: Supabase integration

## Installation & Usage

CoTeX is distributed as a desktop application for macOS, Windows, and Linux platforms. Download the appropriate installer for your operating system from the releases section.

### System Requirements

- **macOS**: macOS 10.14 or later

## Development

This application is built using:
- React frontend (`app/` directory)
- Electron main process (`electron/` directory)
- Cross-platform build system using electron-builder


## [Backend](Backend.md)

### License

All packaged builds are © 2025 Brandon Garate.
Distributed binaries are for personal or team use only. Please see the main CoTeX repository for source code licensing terms.

### Support

For issues, feature requests, or contributions, please visit [CoTeX.md/Contact](https://cotex-md.netlify.app/contact)
