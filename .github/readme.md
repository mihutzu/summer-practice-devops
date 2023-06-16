## GitHub Runner Workflow for Continuous Integration

In this section, we will add a basic GitHub Actions workflow to automate the build and test process for your Dockerized Python app. GitHub Actions allows you to define custom workflows that run in response to various events, such as pushing code to a repository.

### Step 1: Go to `.github` directory

In your project directory, navigate into the directory named `.github/workflows`

### Step 2: Create `docker-flow.yml` File

Inside the `.github/workflows` directory, create a new file named `docker-flow.yml`. This file will contain the github runner configuration.

Open the `docker-flow.yml` file in a text editor and paste the following code:

<details> 
    <summary>You can try and create workflow by yourself or use the following code</summary>
    
    name: Build - Test - Push
    
    on:
      push:
        branches:
          - master
    
    jobs:
      build:
        runs-on: ubuntu-latest
    
        steps:
          - name: Checkout repository
            uses: actions/checkout@v3
    
          - name: Set up Python
            uses: actions/setup-python@v4
            with:
              python-version: 3.9
    
          - name: Build and test Docker image
            run: |
              docker-compose build
              docker-compose run --rm app pytest tests/
    
          - name: Log in to the Container registry
            uses: docker/login-action@65b78e6e13532edd9afa3aa52ac7964289d1a9c1
            with:
              registry: ghcr.io
              username: ${{ github.actor }}
              password: ${{ secrets.GITHUB_TOKEN }}
          
          - name: Extract metadata (tags, labels) for Docker
            id: meta
            uses: docker/metadata-action@9ec57ed1fcdbf14dcef7dfbe97b2010124a938b7
            with:
              images: |
                my-docker-hub-namespace/my-docker-hub-repository
                ghcr.io/${{ github.repository }}
          
          - name: Build and push Docker images
            uses: docker/build-push-action@3b5e8027fcad23fda98b2e3ac259d8d67585f671
            with:
              context: .
              push: true
              tags: ${{ steps.meta.outputs.tags }}
              labels: ${{ steps.meta.outputs.labels }}
</details>

Make sure to replace `your-dockerhub-username` with your Docker Hub username.

Save the `docker-flow.yml` file.

### Step 3: Commit and Push Changes

Commit the `.github` directory and its contents to your repository.

```bash
git add .github
git commit -m "Add GitHub Actions workflow"
git push origin master
```

### Step 4: Job checking

After the merge was completed, a job will start. You will see a new tab on your repository named: `Actions`, click on that and navigate to the latest job.
