ref: https://squidfunk.github.io/mkdocs-material/getting-started/


1. Create a new environment
     conda create --name mkdocsenv python

2. Activate the environment
    conda activate mkdocsenv

3. Install mkdocs-material
    pip install mkdocs-material


4. Create a new project
    mkdocs new mkdocs-project
    cd mkdocs-project



5. modify mkdocs.yml by adding

    theme:
        name: material



6. Run the server
    mkdocs serve


7. Build the site
    mkdocs build
    
8. Deploy the site
    mkdocs gh-deploy


9. Add github actions

name: ci 
on:
  push:
    branches:
      - master 
      - main
permissions:
  contents: write
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-python@v4
        with:
          python-version: 3.x
      - uses: actions/cache@v3
        with:
          key: mkdocs-material-${{ github.ref }} 
          path: .cache
          restore-keys: |
            mkdocs-material-
      - run: pip install mkdocs-material 
      - run: mkdocs gh-deploy --force

