# TARZO — Visual Studio Code and GitHub setup (Roman Urdu)

## 1) ZIP se project kholna

1. Is ZIP ko **Extract All** karo.
2. `TARZO-GitHub-Ready-Project` folder ko Visual Studio Code mein **File > Open Folder** se kholo.
3. Node.js 22.13+ install hona chahiye.
4. VS Code mein Terminal > New Terminal kholo aur run karo:

```bash
npm ci
npm run dev
```

Terminal jo localhost URL dikhaye, browser mein open karo. Agar API/DB route local environment mangta ho to local Cloudflare D1 setup bhi karna padega.

## 2) Naya GitHub repository banana

1. [github.com/new](https://github.com/new) kholo, account mein login karo.
2. Repository name: `wear-tarzo-website`.
3. **Private repository recommended**: auth/backend code ki privacy aur deployment review ke liye.
4. **Do not add a README, gitignore or license** during repo creation, kyunki folder mein files already maujood hain.
5. VS Code terminal mein niche commands run karo (YOUR_USERNAME apne GitHub username se replace karo):

```bash
git init
git add .
git commit -m "Add TARZO full-stack website source"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/wear-tarzo-website.git
git push -u origin main
```

GitHub authentication maang sakta hai. GitHub Desktop se bhi folder ko GitHub par publish kar sakte ho.

## 3) GitHub upload mein kya include na karein

**Never commit** actual `.env`, `.dev.vars`, passwords, API keys, Cloudflare tokens, admin secrets, user emails/real customer database, `node_modules`, `dist` or `.wrangler` data. `.env.example` sirf sample hai aur tracked hai.

Agar private keys kabhi source mein aa gayi hon, upload se pehle secrets rotate karo. This archive has been scanned for common embedded secret formats but no scanner can guarantee 100% absence.

## 4) GitHub != original live Sites deployment

GitHub par code upload karne se `wear-tarzo.papanotify.chatgpt.site` automatically update nahi hoga. Hosting/deployment alag connected project se hoti hai. Cloudflare host karna ho to Cloudflare Worker account, D1 database aur environment secrets configure karo.

**Snapshot warning:** Ye available saved v18-era code archive hai, **currently deployed latest code ka exact export verified nahi hai**. Newer Shop Now/header animations/navigation/newsletter changes is copy mein missing ho sakte hain. Current live site ko replace karne ke liye latest Sites repository ka source pehle retrieve/compare karo.

## 5) Included source

React, TypeScript, Next-style app routes on Vinext / Vite, Cloudflare Worker, D1/Drizzle schema, pages, UI components, media and project configuration. Public campaign media full ZIP mein included hain; code-only ZIP mein videos deliberately omitted hain.
