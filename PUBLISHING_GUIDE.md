# Publishing Kodi Log Highlighter to Package Control

## Official Guidelines Reference

This guide follows the official Sublime Text documentation:
https://docs.sublimetext.io/guide/package-control/submitting.html

## Prerequisites Checklist

Before submitting, ensure your package meets these requirements:

- ✓ **Name follows guidelines**: No "Sublime" in name, ASCII only, no special characters
- ✓ **Git repository is clean**: No `.pyc` files, no `package-metadata.json`
- ✓ **Semantic version tag exists**: Create a tag like `1.0.0`
- ✓ **README is comprehensive**: Clear description of purpose and usage
- ✓ **License file exists**: GPL-3.0 license included
- ✓ **No .no-sublime-package file needed**: (only needed for executables/shared libraries)
- ✓ **No default keybindings**: Settings only, no forced keyboard shortcuts
- ✓ **No context menu additions**: Not needed for a syntax package
- ✓ **Settings accessible via menu**: Handled automatically by Sublime

## Step-by-Step Publishing Guide

### 1. Create GitHub Repository

1. Create a new repository: `https://github.com/bossanova808/kodi-log-highlighter`
   
   **Important naming**: The repository name should match your package name (or be similar).

2. Clone it locally:
   ```bash
   git clone https://github.com/bossanova808/kodi-log-highlighter.git
   cd kodi-log-highlighter
   ```

### 2. Set Up Repository Structure

Copy these files to your repository root:

```
kodi-log-highlighter/
├── Kodi.sublime-syntax
├── Kodi Log Highlighter.sublime-settings
├── README.md
├── LICENSE (your GPL-3.0 license)
├── .gitignore
├── messages.json
└── messages/
    └── install.txt
```

**Critical**: The package name in the folder structure must match the `name` field in your `.sublime-syntax` file.

### 3. Create .gitattributes (Optional but Recommended)

To exclude unnecessary files from the package distribution:

```gitattributes
.gitattributes export-ignore
.gitignore export-ignore
*.md export-ignore
```

This keeps images and docs in the repo but out of the installed package.

### 4. Initial Commit and Tag

```bash
git add .
git commit -m "Initial release v1.0.0"
git tag -a 1.0.0 -m "Version 1.0.0 - Initial release"
git push origin main
git push --tags
```

**Important**: The tag must follow [semantic versioning](http://semver.org) (MAJOR.MINOR.PATCH).

### 5. Fork Package Control Channel

1. Go to https://github.com/sublimehq/package_control_channel
2. Click "Fork" in the top right
3. Clone your fork:
   ```bash
   git clone https://github.com/bossanova808/package_control_channel.git
   cd package_control_channel
   ```

### 6. Add Your Package Entry

1. Open or create `repository/k.json`
2. Add your package entry (use the provided `k.json.example` as reference):

```json
{
    "schema_version": "4.0.0",
    "packages": [
        {
            "name": "Kodi Log Highlighter",
            "details": "https://github.com/bossanova808/kodi-log-highlighter",
            "releases": [
                {
                    "sublime_text": ">=4000",
                    "tags": true
                }
            ],
            "labels": ["language syntax", "logs"],
            "readme": "https://raw.githubusercontent.com/bossanova808/kodi-log-highlighter/main/README.md",
            "issues": "https://github.com/bossanova808/kodi-log-highlighter/issues"
        }
    ]
}
```

**Label Guidelines** (from official docs):
- Use "language syntax" for packages providing syntax definitions
- Labels are always lowercase
- Keep labels relevant and minimal

### 7. Test Your JSON

Before submitting, validate your JSON:
```bash
python -m json.tool repository/k.json
```

### 8. Submit Pull Request

1. Commit your changes:
   ```bash
   git add repository/k.json
   git commit -m "Add Kodi Log Highlighter package"
   git push
   ```

2. Go to https://github.com/sublimehq/package_control_channel
3. Click "Pull Requests" → "New Pull Request"
4. Select your fork and branch
5. Create the PR with a clear title: "Add Kodi Log Highlighter"

**Important**: Submit only ONE package per PR.

### 9. Wait for Review

- Reviews are done by volunteers in their spare time
- Typical wait time: a few days to a week
- Respond promptly to any feedback or requested changes
- Tests must pass (automated checks run on your PR)

## Things That Help Get Approved Quickly

From the official guidelines:

✓ **Only maintainers submit**: You must be the package maintainer  
✓ **Valid semver tag**: Must exist before submitting  
✓ **Clear README**: Purpose and usage clearly explained  
✓ **No default keybindings**: Only provide commented examples  
✓ **Settings in menu**: Use standard Sublime Text patterns  
✓ **Proper labels**: Follow the label guidelines above  

## After Approval

Once approved and merged:

1. Package Control will automatically detect your releases via Git tags
2. Users can install via Package Control within 24 hours
3. Future updates: Just create new semver tags - no PR needed!

## Version Management

For future releases:

1. Make your changes
2. Update CHANGELOG in README.md
3. Commit changes
4. Create and push new tag:
   ```bash
   git tag -a 1.1.0 -m "Version 1.1.0 - [brief description]"
   git push --tags
   ```

Package Control automatically detects new tags.

## Repository Best Practices

- Keep a CHANGELOG section in README.md
- Use semantic versioning strictly
- Tag format: `1.0.0` (not `v1.0.0`)
- Respond to issues and PRs promptly
- Test on multiple Sublime Text versions if possible

## Additional Resources

- [Package Control Docs](https://packagecontrol.io/docs)
- [Official Submission Guide](https://docs.sublimetext.io/guide/package-control/submitting.html)
- [Repository JSON Format](https://packagecontrol.io/docs/repository_json)
- [Sublime Text Syntax Guide](https://www.sublimetext.com/docs/syntax.html)

## Troubleshooting

**Q: My package isn't showing up after approval**  
A: Wait 24 hours for Package Control's cache to update

**Q: Can I rename my package later?**  
A: Yes, but follow the [renaming guidelines](https://docs.sublimetext.io/guide/package-control/renaming.html)

**Q: Should I include screenshots?**  
A: Yes! Add them to your README (they won't be in the package itself due to .gitattributes)

**Q: Tests are failing on my PR**  
A: Check the error messages - usually JSON formatting or invalid URLs
