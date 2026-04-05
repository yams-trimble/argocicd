# TODO: Reflect changes in ArgoCD after adding docker.yml

## Steps to complete:
1. [x] Fix image repo mismatch in helm-chart/values.yaml (change repository to yams0325/flask-app)
2. [ ] Check git status and stage changes (git add .github/workflows/docker.yml etc.)
3. [ ] Commit and push to main (git commit -m "Add docker.yml workflow" && git push origin main)
4. [ ] Monitor GitHub Actions workflow run (gh run list or GitHub UI)
5. [ ] Get new image tag (GITHUB_SHA from workflow) and update values.yaml image.tag
6. [ ] Commit/push tag update (triggers ArgoCD sync)
7. [ ] Verify ArgoCD sync and deployment (argocd app get flask-app, port-forward test)

Track progress by updating this file after each step.
