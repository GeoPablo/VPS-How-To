# Git commands

1. Check ignored files

`git status --ignored`

2. Delete changes
   `git reset --hard`

# Errors

1. [cant access git attrs](https://stackoverflow.com/questions/27150926/unable-to-access-git-attributes)

# Git commits tags:

- `@fix` a bug / error fix
- `@refactor` change the implementation of a code
- `@feat` - a new feature
- `@docs` - documentation
- `@style` -formatting, missing semi colons, …
- `@test` - (when adding missing tests)
- `@chore` - (maintenance work, dependencies upgrading or downgrading commit)
- `@security`
- `@example`
- `@breaking`
- `@config`
- `@wip` - for work in progress commit

## Examples

1. `git commit -m "@wip - setting up the initial project structure"` - good when you first create a new project

2. `git commit -m "@breaking @refactor @chore - update the dependency X"` - a new breaking change while refactoring some code that required maintenance
