# Release-Please Prerelease and Release Example

This repository demonstrates how to implement a SOC 2 compliant release workflow using the [release-please-action](https://github.com/googleapis/release-please-action). The workflow automates version management, changelog generation, and GitHub release creation, ensuring a consistent and auditable release process.

## Overview

The release workflow consists of two main stages:
1. **Prerelease** - Creates release candidates (RC) for testing before final release
2. **Release** - Creates the final release after successful testing

This approach supports SOC 2 compliance by:
- Maintaining a clear audit trail of all changes
- Enforcing a consistent release process
- Automating version management
- Providing traceability between code changes and releases

## Workflow Features

- **Automated Versioning**: Automatically increments version numbers based on [Conventional Commits](https://www.conventionalcommits.org/)
- **Changelog Generation**: Automatically creates and updates CHANGELOG.md with categorized changes
- **GitHub Releases**: Creates GitHub releases with appropriate tags
- **Version Synchronization**: Updates version information across multiple files
- **Prerelease Support**: Creates release candidates for testing before final release
- **Conditional Execution**: Runs different jobs based on whether it's a prerelease or final release

## How It Works

### Configuration Files

- `.github/prerelease-config.json`: Configuration for prerelease stage
- `.github/release-config.json`: Configuration for final release stage
- `.github/prerelease-manifest.json`: Tracks the prerelease version
- `.github/release-manifest.json`: Tracks the release version

### Workflow Stages

1. **Label Check**: Creates the necessary labels for release-please PRs
2. **Prerelease Preparation**: Creates or finalizes a prerelease pull request
3. **Prerelease Testing**: Runs tests before creating the prerelease
4. **Prerelease Creation**: Creates the prerelease and a subsequent release pull request
5. **Post-Prerelease Steps**: Runs any necessary steps after prerelease
6. **Release Creation**: Creates the final release
7. **Post-Release Steps**: Runs any necessary steps after release

### Version Management

In this example the workflow updates version information in:
- `version.txt`: Simple version tracking
- `.github/prerelease-manifest.json`: Version manifest for release-please
- `library/build.gradle.kts`: Version in build configuration (using special markers)

### Changelog Management

The CHANGELOG.md file is automatically updated with:
- New features (from `feat:` commits)
- Bug fixes (from `fix:` commits)
- Miscellaneous changes (from `chore:` and `build:` commits)
- Documentation updates (from `docs:` commits)

## Usage

1. Push changes to the main branch with [Conventional Commits](https://www.conventionalcommits.org/)
2. The workflow automatically creates a prerelease pull request
3. When the prerelease PR is merged, a release candidate is created
4. After testing, the workflow creates a final release pull request
5. When the release PR is merged, the final release is created

## Implementation Details

The workflow is implemented using GitHub Actions and the release-please-action. It requires:
- GitHub repository permissions for contents, pull-requests, and repository-projects
- Conventional commit messages for proper changelog generation and version bumping
- Configuration files for prerelease and release stages
