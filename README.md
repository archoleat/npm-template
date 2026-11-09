# NPM Template

A TypeScript package starter that builds an ES module and declaration files
with Rollup. Tests run with Bun; semantic-release handles versions and
publication from Conventional Commits after the configured checks pass.

## Getting started

Create a repository with **Use this template** and install Bun, Git and
Node.js LTS. Replace the placeholders below:

```shell
git clone git@github.com:YOUR_OWNER/YOUR_REPOSITORY.git my-package

cd my-package

bun run init
```

`init` installs dependencies and enables Husky hooks. This is a library
starter, so there is no application server.

## Configuration

| Setting | Where to change it |
| --- | --- |
| Package identity | [package.json](package.json). |
| Public API | [src/index.ts](src/index.ts). |
| Example test | [message.spec.ts](specs/message.spec.ts). |
| Build outputs | [rollup.config.ts](rollup.config.ts). |
| Release policy | [release.config.js](release.config.js). |
| Maintainers | [CODEOWNERS](.github/CODEOWNERS) and README badges. |

Choose an available package name and update the author, repository URLs and
keywords. When changing entry points, keep Rollup outputs and the package's
`exports`, `types` and `files` fields in sync.

> [!CAUTION]
> Review the license and retain required copyright notices when reusing the
> template. Keep publication disabled until package ownership and credentials
> are configured.

## Development checks

```shell
bun test
bun tsc --noEmit
bun rollup -c
bun eslint 'src/**/*.ts'
bun prettier . --check
bun remark . --quiet --frail

npm pack --dry-run
```

The build writes `index.js` and `index.d.ts`. Inspect the dry-run file list
before publishing. ESLint reads [`eslint.config.js`](eslint.config.js);
[`.remarkignore`](.remarkignore) applies to Markdown checks only.

Hooks and CI run the checks configured in this repository; they do not
replace API design or code review. The existing
[`stale.yaml`](.github/workflows/stale.yaml) marks eligible issues and pull
requests stale after **90 inactive days**. Exempt labels and closure behavior
are configured in that workflow.

## Publication

The original `archoleat/npm-template` repository is excluded by the guard in
[`release.yaml`](.github/workflows/release.yaml). Review this guard and the
workflow before enabling publication in a repository created from the template.

| Actions secret | Purpose |
| --- | --- |
| `ARCHOLEATER_APP_ID` | Client ID of your publishing GitHub App. |
| `ARCHOLEATER_APP_PRIVATE_KEY` | App private key. |
| `NPM_PUBLISH_TOKEN` | npm token allowed to publish your package. |

Keep these names or update their references in the workflow. Configure App
permissions and branch rules for the publishing identity. Pull requests and
auto-merge must be enabled if you keep the Dependabot auto-merge workflow.

Release runs after a successful `Spec` push check on the current `main`
revision, repeats quality checks and builds the package before publication.
The supplied configuration maps `feat` to a minor release and `fix` to a patch;
`docs`, `ci` and `chore` alone do not publish a version.

## Contributing

See the [contribution guide](https://github.com/archoleat/.github/blob/main/CONTRIBUTING.md).

## License

[MIT](LICENSE).
