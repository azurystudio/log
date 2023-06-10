## log

If you use log, you should have a `changelog.md` file (if you don`t, it will be generated). All your changes should be made through pull requests. log collects the titles of the last merged pull requests and creates a changelog and a release when you push a new tag to the origin.

`.github/workflows/update.yml`

```yml
name: 'publish'

on:
  push:
    tags:
      - 'v*'

jobs:
  publish:
    runs-on: 'ubuntu-latest'

    permissions:
      pull-requests: 'read'
      contents: 'write'

    steps:
      - uses: 'actions/checkout@v3'

      - name: 'Publish Release'
        uses: 'azurystudio/log@v1'
```

### Action Inputs

| Name | Description | Default |
| --- | --- | --- |
| `draft` | Create the release as a draft. | `false` |
| `prerelease` | Create the release as a prerelease. | `false` |
| `style` | Set the style of the changelog. This is a combination of the following options separated by a comma and space, e.g. `author, description`: `description`, `author` | |
| `commit_message` | Set a custom commit message. If your message contains `{tag}`, it'll be automatically replaced with the tag name of the release. | `package: publish {tag}` |
| `token` | `GITHUB_TOKEN` (permissions `contents: write` and `pull-requests: read`) or a `repo` scoped [Personal Access Token (PAT)](https://docs.github.com/en/github/authenticating-to-github/creating-a-personal-access-token). | `GITHUB_TOKEN` |

### Action Outputs

| Name | Description | Example |
| --- | --- | --- |
| `release_id` | Create the release as a draft. | `1` |
| `tag_name` | Create the release as a draft. | `v1.0.0` |
| `created_at` | Create the release as a draft. | `2023-06-10T16:29:08.625Z` |
| `release_body` | Create the release as a draft. | |
| `changelog_body` | Create the release as a draft. | |
