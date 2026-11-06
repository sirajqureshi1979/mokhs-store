# MOKHS.STORE — GitHub Hosting & Custom Domain Guide (https://mokhs.store/)

This guide provides instructions to connect this repository to GitHub and host it directly under your custom domain **https://mokhs.store/** using GitHub Pages and automated GitHub Actions.

---

## 1. Quick Terminal Commands

Run these commands in your project root terminal to connect and push this codebase to your GitHub repository:

```bash
# 1. Add your GitHub remote repository
git remote add origin https://github.com/sirajwuhan-bot/MOKHS.git

# 2. Ensure default branch is main
git branch -M main

# 3. Push all code and deployment workflows to GitHub
git push -u origin main
```

---

## 2. GitHub Pages Configuration

1. Open your repository on GitHub (`https://github.com/sirajwuhan-bot/MOKHS`).
2. Navigate to **Settings** > **Pages** (in the left sidebar).
3. Under **Build and deployment**:
   - **Source**: Select `GitHub Actions`.
4. Under **Custom domain**:
   - Verify that **`mokhs.store`** is entered (automatically created via the `public/CNAME` file).
5. Check **Enforce HTTPS** (GitHub will provision a free Let's Encrypt SSL/TLS certificate).

---

## 3. Domain Registrar DNS Settings (Point `mokhs.store` to GitHub)

In your DNS Management console (e.g., GoDaddy, Namecheap, Cloudflare, PKNIC, etc.), add the following DNS records:

### A Records (Apex Domain `@` / `mokhs.store`):
| Type | Name / Host | Value / Target IP | TTL |
|------|-------------|-------------------|-----|
| `A`  | `@`         | `185.199.108.153` | 3600 (or Auto) |
| `A`  | `@`         | `185.199.109.153` | 3600 (or Auto) |
| `A`  | `@`         | `185.199.110.153` | 3600 (or Auto) |
| `A`  | `@`         | `185.199.111.153` | 3600 (or Auto) |

### CNAME Record (Subdomain `www`):
| Type    | Name / Host | Value / Target                              | TTL |
|---------|-------------|---------------------------------------------|-----|
| `CNAME` | `www`       | `sirajwuhan-bot.github.io`                  | 3600 (or Auto) |

---

## 4. Automatic Continuous Deployment (CI/CD)

The repository includes `.github/workflows/deploy.yml`. Every time you push a commit to the `main` branch:
1. GitHub Actions automatically installs packages (`npm install`).
2. Builds the optimized production bundle (`npm run build`).
3. Deploys the static site to GitHub Pages with the `CNAME` pointing to `https://mokhs.store/`.
