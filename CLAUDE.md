# React Native Guides & Tutorials Branch

## Purpose

This branch (`claude/react-native-guide-*`) is dedicated to creating **educational content** - guides, tutorials, and documentation for React Native development.

## Content Guidelines

### Writing Style

- **Clarity first**: Explain concepts from first principles
- **Target audience**: Developers familiar with React/JavaScript but new to React Native
- **Structure**: Use progressive disclosure - simple concepts first, then complexity
- **Examples**: Include concrete code examples for every major concept
- **Comparisons**: Show React Native vs Web React when explaining differences

### Content Requirements

- **Background context**: Always explain "why" before "how"
- **Prerequisites**: List what readers should know beforehand
- **Platform differences**: Note iOS/Android differences when relevant
- **Common pitfalls**: Include troubleshooting and common mistakes
- **Best practices**: Reference official documentation and 2025 standards

### File Organization

```
guides/
  ├── getting-started/
  ├── core-concepts/
  ├── navigation/
  ├── styling/
  ├── platform-apis/
  └── deployment/
```

## Writing Best Practices

- Use clear section headers (##, ###)
- Code blocks with language tags (```typescript, ```bash)
- Tables for comparisons
- Callout boxes for important notes
- Working, tested code examples
- Links to official docs when appropriate

## Quality Standards

### Before Committing

- [ ] Technical accuracy verified
- [ ] Code examples tested (when applicable)
- [ ] No broken links
- [ ] Proper markdown formatting
- [ ] Spell check completed

### Code Example Format

```typescript
// ✅ Good - Clear, commented, complete
import { View, Text } from 'react-native';

export default function HelloWorld() {
  // Component renders native View and Text
  return (
    <View>
      <Text>Hello, React Native!</Text>
    </View>
  );
}
```

## Tone

- Professional but friendly
- Objective and factual
- Avoid marketing language or excessive superlatives
- Acknowledge tradeoffs and limitations
- Current as of 2025 standards

## Research Requirements

- Cross-reference official React Native docs
- Verify with Expo documentation when relevant
- Check current community best practices
- Note version-specific features
- Include deprecation warnings when needed

## Commands

```bash
# Verify markdown formatting
npx markdownlint-cli2 "**/*.md"

# Check for broken links (if tools available)
npx markdown-link-check guides/**/*.md
```

## Repository Etiquette

- Descriptive commit messages: "Add navigation guide with React Navigation examples"
- One guide per commit when possible
- Push to branch: `claude/react-native-guide-015KyrBQYiQQkGTSPvnZvoN5`
- No pushing to main without PR review

---

**IMPORTANT**: All content should be accurate, tested, and helpful for developers learning React Native in 2025.
