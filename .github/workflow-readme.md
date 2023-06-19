## GitHub Runner Workflow for Continuous Integration

In this section, we will add a basic GitHub Actions workflow to automate the build and test process for your Dockerized Python app. GitHub Actions allows you to define custom workflows that run in response to various events, such as pushing code to a repository.

### Prerequisite

- Fork the repository
- Go to your fork repository and click on `Settings`
- On the left part of your screen click on `Actions` -> `General`
- On this page, look for `Workflow permissions` and check `Read and write permissions`
- Save the changes

### Step 1: Go to `.github` directory

In your project directory, navigate into the directory named `.github/workflows`

### Step 2: Create workflow file

Inside the `.github/workflows` directory, create a new file and give and add `.yml` extension to it. This file will contain the github runner configuration.

<details> 
    <summary>You can try and create the workflow yourself or use the following code</summary>

    name: Build - Test - Push
    
    on:
      push:
        branches: 
          - master
    
    env:
      REGISTRY: ghcr.io
      IMAGE_NAME: ${{ github.repository }}
    
    jobs:
      build-and-push-image:
        runs-on: ubuntu-latest
        permissions:
          contents: read
          packages: write
    
        steps:
          - name: Checkout repository
            uses: actions/checkout@v3
    
          - name: Log in to the Container registry
            uses: docker/login-action@65b78e6e13532edd9afa3aa52ac7964289d1a9c1
            with:
              registry: ${{ env.REGISTRY }}
              username: ${{ github.actor }}
              password: ${{ secrets.GITHUB_TOKEN }}
    
          - name: Extract metadata (tags, labels) for Docker
            id: meta
            uses: docker/metadata-action@9ec57ed1fcdbf14dcef7dfbe97b2010124a938b7
            with:
              images: ${{ env.REGISTRY }}/${{ env.IMAGE_NAME }}
    
          - name: Build and push Docker image
            uses: docker/build-push-action@f2a1d5e99d037542a71f64918e516c093c6f3fc4
            with:
              context: .
              push: true
              tags: ${{ steps.meta.outputs.tags }}
              labels: ${{ steps.meta.outputs.labels }}
    
</details>

### Step 3: Commit and Push Changes

Commit the `.github` directory and its contents to your repository.

```bash
git add .github
git commit -m "Add GitHub Actions workflow"
git push origin master
```

### Step 4: Job checking

After the merge was completed, a job will start. You will see a new tab on your repository named: `Actions`, click on that and navigate to the latest job.
