1. 
the build pipeline workflow was first step up to make sure everthing runs well before deploying testing with kubernetes deployments file.

Github self-hosted runner was firstly settup and it was has two labels, [selt-hosted, kubernetes] in which the workflow runs.

a github reposiory was created with two branches, main and develop for the workflow runs, and a github token was created and store in the github security page of the repo.

A local registry was created (regitry.local whixh house the image)



prerequite

kustomize installation
self-hosted github runner















Here’s a clear breakdown of each tool and how they’re used in GitHub Actions development:

---

### ⚙️ `act` by Nektos
**Purpose:** Run GitHub Actions locally on your machine.

**What it does:**
- Simulates GitHub Actions workflows without needing to push to GitHub.
- Helps test and debug workflows faster and offline.

**How to use:**
1. Install via Homebrew (`brew install act`) or download from [GitHub](https://github.com/nektos/act).
2. Run a workflow locally:
   ```bash
   act
   ```
   You can specify events like:
   ```bash
   act push
   act pull_request
   ```

**Why it’s useful:**
- Speeds up development by avoiding commits just to test workflows.
- Lets you catch runtime errors early.

---


-Validates YAML structure (indentation, spacing, etc.).
yamllint .github/workflows/ci.yml



actionlint


















































```bash
mkdir auth
htpasswd -Bbn admin yourpassword > auth/htpasswd
```

- `admin` is the username
- `yourpassword` is the password you want to use

---

### 🚀 Step 2: Run the registry with authentication
```bash
docker run -d -p 5000:5000 --restart=always --name registry \
  -v $(pwd)/auth:/auth \
  -e "REGISTRY_AUTH=htpasswd" \
  -e "REGISTRY_AUTH_HTPASSWD_REALM=Registry Realm" \
  -e "REGISTRY_AUTH_HTPASSWD_PATH=/auth/htpasswd" \
  registry:2
```


```bash
docker login registry.local:5000 -u admin
```


.............................................................


```json
"scripts": {
  "test": "echo \"Running tests...\" && exit 0"
}
```

.................................................................

  - uses: github/codeql-action/upload-sarif@v3
      with:
        sarif_file: trivy-results.sarif

    - name: Trigger Dev Deployment
      if: success()
      uses: actions/github-script@v7
      with:
        github-token: ${{ secrets.MY_GITHUB_TOKEN }}
        script: |
          await github.rest.repos.createDispatchEvent({
            owner: context.repo.owner,
            repo: context.repo.repo,
            event_type: 'deploy-dev',
            client_payload: { sha: context.sha }
          })

...............................................................
✅ Exactly — when you shut down your machine, **Docker containers (including your local registry)** stop. That’s why `registry.local:5000` is refusing connections.

---

   ```bash
   docker start registry
   ```

   ```bash
   docker run -d -p 5000:5000 --name registry --restart=always registry:2
   ```

3. verify
   ```bash
   curl http://registry.local:5000/v2/_catalog
   ```
..............................................