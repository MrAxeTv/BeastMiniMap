# GitHub and GitBook Workflow

The editable wiki is stored under `docs/gitbook/`. The repository-root `gitbook-docs.yaml` maps the BeastMiniMap space to that folder. Inside the folder, `README.md` is the welcome page, `SUMMARY.md` controls the sidebar, and `.gitbook.yaml` defines the space's content settings.

Use the public [MrAxeTv/BeastMiniMap repository](https://github.com/MrAxeTv/BeastMiniMap) for GitBook synchronization. It contains plugin information and downloads. Plugin source code and plugin JARs remain outside this documentation repository.

## Connect GitBook

For the site's Git Sync **Configure** screen:

1. Create or open the BeastMiniMap documentation site in GitBook and connect its GitHub integration.
2. Select repository `MrAxeTv/BeastMiniMap` and branch `main`.
3. Choose **GitHub to GitBook** for the first import, after checking any existing GitBook pages you want to retain.
4. Leave **Project directory** as **`./`**: the repository root. This field locates the site configuration, not the wiki's Markdown folder.
5. Click the refresh icon beside the project-directory field so GitBook reads the current branch again, then click **Sync**.
6. Confirm that the imported BeastMiniMap space contains Welcome, Getting Started, Resource Packs, Maps, Commands, Permissions, Customization, Terrain, Storage, and Troubleshooting.
7. Preview the imported pages and links, then publish the site when ready.

The repository has two configuration levels:

```text
gitbook-docs.yaml
docs/
  gitbook/
    .gitbook.yaml
    README.md
    SUMMARY.md
```

The repository-root `gitbook-docs.yaml` maps the space to the wiki directory:

```yaml
$schema: https://api.gitbook.com/gitbook-docs.yaml
site:
  title: BeastMiniMap
  structure:
    - type: space
      key: beastminimap
      title: BeastMiniMap
      path: beastminimap
      default: true
      content:
        directory: ./docs/gitbook
        language: en
```

The space's `.gitbook.yaml` stays inside `docs/gitbook/`:

```yaml
root: ./

structure:
  readme: README.md
  summary: SUMMARY.md
```

The site's **Project directory** remains `./`, while the space's `content.directory` is `./docs/gitbook`. This imports the wiki without turning the repository's language downloads and pack information into wiki pages. The space's `root: ./` is relative to its mapped directory.

After the first sync, keep the space key **`beastminimap`** stable. GitBook uses this key to identify the space; changing it creates a replacement rather than renaming the existing space. When adapting an already connected site, preserve its existing space key instead of replacing it with a new one.

These lowercase configuration keys belong to GitBook, rather than the plugin's PascalCase configuration.

## Missing gitbook-docs.yaml error

If Configure reports that `gitbook-docs.yaml` is missing, check that the file exists at the root of the selected repository and branch. Set **Project directory** to `./`, click its refresh icon, then retry **Sync**. Setting this field to `docs/gitbook` makes GitBook look for the site configuration in the wrong directory for this layout. The `.gitbook.yaml` inside the wiki folder serves a different purpose and does not replace the site configuration.

GitBook's settings labels can change. See the official [Git Sync content configuration guide](https://gitbook.com/docs/docs-as-code/git-sync/content-configuration) for the current directory mapping and navigation format.

## Update the wiki

Edit the authoritative Markdown under `docs/gitbook/` in the plugin project. Review and copy only the wiki files to the public checkout's matching directory. Keep the public copy byte-for-byte aligned with the reviewed authoring files.

From the **public documentation checkout**, review the exact files before committing:

```powershell
git status --short
git diff -- gitbook-docs.yaml docs/gitbook README.md
git add -- gitbook-docs.yaml docs/gitbook README.md
git diff --cached --name-only
git diff --cached --check
git commit -m "Update BeastMiniMap wiki"
git push origin main
```

The staged list should contain only the intended wiki files, GitBook configuration and public landing-page changes. Preserve existing language snapshots, releases, and download files. Publishing wiki edits does not require rebuilding the plugin or its resource packs.

GitBook synchronizes the configured branch. Site publication behavior depends on the connected GitBook site's settings; check its preview and published pages after a sync rather than assuming the push published the site.

## Keep pages consistent

When an option changes, update its instructions and examples in the same change. Maintain `SUMMARY.md` when pages move or are added; list each page once. Keep links relative to the wiki so they work both on GitHub and after GitBook import.

Update [Permissions](../permissions.md) whenever action nodes or quotas change. Add messages to every supported locale when the plugin changes its messages. Keep language-download catalog changes in the separate language publication workflow.

For screenshots, follow the [image placement guide](../image-placement-guide.md). Do not add links to files that have not been uploaded.
