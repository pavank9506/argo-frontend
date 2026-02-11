# GitOps Runbook for Argo Frontend

## Overview
This runbook provides step-by-step instructions for managing the Argo Frontend application using GitOps principles. All changes to the application, infrastructure, and configuration are made via Git and automatically applied by Argo CD.

---

## 1. Prerequisites
- Access to the Git repository containing the manifests.
- Argo CD installed and configured.
- Kubernetes cluster access.

---

## 2. Workflow

### 2.1. Making Changes
1. Clone the repository:
   ```bash
   git clone <repo-url>
   ```
2. Create a new branch for your changes:
   ```bash
   git checkout -b <feature-branch>
   ```
3. Edit the relevant YAML files (e.g., `frontend/values.yaml`, `frontend/templates/deployment.yaml`).
4. Commit your changes:
   ```bash
   git add .
   git commit -m "Describe your change"
   ```
5. Push the branch:
   ```bash
   git push origin <feature-branch>
   ```
6. Create a Pull Request and get it reviewed.
7. Merge the PR to the main branch.

---

### 2.2. Argo CD Sync
- Argo CD will automatically detect changes in the repository and apply them to the cluster.
- To manually sync:
  1. Open Argo CD UI.
  2. Select the application.
  3. Click "Sync".

---

## 3. Rollback
1. Identify the commit to rollback to.
2. Create a new branch from that commit:
   ```bash
   git checkout <commit-hash>
   git checkout -b rollback-branch
   ```
3. Push and create a PR to merge this branch.
4. Argo CD will apply the rollback after merge.

---

## 4. Troubleshooting
- **Sync failures:**
  - Check Argo CD UI for error messages.
  - Validate YAML syntax.
  - Ensure all referenced resources exist.
- **Application not updating:**
  - Confirm Argo CD is monitoring the correct branch.
  - Check for webhook issues if using automatic sync.

---

## 5. Best Practices
- Use descriptive commit messages.
- Test changes in a staging environment before production.
- Keep manifests DRY and modular.
- Review all changes via Pull Requests.

---

## 6. References
- [Argo CD Documentation](https://argo-cd.readthedocs.io/en/stable/)
- [GitOps Principles](https://www.gitops.tech/)

---

## 7. Contacts
- DevOps Team: devops@example.com
- Argo CD Admin: admin@example.com

---

_Last updated: February 11, 2026_
