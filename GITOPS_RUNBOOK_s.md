
# GitOps Runbook

## 1. Introduction
This runbook provides a comprehensive, industry-standard guide for implementing and operating GitOps workflows for Kubernetes-based applications using Argo CD.

---

## 2. Prerequisites
- Version-controlled repository (e.g., GitHub, GitLab, Bitbucket)
- Kubernetes cluster access
- Argo CD installed and configured
- Argo CD access (UI, CLI, or API)
- Access control and RBAC policies in place

---

## 3. GitOps Workflow with Argo CD

### 3.1. Change Management
1. **Branching:**
   - Use feature branches for changes (e.g., `feature/xyz`, `bugfix/abc`).
2. **Pull Requests (PRs):**
   - All changes must be submitted via PRs.
   - Require code review and approval before merging.
3. **Commit Messages:**
   - Use clear, descriptive commit messages following the Conventional Commits standard.
4. **Merging:**
   - Only merge to main/trunk after successful review and CI checks.

### 3.2. Repository Structure
- Separate application, infrastructure, and environment manifests.
- Use overlays, Kustomize, or Helm for environment-specific configuration.
- Example structure:
  ```
  ├── apps/
  ├── infra/
  ├── environments/
  │   ├── dev/
  │   ├── staging/
  │   └── prod/
  ```

### 3.3. Argo CD Application Management
- Define Argo CD Application manifests for each deployable unit.
- Store Application manifests in Git.
- Use ApplicationSets for dynamic or multi-cluster deployments if needed.

### 3.4. Syncing Changes
- Argo CD continuously monitors the repository for changes.
- On merge, Argo CD applies changes to the cluster.
- Manual sync can be triggered via Argo CD UI, CLI, or API if needed.

---

## 4. Rollback & Disaster Recovery
1. **Rollback:**
   - Revert to a previous commit/tag in Git.
   - Merge the rollback PR to main/trunk.
   - Argo CD will sync the rollback automatically.
   - Alternatively, use the Argo CD UI/CLI to rollback to a previous application revision.
2. **Disaster Recovery:**
   - Store all manifests and Argo CD Application definitions in Git (single source of truth).
   - To recover, redeploy Argo CD and point it to the repository.
   - Cluster state will be restored to match Git.

---

## 5. Security & Compliance
- Enforce RBAC for Git, Argo CD, and cluster access.
- Use signed commits and tags.
- Enable audit logging in Git, Argo CD, and Kubernetes.
- Scan manifests for vulnerabilities (e.g., with OPA, Kyverno, Snyk).
- Protect main/trunk branch (require PR reviews, CI checks).
- Use Argo CD SSO and restrict admin access.

---

## 6. Monitoring & Alerts
- Monitor Argo CD health and application status (UI, CLI, Prometheus metrics).
- Set up alerts for sync failures, drift, or policy violations.
- Integrate with incident management tools (PagerDuty, Opsgenie, etc.).

---

## 7. Best Practices
- Keep manifests DRY and modular.
- Use parameterization for environment differences.
- Document all processes, repository structure, and Argo CD Application definitions.
- Regularly review and update RBAC and security policies.
- Test changes in lower environments before production.
- Use Argo CD Projects to enforce multi-tenancy and policy boundaries.

---

## 8. Troubleshooting
- **Sync failures:**
   - Check Argo CD application status and logs (UI, CLI).
   - Validate manifest syntax and schema.
   - Ensure cluster connectivity and permissions.
- **Drift detected:**
   - Investigate manual changes in the cluster.
   - Reconcile state by re-syncing from Git or using the "Refresh" and "Sync" options in Argo CD.

---



