# Release Process

This project uses Release Please for automated releases.

## Release Workflow

### Conventional Commits

We follow [Conventional Commits](https://www.conventionalcommits.org/) specification:

- `fix:` patches
- `feat:` minor features
- `feat!:` or `fix!:` breaking changes

### Pre-1.0 Versioning

While version is `0.x.x`, breaking changes bump **minor** version.

### Release Process

1. Push commits to `main` branch
2. Release Please will:
   - Analyze commits
   - Determine version bump
   - Update `package.json`
   - Update `CHANGELOG.md`
   - Create a release PR

3. Review and merge the Release Please PR

### Commit Message Examples

- `fix: resolve task tracking issue`
- `feat: add global task support`
- `feat!: change task management API`
- `docs: improve README`
- `chore: update dependencies`

## Do Not

- Manually edit Release Please PRs
- Manually create GitHub releases
- Modify version numbers directly

## Publishing

Releases are automatically published to NPM when the Release Please PR is merged.

### NPM Trusted Publishing

This project uses [NPM Trusted Publishing](https://docs.npmjs.com/generating-provenance-statements) with GitHub Actions. No npm tokens are needed - authentication is handled automatically via OIDC (OpenID Connect).

When you merge a release PR, the GitHub Actions workflow will automatically:

1. Build the plugin
2. Publish to NPM with provenance statements
3. Create a GitHub release

### Manual Releases

You can also manually trigger a release by pushing a tag in the format `v{semver}`:

```bash
git tag v1.2.3
git push origin v1.2.3
```

This will:

1. Trigger the release workflow
2. Create a GitHub release
3. Publish to NPM with the tag version

Use manual releases for:

- Hot-fixes outside the normal release cycle
- Bypassing Release Please when needed
- Direct version control
