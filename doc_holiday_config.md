# .doc.holiday/config
 
The `.doc.holiday/config` file is a configuration file used by the Sandgarden AI documentation system to control which files from a GitHub repository should be indexed and made available for AI-powered documentation generation and updates.
 
## Purpose
 
The `.doc.holiday/config` file serves two main purposes:
 
1. **File Allowlist**: Defines which files in the repository should be included in the AI documentation system's knowledge base
2. **Style Guide Reference**: Optionally specifies a style guide URL or content that the AI should follow when generating documentation
 
## File Location
 
The configuration file must be placed at the root of your repository as:
 
```
.doc.holiday/config
```
 
## File Format Support
 
The `.doc.holiday/config` file supports three different formats:
 
### 1. TOML Format (Recommended)
 
```toml
StyleGuide = "https://docs.google.com/document/d/your-style-guide-id"
Include = [
   "*.md",
   "docs/**/*.md",
   "README.md",
   "!docs/deprecated/*.md" # exclude these files
]
```
 
### 2. JSON Format
 
```json
{
 "styleGuide": "https://docs.google.com/document/d/your-style-guide-id",
 "include": ["*.md", "docs/**/*.md", "README.md", "!docs/deprecated/*.md"]
}
```
 
## Configuration Fields
 
### StyleGuide
 
- **Type**: String
- **Required**: No
- **Description**: URL or content reference for the style guide that the AI should follow when generating documentation
- **Supported URLs**:
 - Google Docs URLs (e.g., `https://docs.google.com/document/d/...`)
 - Notion page URLs (e.g., `https://www.notion.so/...`)
 - Raw content (inline style guide text)
 
**Example with inline style guide:**
 
```toml
StyleGuide = """
# Documentation Style Guide
 
## Writing Guidelines
- Use clear, concise language
- Include code examples where appropriate
- Use consistent formatting for headers and lists
- Always include a brief description for new features
 
## Code Examples
- Use syntax highlighting
- Include comments for complex logic
- Show both input and expected output
 
## Structure
- Start with an overview
- Include step-by-step instructions
- End with troubleshooting tips
"""
```
 
### Include
 
- **Type**: Array of strings
- **Required**: Yes (if no include patterns are found, the system will skip HEAD metadata scanning)
- **Description**: List of file patterns to include in the AI documentation system
 
## File Pattern Syntax
 
The `Include` field supports glob-like patterns with the following features:
 
### Match Patterns
 
- `*.md` - All markdown files in the current directory
- `README.md` - Specific file
- `docs/*.md` - All markdown files in the `docs` directory
- `**/*.md` - All markdown files in any subdirectory
- `docs/**/*.md` - All markdown files in the `docs` directory and its subdirectories
 
### Negation Patterns
 
- `!docs/deprecated/*.md` - Exclude all markdown files in `docs/deprecated/`
- `!*.tmp.md` - Exclude temporary markdown files
 
### Pattern Matching Rules
 
1. Patterns are processed in order
2. Later patterns can override earlier ones
3. Negation patterns (starting with `!`) exclude matching files
4. Non-negation patterns include matching files
5. If no pattern matches a file, it is excluded by default
 
## Examples
 
### Minimal Configuration
 
```toml
Include = ["*.md"]
```
 
### Comprehensive Documentation Setup
 
```toml
StyleGuide = "https://docs.google.com/document/d/1ABC123DEF456GHI789JKL"
Include = [
   "README.md",
   "docs/**/*.md",
   "*.md",
   "!docs/deprecated/*.md",
   "!docs/archive/*.md"
]
```
 
### API Documentation Focus
 
```toml
StyleGuide = "https://www.notion.so/API-Style-Guide-1234567890abcdef"
Include = [
   "api/**/*.md",
   "docs/api/*.md",
   "swagger/*.yaml",
   "swagger/*.json"
]
```
 
## Best Practices
 
1. **Be Specific**: Use precise patterns to avoid indexing unnecessary files
2. **Use Negation**: Exclude temporary, deprecated, or private files
3. **Include Style Guide**: Provide a style guide for consistent AI-generated content
