# My Resume

Powered by [GitResume](https://gitresume.co) — Resume as Code.

> **Live Preview:** See what this template looks like when built by GitResume:
> [gitresume.co/@gitresume-co/resume-template](https://gitresume.co/@gitresume-co/resume-template)

## Quick Start

1. Click <kbd>Use this template</kbd> on GitHub to create your own repo
2. Create your `gitresume.yaml` using the [Resume Builder](https://gitresume.co/builder) or by copying `example.gitresume.yaml`
3. [Connect your repo to GitResume](#connect-to-gitresume)
4. Commit and push — GitResume automatically builds your PDF and web resume

## Connect to GitResume

After creating your repo from this template, follow these steps to publish it with GitResume.

### Step 1: Sign in

Go to [gitresume.co/login](https://gitresume.co/login) and sign in with **GitHub** or **Google**.

> If you sign in with Google but your resume repo is on GitHub, that's fine — you'll connect GitHub in the next step.

### Step 2: Create a project

On the dashboard, click <kbd>New Project</kbd> (this takes you to the setup wizard).

**2a — Grant repository access** (first time only)

The wizard will prompt you to grant the **GitResume** GitHub App access to your repos. Pick:

- **Only select repositories** (recommended) — choose just this resume repo
- **All repositories** — convenient but broader than necessary

You can adjust this later from GitHub → Settings → Applications → GitResume, or directly at <https://github.com/apps/gitresume-co/installations/select_target>.

**2b — Select your repo**

Pick the repo you just created from the template. Use the search box if you have many repos.

**2c — Fill in project details**

- **Project name** — defaults to the repo name; edit if you want
- **Slug** — auto-generated from the name; the field shows a live URL preview. This becomes your public URL: `gitresume.co/@<your-username>/<slug>`. Lowercase letters, numbers, and hyphens only.

Click <kbd>Create Project</kbd>.

> Using a filename other than `gitresume.yaml` (e.g. `cv.yaml`)? Create the project with the default first, then update **Resume Path** in the project's **Settings** tab.

### Step 3: Push your resume

Back in your local clone:

```bash
# If you haven't already, copy the example as a starting point
cp example.gitresume.yaml gitresume.yaml

# Edit gitresume.yaml, then:
git add gitresume.yaml
git commit -m "add my resume"
git push
```

GitResume's webhook receives the push and starts building automatically. Watch the build status on your project page; once green:

- **PDF** — downloadable from the project dashboard
- **Web** — published at `gitresume.co/@<your-username>/<slug>`

No webhook fired? Click <kbd>Build Now</kbd> on the project page to trigger one manually.

### Tailoring for specific applications

Push to any **non-default branch** to build a tailored variant without touching your public resume:

```bash
git checkout -b company-acme
# edit gitresume.yaml to emphasise relevant experience
git commit -am "tailor for Acme"
git push -u origin company-acme
```

Branch builds appear in your project's build list alongside the main branch's builds, tagged with the branch name.

## Editor Setup

Autocompletion and validation work out of the box: GitResume is listed in [SchemaStore](https://www.schemastore.org), so editors recognize `gitresume.yaml` (and `*.gitresume.yaml`) by filename alone. In VS Code, install the [YAML extension (Red Hat)](https://marketplace.visualstudio.com/items?itemName=redhat.vscode-yaml); JetBrains IDEs and Neovim (with SchemaStore support) work without extra setup. See `example.gitresume.yaml` for reference.

## Resources

- [Getting Started](https://gitresume.co/docs) — Full setup guide
- [YAML Schema Reference](https://gitresume.co/docs/schema) — All available fields
