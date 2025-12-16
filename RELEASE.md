# Release & Versioning

This project uses semantic version tags in the format `vMAJOR.MINOR.PATCH` (e.g., `v1.2.3`). The GitHub Actions release workflow validates this format before building and publishing artifacts.

## Steps to Create a Release

1. Ensure `main` (or `master`) has the changes you want to release.
2. Create and push a tag in the format `vMAJOR.MINOR.PATCH`:

   ```powershell
   git pull
   git tag v1.0.0
   git push origin v1.0.0
   ```

3. The workflow will:
   - Validate tag format: must match `^v\d+\.\d+\.\d+$`.
   - Build and publish binaries from `src/csharp/csharp.csproj`.
   - Upload the build artifact and create a GitHub Release with attached files.

## Versioning Guidance

- Bump **MAJOR** for breaking changes.
- Bump **MINOR** for new functionality that is backwards compatible.
- Bump **PATCH** for bug fixes and small improvements.

## Troubleshooting

- If the workflow fails with "Invalid tag format", retag with the correct pattern, e.g., `v2.1.0`.
- Ensure the tag points to the commit you intend to release (`git tag -d vX.Y.Z; git tag vX.Y.Z <commit-sha>`).