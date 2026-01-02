# VPM - VYL Package Manager v1.0

The official package manager for the VYL programming language.

## Installation

```bash
# Compile VPM
cd vpm/
vyl -c main.vyl

# Install system-wide (optional)
ln -s /FULL/PATH/TO/VPM/EXEC /usr/local/bin/vpm
```

## Usage

### Initialize a New Project

```bash
vpm init my-project
cd my-project
vyl main.vyl -o app
./app 
# or
vyl -c main.vyl
./main.vylo
```

This creates:
- `mod.vinfo` - Package metadata
- `main.vyl` - Hello world template

### Install Packages

```bash
# Install latest version
vpm install http

# Install specific version
vpm install http@1.0.0
```

Packages are installed to `~/.vyl/modules/`

### Search for Packages

```bash
vpm search string
vpm search http
```

Searches the package registry for matching names and descriptions.

### List Installed Packages

```bash
vpm list
```

### Show Package Information

```bash
vpm info stdlib
```

Displays version, author, description, and dependencies.

### Remove a Package

```bash
vpm remove old-package
```

## Package Registry

VPM fetches packages from:
```
https://github.com/New-Tech-Exclusive/VYL-Language/mods
```

### Adding Packages to Registry

1. Create a directory under `mods/your-package/`
2. Add `mod.vinfo`:
   ```
   name=your-package
   version=1.0.0
   author=Your Name
   description=What your package does
   dependencies=
   ```
3. Add `mod.vyl` with your code
4. Update `index.txt` in repository root:
   ```
   your-package - Description for search
   ```
5. Tag releases with `v1.0.0` for version support

## mod.vinfo Format

```
name=my-package
version=1.0.0
author=Your Name
description=Package description
dependencies=stdlib,http
```

- **dependencies**: Comma-separated list (no spaces)
- **version**: Semantic versioning (major.minor.patch)

## Version Pinning

```bash
# Install specific version (uses git tags)
vpm install package@1.0.0

# This resolves to:
# https://.../VYL-Language/v1.0.0/mods/package/mod.vyl
```

Versions must be tagged in the repository as `v1.0.0`, `v2.1.3`, etc.

## Development

VPM is written in VYL and uses:
- `import stdlib` - For file I/O and string operations
- Built-in HTTP support via `HttpDownload()`
- ANSI escape codes for colored output

### File Structure

```
vpm/
├── main.vyl       # VPM source code
├── main.vylo      # Compiled bytecode (optional)
└── README.md      # This file
```

## Troubleshooting

### "Package not found"
- Check package name spelling
- Verify package exists in registry
- Check internet connection

### "Failed to download"
- Ensure GitHub is accessible
- Check if version tag exists for versioned installs
- Verify repository structure

### "Cyclic dependency detected"
- Review your mod.vinfo dependencies
- Remove circular references

## Future Enhancements

- [ ] `vpm update` - Update all packages
- [ ] `vpm publish` - Publish packages from CLI
- [ ] Local `vyl_modules/` support (project-specific)
- [ ] Lockfile generation for reproducible builds
- [ ] Private registry support
- [ ] Package checksums/verification

## Contributing

VPM is part of the VYL Language project. See the [main repository](https://github.com/New-Tech-Exclusive/VYL-Language) for contribution guidelines.

## License

Same as VYL Language (see VYL language repository root)
