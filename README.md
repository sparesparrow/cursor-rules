# Cursor Rules Repository

A comprehensive collection of Cursor IDE rules for developing AI-powered applications with a focus on agentic workflows, TypeScript development, and cognitive architectures.

## Structure

The rules are organized in a hierarchical structure with increasing specificity:

```
.cursor/rules/
├── 01-base-*.rules.md        # Base rules (agentic, devops)
├── 02-*.rules.md            # Framework rules (typescript, mcp)
├── 03-*.rules.md            # Domain rules (composer, cognitive)
├── 04-security.rules.md     # Security rules
└── 05-top5-inspirations.rules.md  # Advanced patterns
```

## Rule Categories

1. **Base Rules** (01-*)
   - `01-base-agentic.rules.md`: Foundational patterns for agentic workflows
   - `01-base-devops.rules.md`: AI-driven DevOps pipeline standards

2. **Framework Rules** (02-*)
   - `02-typescript.rules.md`: TypeScript development standards
   - `02-mcp-typescript.rules.md`: MCP-specific TypeScript standards

3. **Domain Rules** (03-*)
   - `03-composer-agent.rules.md`: AI composer agent standards
   - `03-cognitive-architecture.rules.md`: Cognitive architecture standards

4. **Security Rules** (04-*)
   - `04-security.rules.md`: Universal security standards

5. **Advanced Patterns** (05-*)
   - `05-top5-inspirations.rules.md`: Advanced workflow patterns and best practices

## Usage

1. **Installation**
   - Clone this repository into your project's root directory
   - Ensure the `.cursor/rules` directory is properly structured

2. **Rule Application**
   - Rules are automatically applied based on file patterns (globs)
   - Higher priority rules (higher numbers) override lower priority ones
   - Security rules (04-*) always take precedence

3. **Development Workflow**
   - Follow the patterns and examples in each rule file
   - Use the provided validation rules for code quality
   - Implement security considerations as specified

## Contributing

1. **Adding New Rules**
   - Follow the existing numbering convention
   - Include proper metadata (description, globs, priority)
   - Provide clear examples and anti-patterns

2. **Modifying Rules**
   - Maintain backward compatibility
   - Update dependencies appropriately
   - Document changes in commit messages

## License

This project is licensed under the MIT License - see the LICENSE file for details.
