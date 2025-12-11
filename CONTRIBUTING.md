# CONTRIBUTING.md

# Contributing to Defensible PCI DSS Frameworks

Thank you for your interest in improving these frameworks! This document provides guidelines for contributing.

## Types of Contributions

We welcome several types of contributions:

### 1. Framework Improvements

- Additional real-world breach examples with citations
- Updated implementation timelines based on actual experience
- Additional metrics and measurement approaches
- Clarifications to technical content

### 2. New Framework Chapters

- Additional threat-based frameworks following the established pattern
- Cross-framework integration guidance
- Industry-specific adaptations (retail, healthcare, financial services)

### 3. Documentation Enhancements

- Improved diagrams and visualizations
- Additional use cases and examples
- Better cross-references between frameworks
- Corrections to PCI DSS requirement mappings

### 4. Technical Corrections

- Fixing broken links or citations
- Correcting technical inaccuracies
- Updating requirement numbers if PCI DSS evolves

## Submission Guidelines

### Before You Submit

1. **Check existing issues and pull requests** to avoid duplicate work
2. **Read the existing frameworks** to understand the style and structure
3. **Ensure accuracy** - all claims should be factual and, where possible, cited

### Making a Contribution

1. **Fork the repository**
2. **Create a feature branch** (`git checkout -b improve-phishing-framework`)
3. **Make your changes** following our style guide
4. **Test your changes** - ensure all links work and Markdown renders correctly
5. **Commit with a clear message** describing what and why
6. **Submit a pull request** with detailed description

### Style Guide

**Markdown formatting:**

- Use ATX-style headings (`#` for H1, `##` for H2, etc.)
- Wrap lines at 120 characters for better diff viewing
- Use bold for emphasis on first use of key terms
- Use code blocks with language hints for better syntax highlighting

**Framework structure (when adding new frameworks):**

- Start with real-world breach example
- Include defense architecture with layers
- Provide use cases for each layer
- Add implementation sequence with timelines
- Include measurable metrics
- Map to specific PCI DSS requirements

**Technical accuracy:**

- Cite sources for breach examples and statistics
- Use current PCI DSS v4.0.1 requirement numbers
- Prefer authoritative sources (NIST, SANS, vendor documentation)
- When describing tools or technologies, use current versions

**Writing style:**

- Use active voice
- Write for a technical security audience
- Be specific rather than generic ("Deploy TLS 1.2+" not "Use encryption")
- Explain the "why" not just the "what"

### Pull Request Process

1. **PR description should include:**
    - What you changed
    - Why you made the change
    - How you tested it (if applicable)
    - References to related issues
2. **Review process:**
    - Maintainers will review within 7 days
    - Feedback will be provided for revisions
    - Approved PRs will be merged to main branch
    - Contributors will be credited in [CHANGELOG.md](http://CHANGELOG.md)
3. **After merge:**
    - Your contribution will appear in the next release
    - You'll be added to the contributors list

## Framework Addition Template

When proposing a new framework chapter, use this template:

```markdown
# [Framework Name]: [Descriptive Subtitle]

## Real-World [Attack Type] Examples
[Specific breach example with date, organization, impact]

## Defense Architecture
[Overview of layered defense approach]

### Layer 1: [Control Name] (PCI DSS X.X)
[Description, use case, real-world example]

### Layer 2: [Control Name] (PCI DSS X.X)
[Description, use case, real-world example]

[Continue for 3-5 layers]

## Implementation Sequence
1. [Action] within [timeframe] ([purpose])
2. [Action] within [timeframe] ([purpose])
[Continue for 5-7 steps]

## Metrics That Matter
- **[Metric name]:** Target [value] with [measurement approach]
[Continue for 4-6 metrics]

## [Closing section tying framework to overall defense strategy]
```

## Questions?

If you have questions about contributing:

- Open an issue with the "question" label
- Check existing issues for similar questions
- Review the main README for project goals and scope

## Code of Conduct

This project follows a simple code of conduct:

- Be respectful and professional
- Focus on technical merit
- Assume good intentions
- Help make the frameworks better for everyone

## Recognition

Contributors will be recognized in:

- [CHANGELOG.md](http://CHANGELOG.md) for each release
- Contributors section of [README.md](http://README.md)
- Git commit history

Significant contributions may warrant co-authorship credit.

## License

By contributing, you agree that your contributions will be licensed under the MIT License.