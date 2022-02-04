# Javadoc-publisher.yml
Automatically generate Javadoc from your maven project and deploy it with GitHub Page on *javadoc* branch.

## Requirements
- Your project need to use Maven

## Usage

The workflow, usually declared in `.github/workflows/javadoc-publish.yml`, looks like:
```YAML
name: Deploy Javadoc

on:
  push:
    branches:
      - master

jobs:
  publish:
    runs-on: ubuntu-latest
    steps:
      - name: Deploy JavaDoc 🚀
        uses: MathieuSoysal/Javadoc-publisher@2.0.0
        with:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          javadoc-branch: javadoc
          java-version: 17
```

### GitHub page

Don't forget to configure your repository settings with your new GitHub Page. 😉

### Badge

```Markdown
[![Javadoc](https://img.shields.io/badge/JavaDoc-Online-green)](https://YOUR-USERNAME.github.io/YOUR-REPO/javadoc/)
```
In the badge link, replace *YOUR-USERNAME* with your GitHub Username and replace *YOUR-REPO* with the name of your GitHub repository.

## License
The Dockerfile and associated scripts and documentation in this project are released under the [Apache 2.0 License](https://github.com/MathieuSoysal/Javadoc-publisher.yml/blob/main/LICENSE).
