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
      - uses: actions/checkout@v2
        with:
          fetch-depth: 0
      - uses: actions/setup-java@v2
        with:
          java-version: 17
          distribution: 'adopt'
      - name: Generate Javadoc
        run: mvn org.apache.maven.plugins:maven-javadoc-plugin:3.3.1:aggregate
      - name: Deploy 🚀
        uses: JamesIves/github-pages-deploy-action@4.1.8
        with:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          BRANCH: javadoc
          CLEAN: true
          FOLDER: target/site/apidocs
          TARGET_FOLDER: javadoc
```

### Your Java version is not 17 ?

If your Java project is not in Java 17, don't forget to modify that line:
```YAML
      uses: actions/setup-java@v2
      with:
        distribution: 'adopt'
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
