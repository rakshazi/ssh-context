# ssh-context [![Donate](https://liberapay.com/assets/widgets/donate.svg)](https://liberapay.com/rakshazi/donate)

Bash wrapper around ssh which provides you ability to use contexts (as in kubectl) for SSH.

Better to describe it with example.

1. You are developer involved in multiple projects. Each project has own dev/staging/production servers, git services, ssh keys, etc.
2. You don't want to manually enter ssh key location each time (or mix your ssh config file).
3. You want to share ssh config of one of the projects.
4. It's not usable to do that with standard ssh toolchain

And here is ssh-context.

1. Project = context
2. Context = separate ssh config, keys, git repos, etc.
3. Use full power of isolated ssh config

## Installation

Just place `ssh-context` bash script in any location from your `$PATH`, `chmod +x` against it and run `ssh-context bootstrap` to init file structure

### Optional: Set ssh-context as alias for ssh

**Bash**: Add this alias to `.bashrc` or `.bash_profile` (for OSX):

**ZSH**: Add this alias to `.zshrc`

**Fish**: Add this alias to `config.fish`

```bash
alias ssh="ssh-context wrapper"
```

### Set context per git repo

If you have multiple git repos, like `project1`, `project2`, `projectN`, etc. you may want to use them with different contexts.
In that case, run `ssh-context switch CONTEXT_YOU_WANT_TO_USE_FOR_THAT_GIT_REPO` and context name will be saved to `git config ssh.context` var
in your local repo (remote not affected).

## Usage

**Install ssh-context**

```bash
ssh-context bootstrap
```

**Create new context**

```bash
ssh-context init myproject
```

**Switch context**

> **NOTE**: if you run `switch` inside the folder with git repo,
> context name will be saved to `git config ssh.context`,
> so next time when you will ssh from that folder, context from `git config ssh.context`
> will be used automaticly, if you don't set context name explicitly.

```bash
ssh-context switch context_name
```

**Connect with current context**

```bash
ssh-context wrapper <ssh args>
# example:
ssh-context wrapper -vv user@server
```

**Connect with another context**

```bash
ssh-context wrapper <context> <ssh args>
# example:
ssh-context wrapper anotherproject server
```
