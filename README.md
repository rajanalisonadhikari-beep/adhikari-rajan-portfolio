# Rajan Adhikari — Portfolio Website

A clean, fast portfolio website with a built-in admin panel at **/admin**.
No database, no server to manage. When you edit content in the admin panel it
saves straight into these files and Netlify re-publishes the site automatically.

## What's inside

```
index.html          → the whole website (one page)
css/styles.css      → styling
js/main.js          → loads your content from the /content files
content/
  site.json         → your name, tagline, about text, contact info
  ventures.json     → your businesses (treks, barbershop, imports)
  blog.json         → blog posts
admin/
  index.html        → the admin panel (Decap CMS)
  config.yml        → what you can edit in the admin panel
images/uploads/     → photos you upload from the admin panel land here
netlify.toml        → Netlify settings
```

You never *have* to touch the code. Everything on the site is editable from
`adhikari-rajan.com.np/admin`.

---

## One-time setup (about 15 minutes)

Do these steps in order. You only do this once.

### 1. Put these files on GitHub
1. Go to https://github.com/new and create a **new empty repository**
   (name it e.g. `adhikari-rajan-portfolio`). Leave it Public. Don't add a README.
2. On the new repo page click **uploading an existing file**.
3. Drag in **all the files and folders** from this download (keep the folder
   structure) and click **Commit changes**.

### 2. Connect it to Netlify
1. Go to https://app.netlify.com and sign up / log in (you can log in with GitHub).
2. Click **Add new site → Import an existing project → GitHub**.
3. Pick the repo you just created. Leave build settings empty (this is a static
   site) and click **Deploy**.
4. In a few seconds you'll get a live URL like `random-name.netlify.app`. Open it
   — your site is live already.

### 3. Turn on the admin panel login (Netlify Identity + Git Gateway)
The admin panel needs to know who is allowed to log in.
1. In your Netlify site dashboard, go to **Integrations / Identity** (newer
   accounts: **Site configuration → Identity**) and click **Enable Identity**.
2. Under Identity settings:
   - **Registration** → set to **Invite only** (so only you can log in).
   - Scroll to **Services → Git Gateway** and click **Enable Git Gateway**.
3. Go to the **Identity** tab → **Invite users** → enter your email → send.
4. Check your email, click the invite link, and set a password.
   - If the link opens the live site instead of a password box, add `/admin/` to
     the end of the URL and paste the invite token there.

Now visit `your-site.netlify.app/admin/` and log in. You can edit everything.

### 4. Connect your domain adhikari-rajan.com.np
1. First, in your current host (GitHub Pages), the domain is pointed there —
   you'll re-point it to Netlify.
2. In Netlify: **Domain management → Add a domain** → type `adhikari-rajan.com.np`.
3. Netlify shows you DNS records to set. Log in to wherever you bought the domain
   (your domain registrar) and either:
   - **Easiest:** change the nameservers to the ones Netlify gives you, **or**
   - Add the **A record** / **CNAME** records exactly as Netlify lists them.
4. Also add `www.adhikari-rajan.com.np` if you want the www version to work.
5. Wait for it to verify (can take from a few minutes up to a few hours). Netlify
   will automatically issue a free HTTPS certificate.

> Note: because the domain currently points to GitHub Pages, you must change it
> at your registrar so it points to Netlify instead. Only one host can "own" the
> domain at a time.

### 5. Done
From now on:
- Edit content at **adhikari-rajan.com.np/admin/**
- Click **Publish** — the change appears on the live site within ~1 minute.

---

## Tips
- **Add your photo:** admin → Home & About → Profile Photo → upload.
- **Add/remove a business:** admin → Ventures → add or delete an item.
- **Write a blog post:** admin → Blog → add a post.
- If a change doesn't show up, wait a minute then hard-refresh (Ctrl/Cmd+Shift+R).

## Want a custom OAuth login instead of Netlify Identity?
Not needed — Netlify Identity is the simplest and is what the setup above uses.
