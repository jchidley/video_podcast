# Licensing Implementation Plan

## Overview
Adopting a dual-licensing approach inspired by Rust and permissive content licensing inspired by creators like Nam Tao.

## Code Licensing (Apache 2.0 / MIT Dual License)

### Why Dual License?
- **Apache 2.0**: Provides patent protection and explicit grant of patent rights
- **MIT**: Simple, permissive, widely compatible
- **User Choice**: Developers can choose whichever suits their project

### Implementation Steps

#### 1. Create License Files
```bash
# In project root:
LICENSE-APACHE   # Full Apache 2.0 license text
LICENSE-MIT      # Full MIT license text
README.md        # Must mention dual licensing
```

#### 2. File Headers Template
```rust
// SPDX-License-Identifier: Apache-2.0 OR MIT
// Copyright (c) 2025 [Your Name]
// See LICENSE-APACHE and LICENSE-MIT files for details
```

#### 3. Package Metadata
For any published packages:
```toml
[package]
license = "Apache-2.0 OR MIT"
license-file = ["LICENSE-APACHE", "LICENSE-MIT"]
```

## Content Licensing (CC BY 4.0)

### Applies To:
- Video files
- Audio podcasts
- Graphics and thumbnails
- Documentation (non-code)
- Show notes and transcripts

### Implementation Steps

#### 1. License Notice in Content
**Video**: Add to description and credits
```
This video is licensed under Creative Commons Attribution 4.0 International (CC BY 4.0)
https://creativecommons.org/licenses/by/4.0/
```

**Audio**: Include in show notes and spoken credits

#### 2. Metadata Embedding
- Use tools to embed license metadata in files
- Include attribution requirements
- Add license URL

## Attribution Tracking System

### 1. Create ATTRIBUTIONS.md
Track all external content used:
```markdown
# Attributions

## Images
- [Image Name] by [Creator] - [Source URL] - [License]

## Music
- [Track Name] by [Artist] - [Source URL] - [License]

## Code Snippets
- [Description] by [Author] - [Source URL] - [License]
```

### 2. Attribution Database
Consider JSON/YAML for automation:
```yaml
attributions:
  - type: image
    title: "Background Pattern"
    author: "Jane Doe"
    source: "https://example.com/pattern"
    license: "CC BY 4.0"
    modifications: "Resized and color adjusted"
```

## Content Templates

### 1. Video Template
```
[Video Content]

---
Credits:
Created by: [Your Name]
License: CC BY 4.0 (https://creativecommons.org/licenses/by/4.0/)

Attributions:
[List any content used]

Source files available at: [Repository URL]
```

### 2. Repository Structure
```
/video_podcast/
├── LICENSE-APACHE
├── LICENSE-MIT
├── LICENSE-CC-BY-4.0
├── ATTRIBUTIONS.md
├── CONTRIBUTING.md
├── code/              # Apache/MIT licensed
│   └── [headers]
├── content/           # CC BY 4.0 licensed
│   ├── videos/
│   ├── audio/
│   └── graphics/
└── third-party/       # Tracked attributions
```

## Automation Tools

### 1. License Header Checker
Script to verify all code files have proper headers

### 2. Attribution Generator
Tool to generate attribution text from database

### 3. Metadata Injector
Automated license metadata for media files

## Compliance Workflow

### Pre-Release Checklist
- [ ] All code files have license headers
- [ ] LICENSE files are present and correct
- [ ] External content is properly attributed
- [ ] Content includes license notices
- [ ] Metadata is embedded in media files
- [ ] CONTRIBUTING.md explains licensing

### Regular Audits
- Monthly: Check for missing attributions
- Quarterly: Verify license compatibility
- Yearly: Update license versions if needed

## Quick Start Actions

1. **Today**: Create LICENSE-MIT and LICENSE-APACHE files
2. **This Week**: Set up attribution tracking
3. **First Content**: Include proper notices
4. **First Code**: Add license headers
5. **First Release**: Complete compliance checklist