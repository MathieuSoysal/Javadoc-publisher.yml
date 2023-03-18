# Deploy Publish JavaDoc
[![Public workflows that use this action.](https://img.shields.io/endpoint?url=https%3A%2F%2Fapi-endbug.vercel.app%2Fapi%2Fgithub-actions%2Fused-by%3Faction%3DMathieuSoysal%2FJavadoc-publisher%26badge%3Dtrue)](https://github.com/search?o=desc&q=MathieuSoysal+javadoc-publisher+path%3A.github%2Fworkflows+language%3AYAML&s=&type=code) [![Test Actions](https://github.com/MathieuSoysal/publish-javadoc/actions/workflows/test-action-final.yml/badge.svg)](https://github.com/MathieuSoysal/publish-javadoc/actions/workflows/test-action-final.yml)*(Tested on Java 8, 11, 17, 19, Maven, Gradle, Ubuntu, Macos, Windows)*


Automatically generate Javadoc from your Java project and publish it to GitHub Page.

## Requirements
- Your project need to use **Maven** or **Gradle**.
<details>
<summary>
<h2>Inputs</h2>
</summary>

|                   |                                                            |                  |
|-------------------|------------------------------------------------------------|------------------|
| java-version      | java version inside your project                           | 17               |
| GITHUB_TOKEN      | The GitHub token the GitHub repository                     |                  |
| javadoc-branch    | Branch where the javadoc is hosted                         | javadoc          |
| target-folder     | Directory where the javadoc contents should be stored      | .                |
| java-distribution | Java distribution inside your project                      | adopt            |
| project           | Maven or Gradle project                                    | maven            |
| custom-command    | Custom command to generate the javadoc                     | ""               |
| subdirectories    | Custom subdirectories to upload from                       |                  |
| without-deploy    | Enable or disable deploy of the javadoc to the GitHub Page | false            |
| without-checkout  | Enable or disable the checkout                             | false            |
</details>

## Usage

### For Maven project

The workflow, usually declared in `.github/workflows/publish-javadoc.yml`, looks like:

<details open>

<summary>.github/workflows/publish-javadoc-maven.yml</summary>

```YAML
name: Deploy Javadoc

on:
  push:
    branches:
      - master
      - main

jobs:
  publish:
    runs-on: ubuntu-latest
    steps:
      - name: Deploy JavaDoc 🚀
        uses: MathieuSoysal/Javadoc-publisher.yml@v2.4.0
        with:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          javadoc-branch: javadoc
          java-version: 17
          target-folder: javadoc # url will be https://<username>.github.io/<repo>/javadoc, This can be left as nothing to generate javadocs in the root folder.
          project: maven # or gradle
          # subdirectories: moduleA moduleB #for subdirectories support, needs to be run with custom command
```
</details>

### For Gradle project

The workflow, usually declared in `.github/workflows/publish-javadoc.yml`, looks like:

<details open>
<summary>.github/workflows/publish-javadoc-gradle.yml</summary>



```YAML
name: Deploy Javadoc

on:
  push:
    branches:
      - master
      - main

jobs:
  publish:
    runs-on: ubuntu-latest
    steps:
      - name: Deploy JavaDoc 🚀
        uses: MathieuSoysal/Javadoc-publisher.yml@v2.4.0
        with:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          javadoc-branch: javadoc
          java-version: 17
          target-folder: javadoc 
          project: gradle
```
</details>

### With custom command for generating Javadoc

If you want to use a custom command for generating Javadoc, you can use the `custom-command` input. This input is a string that will be executed in the root of your project. For example, if you want to use the `javadoc` command, you can use the following workflow:

<details open>
<summary>.github/workflows/publish-javadoc-custom-command.yml</summary>

```YAML
name: Deploy Javadoc

on:
  push:
    branches:
      - master
      - main

jobs:
  publish:
    runs-on: ubuntu-latest
    steps:
      - name: Deploy JavaDoc 🚀
        uses: MathieuSoysal/Javadoc-publisher.yml@v2.4.0
        with:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          javadoc-branch: javadoc
          java-version: 17
          target-folder: javadoc 
          project: gradle
          custom-command: javadoc -d javadoc -sourcepath src/main/java -subpackages .
```
</details>

### GitHub page

Don't forget to configure your repository settings with your new GitHub Page. 😉

### Badge

```Markdown
[![Javadoc](https://img.shields.io/badge/JavaDoc-Online-green)](https://YOUR-USERNAME.github.io/YOUR-REPO/javadoc/)
```
In the badge link, replace *YOUR-USERNAME* with your GitHub Username and replace *YOUR-REPO* with the name of your GitHub repository.

## Contributing

Want to contribute to Javadoc Publisher? Awesome! Check out [the contributing guidelines](CONTRIBUTING.md) to get involved.

### Requirements to your environment to test in locally

- Install [nektos/act](https://github.com/nektos/act) & clone the repo `git clone git@github.com:MathieuSoysal/Javadoc-publisher.yml.git`  
OR
- Use the devcontainer of the repo: with [GitHub Codespaces](https://github.com/codespaces/new?hide_repo_select=true&ref=main&repo=441722764)

### Command to test your changes

```bash
act workflow_dispatch -W .github/workflows/test-action-local.yml -P ubuntu-latest=quay.io/jamezp/act-maven
```

## Contributors
<img src="CONTRIBUTORS.svg"/>


## Stars 🎇

If you like or use this project, please don't forget to give it a star ⭐️. Thanks!

## License
The Dockerfile and associated scripts and documentation in this project are released under the [Apache 2.0 License](https://github.com/MathieuSoysal/publish-javadoc/blob/main/LICENSE).
