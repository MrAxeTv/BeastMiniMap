# GitHub and GitBook Workflow

The editable wiki is stored under `docs/gitbook/`. `README.md` is its welcome page, `SUMMARY.md` controls its sidebar, and `.gitbook.yaml` defines its content root.

Use the public [MrAxeTv/BeastMiniMap repository](https://github.com/MrAxeTv/BeastMiniMap) for GitBook synchronization. It contains plugin information and downloads. Plugin source code and plugin JARs remain outside this documentation repository.

## Connect GitBook

1. Create or open the BeastMiniMap documentation space in GitBook.
2. Connect its GitHub integration to `MrAxeTv/BeastMiniMap`, branch `main`.
3. Map the BeastMiniMap space to the repository directory **`docs/gitbook`**. Do not import the repository root as the space: it also contains language downloads and pack information.
4. Choose the repository content as the source for the first import, after checking any existing GitBook pages you want to retain.
5. Check that Welcome, Getting Started, Resource Packs, Maps, Commands, Permissions, Customization, Terrain, Storage, and Troubleshooting appear in the sidebar.
6. Preview the imported pages and links, then publish the site when ready.

The mapped directory includes:

```yaml
root: ./

structure:
  readme: README.md
  summary: SUMMARY.md
```

This is GitBook's `.gitbook.yaml` format; its lowercase keys belong to GitBook, rather than the plugin's PascalCase configuration. If GitBook generates a site-level `gitbook-docs.yaml`, keep the space's existing key stable and set its `content.directory` to `./docs/gitbook`. The `root` above remains relative to that mapped directory.

GitBook's settings labels can change. See the official [Git Sync content configuration guide](https://gitbook.com/docs/docs-as-code/git-sync/content-configuration) for the current directory mapping and navigation format.

## Update the wiki

Edit the authoritative Markdown under `docs/gitbook/` in the plugin project. Review and copy only the wiki files to the public checkout's matching directory. Keep the public copy byte-for-byte aligned with the reviewed authoring files.

From the **public documentation checkout**, review the exact files before committing:

```powershell
git status --short
git diff -- docs/gitbook README.md
git add -- docs/gitbook README.md
git diff --cached --name-only
git diff --cached --check
git commit -m "Update BeastMiniMap wiki"
git push origin main
```

The staged list should contain only the intended wiki files and public landing-page changes. Preserve existing language snapshots, releases, and download files. Publishing wiki edits does not require rebuilding the plugin or its resource packs.

GitBook synchronizes the configured branch. Site publication behavior depends on the connected GitBook site's settings; check its preview and published pages after a sync rather than assuming the push published the site.

## Keep pages consistent

When an option changes, update its instructions and examples in the same change. Maintain `SUMMARY.md` when pages move or are added; list each page once. Keep links relative to the wiki so they work both on GitHub and after GitBook import.

Update [Permissions](../permissions.md) whenever action nodes or quotas change. Add messages to every supported locale when the plugin changes its messages. Keep language-download catalog changes in the separate language publication workflow.

For screenshots, follow the [image placement guide](../image-placement-guide.md). Do not add links to files that have not been uploaded.
