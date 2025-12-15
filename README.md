# Livewire Principles Skill

A [Claude Code](https://docs.anthropic.com/en/docs/claude-code) skill that guides you toward simple, maintainable Laravel/Livewire code by helping you avoid over-engineering.

## What is this?

This is a skill for Claude Code - it teaches Claude principles for writing Laravel/Livewire components and tests that are simple, readable, and don't try to be clever. It emerged from real-world refactoring work and captures the mindset needed to write code that's obvious rather than impressive.

## The Core Principles

1. **Trust the Framework** - Laravel validation works. Livewire form binding works. Don't rebuild what's already there.

2. **Test Behavior, Not Implementation** - Test what users see and what data changes. If a test would break when you refactor (without changing behavior), it's testing implementation details.

3. **Let Errors Surface** - Don't hide problems with defensive guards and silent returns. Exceptions are helpful - they tell you something's wrong.

4. **Simple Over Clever** - The right amount of code is the minimum that works. Three similar lines are better than a premature abstraction.

5. **The Happy Path is Enough (Usually)** - For trusted internal apps, test that things work when used correctly. Student-facing features need more care.

## Installation

Copy the skill folder into your project's `.claude/skills/` directory:

```bash
# From your Laravel project root
mkdir -p .claude/skills
cp -r /path/to/livewire-principles .claude/skills/
```

Or clone this repo and copy:

```bash
git clone https://github.com/ohnotnow/claude-skill-livewire.git
cp -r claude-skill-livewire/.claude/skills/livewire-principles your-project/.claude/skills/
```

## Usage

Once installed, Claude Code will automatically use these principles when you're working on Livewire components, Blade templates, or tests. The skill provides guidance through:

- **[SKILL.md](.claude/skills/livewire-principles/SKILL.md)** - The core principles and questions to ask yourself
- **[component-examples.md](.claude/skills/livewire-principles/component-examples.md)** - Side-by-side comparisons of over-engineered vs simple component code
- **[test-examples.md](.claude/skills/livewire-principles/test-examples.md)** - Examples of behavior-focused tests vs implementation-focused tests

## Example: Before and After

**Over-engineered:**
```php
class EditUserModal extends Component
{
    public bool $formModified = false;

    public function updatedName(): void
    {
        $this->formModified = true;
    }

    public function save(): void
    {
        if (! $this->formModified) {
            return;
        }
        // ...
    }
}
```

**Simple:**
```php
class EditUserModal extends Component
{
    public UserForm $form;

    public function save(): void
    {
        $this->form->save();
        Flux::modal('edit-user')->close();
    }
}
```

## The Key Question

Before writing code or tests, ask yourself:

> "Would this test break if I refactored without changing behavior?"

If yes, you're testing implementation. If no, you're testing behavior.

## Philosophy

> "Simplicity is the ultimate sophistication."

Write code that could be read aloud to a business stakeholder. If you find yourself explaining why you needed a `FormModificationTracker` service, something went wrong earlier.

## Customisation

This skill reflects one team's preferences. Feel free to fork and adapt:

- Adjust the staff vs student trust levels for your context
- Add your own framework-specific examples
- Modify principles that don't fit your team's style

## License

MIT - see [LICENSE](LICENSE) for details.

## Contributing

Found these principles helpful? Have suggestions? Issues and PRs are welcome.
