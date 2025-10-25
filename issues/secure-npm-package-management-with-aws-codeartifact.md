# 📦 Secure Private Package Hosting Using AWS CodeArtifact

### 🧩 Problem
Our development team built a custom Node.js package to reuse across multiple projects.  
Initially, it was hosted on **public npm**, which introduced:
- **Security risks** (public exposure of internal code)
- **Version control issues** due to open access
- **No centralized management** of package versions

I proposed using **AWS CodeArtifact** for private package hosting.  
However, developers faced an issue — after configuring CodeArtifact credentials globally, **public npm packages became inaccessible**.

---

### ⚙️ Environment & Tools
- **AWS CodeArtifact**
- **npm (Node.js)**
- **.npmrc configuration**
- **IAM authentication for CodeArtifact**
- **Jenkins / GitLab CI pipelines** (for package publishing & usage)

---

### 🛠️ Solution
To ensure developers could use both **private (CodeArtifact)** and **public npm** packages simultaneously:

1. Created a **custom `.npmrc` file** at the project root (not global) to maintain scoped configuration.  
2. Added **CodeArtifact registry and auth token** settings.  
3. Retained **public npm registry** references for unscoped packages.  
4. Ensured seamless package installation via `npm install` for both sources.

---

### ⚙️ Example `.npmrc` Configuration

```ini
# AWS CodeArtifact (private registry)
@company-scope:registry=https://company-domain-123456.d.codeartifact.ap-south-1.amazonaws.com/npm/private-repo/
//company-domain-123456.d.codeartifact.ap-south-1.amazonaws.com/npm/private-repo/:always-auth=true
//company-domain-123456.d.codeartifact.ap-south-1.amazonaws.com/npm/private-repo/:_authToken=${CODEARTIFACT_AUTH_TOKEN}

# Default public npm registry
registry=https://registry.npmjs.org/
