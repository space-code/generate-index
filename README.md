<h1 align="center" style="margin-top: 0px;">generate-index</h1>

<p align="center">
<a href="https://github.com/space-code/generate-index/blob/main/LICENSE"><img alt="Licence" src="https://img.shields.io/badge/License-MIT-yellow.svg"></a> 
<a href="https://github.com/space-code/generate-index/actions/workflows/ci.yml"><img alt="CI" src="https://github.com/space-code/generate-index/actions/workflows/ci.yml/badge.svg?branch=main"></a>
</p>

## Description

A GitHub Action for automatically generating a beautiful index page for Swift DocC documentation.

## Features

- 🎯 Modern Apple-style design
- 📦 Multi-module support
- 🌐 Responsive layout
- 🚀 Fast and easy setup

## Table of Contents

- [Usage](#usage)
    - [Basic Example](#basic-example)
    - [Single Module](#single-module)
- [Parameters](#parameters)
- [Modules Parameter Format](#modules-parameter-format)
- [Output Structure](#output-structure)
- [DocC Integration](#docc-integration)
- [Communication](#communication)
- [Contributing](#contributing)
- [Lisence](#license)

## Usage

### Basic Example

```
name: Deploy DocC

on:
  push:
    branches: [main]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      
      - name: Generate DocC Index
        uses: space-code/generate-index@v1
        with:
          version: '1.0.0'
          project-name: 'MyAwesomeLibrary'
          project-description: 'Swift library for awesome things'
          modules: |
            [
              {
                "name": "CoreModule",
                "path": "coremodule",
                "description": "Core functionality and base types",
                "badge": "Core"
              },
              {
                "name": "UIModule",
                "path": "uimodule",
                "description": "UI components and helpers",
                "badge": "UI"
              }
            ]
      
      - name: Deploy to GitHub Pages
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./docs
```

### Single module

```
- name: Generate DocC Index
  uses: space-code/generate-index@v1
  with:
    version: '2.0.0'
    project-name: 'SimpleLib'
    project-description: 'A simple Swift library'
    modules: |
      [
        {
          "name": "SimpleLib",
          "path": "simplelib",
          "description": "Main library module"
        }
      ]
```

## Parameters

| Parameter             | Required | Description           | Example                    |
| --------------------- | -------- | --------------------- | -------------------------- |
| `version`             | ✅ Yes    | Documentation version | `1.0.0`                    |
| `project-name`        | ✅ Yes    | Project name          | `MyLibrary`                |
| `project-description` | ✅ Yes    | Project description   | `Swift validation library` |
| `modules`             | ❌ No     | JSON array of modules | See below                  |


## Modules Parameter Format

```
[
  {
    "name": "ModuleName",        // Module name (required)
    "path": "modulepath",        // Lowercase path (required)
    "description": "Description",// Module description (required)
    "badge": "Custom Badge"      // Badge label (optional, defaults to "Module")
  }
]
```

## Output Structure

The Action generates a `docs/index.html` file with the following structure:

```
docs/
└── index.html          # Index page
```

Documentation links follow this pattern:

```
{version}/{ModuleName}/documentation/{modulepath}
```

## DocC Integration

Typical workflow for a Swift project with DocC:

```
name: Documentation

on:
  push:
    branches: [main]
    tags: ['*']

jobs:
  build-docs:
    runs-on: macos-latest
    steps:
      - uses: actions/checkout@v4
      
      - name: Build DocC
        id: build
        uses: space-code/build-docc@main
        with:
          schemes: '["ValidatorCore", "ValidatorUI"]'
          version: ${{ steps.version.outputs.version }}
      
      - name: Generate Index
        uses: space-code/generate-index@v1
        with:
          version: '1.0.0'
          project-name: 'YourProject'
          project-description: 'Your project description'
          modules: |
            [
              {
                "name": "YourTarget",
                "path": "yourtarget",
                "description": "Main module documentation"
              }
            ]
      
      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./docs
```

## Communication

- 🐛 **Found a bug?** [Open an issue](https://github.com/space-code/generate-index/issues/new?template=bug_report.md)
- 💡 **Have a feature request?** [Open an issue](https://github.com/space-code/generate-index/issues/new?template=feature_request.md)
- ❓ **Questions?** [Start a discussion](https://github.com/space-code/generate-index/discussions)
- 🔒 **Security issue?** Email nv3212@gmail.com

## Contributing

Contributions are welcome! Please feel free to submit issues or pull requests.

## Author

**Nikita Vasilev**
- Email: nv3212@gmail.com
- GitHub: [@ns-vasilev](https://github.com/ns-vasilev)

## License

build-docc is released under the MIT license. See [LICENSE](LICENSE) for details.

---

<div align="center">

**[⬆ back to top](#generate-index)**

Made with ❤️ by [space-code](https://github.com/space-code)

</div>