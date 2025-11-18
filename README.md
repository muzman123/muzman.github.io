# My GitHub Pages Blog

A simple, clean blog built with pure HTML/CSS and Bootstrap, inspired by [colah.github.io](https://colah.github.io/).

## Features

- Clean, minimalist design inspired by colah's blog
- Bootstrap 5 for responsive layout
- Each blog post is a folder with its own `index.html`
- Grid layout for blog posts on the home page
- Easy to customize and extend
- Ready for GitHub Pages deployment (no build process needed!)

## Structure

```
.
├── index.html              # Home page with post grid
├── about.html              # About page
├── css/
│   └── style.css          # Custom styles
├── images/
│   └── post-covers/       # Post cover images
├── posts/
│   ├── understanding-neural-networks/
│   │   └── index.html     # Individual post
│   ├── welcome-to-my-blog/
│   │   └── index.html     # Individual post
│   └── getting-started/
│       └── index.html     # Individual post
└── README.md
```

## How It Works

Unlike Jekyll-based blogs, this is a pure HTML/CSS site:
- **No build process** - Just HTML, CSS, and Bootstrap
- **Each post is a folder** - Contains `index.html` and any assets (images, etc.)
- **Simple navigation** - Direct links between pages
- **GitHub Pages ready** - Push and it works immediately

## Adding a New Blog Post

1. Create a new folder in the `posts/` directory:
   ```
   posts/my-new-post/
   ```

2. Copy an existing post's `index.html` as a template:
   ```bash
   cp posts/welcome-to-my-blog/index.html posts/my-new-post/index.html
   ```

3. Edit the new `index.html`:
   - Update the `<title>` tag
   - Update the `<h1>` heading
   - Update the post date
   - Write your content in the `<div class="post-body">` section

4. Add a cover image (optional):
   - Place image in `images/post-covers/`
   - Name it descriptively (e.g., `my-new-post.jpg`)

5. Add the post to the home page grid:
   - Open `index.html`
   - Add a new post card in the `<div id="posts-grid">` section:
   ```html
   <div class="col-md-4">
       <a href="posts/my-new-post/" class="text-decoration-none">
           <div class="post-card">
               <div class="post-image">
                   <img src="images/post-covers/my-new-post.jpg" alt="My New Post">
               </div>
               <div class="post-content">
                   <h3>My New Post Title</h3>
                   <p class="post-excerpt">A brief description of the post.</p>
               </div>
           </div>
       </a>
   </div>
   ```

## Deploying to GitHub Pages

### Method 1: GitHub Pages (Recommended)

1. Create a repository on GitHub named `yourusername.github.io`

2. Push this code to the repository:
   ```bash
   git init
   git add .
   git commit -m "Initial blog setup"
   git branch -M main
   git remote add origin https://github.com/yourusername/yourusername.github.io.git
   git push -u origin main
   ```

3. Your site will automatically be live at `https://yourusername.github.io`

### Method 2: Project Page

If you don't want to use the `username.github.io` format:

1. Create any repository (e.g., `my-blog`)
2. Push your code
3. Go to Settings → Pages
4. Select branch `main` and folder `/` (root)
5. Your site will be at `https://yourusername.github.io/my-blog`

   **Note:** If using a project page, update all paths in your HTML files:
   - Change `href="./css/style.css"` to `href="./my-blog/css/style.css"`
   - Change `href="./"` to `href="./my-blog/"`
   - And so on for all relative paths

## Customization

### Change Site Title and Description

Edit the following in each HTML file:
- `<title>` tags
- Navigation brand: `<a class="navbar-brand">`
- Update the home page heading in `index.html`

### Customize Colors

Edit `css/style.css`:
- Change the gradient in `.post-image` for default post covers
- Modify navbar color (`.bg-dark`)
- Adjust link colors
- Change fonts (update Google Fonts links)

### Add More Pages

1. Create a new HTML file in the root directory (e.g., `contact.html`)
2. Copy the structure from `about.html`
3. Add a link to the navbar in all pages:
   ```html
   <li class="nav-item">
       <a class="nav-link" href="./contact.html">Contact</a>
   </li>
   ```

## Tips

- **Images**: Use optimized images (JPG for photos, PNG for graphics)
- **Responsive**: The site is mobile-friendly thanks to Bootstrap
- **No Jekyll**: Unlike the original colah.github.io, this doesn't use Jekyll, so it's simpler but requires manual updates
- **Fast Loading**: Pure HTML/CSS loads instantly

## Differences from Jekyll-based Blogs

**Advantages:**
- No build process or dependencies
- Instant updates (no waiting for Jekyll to build)
- Full control over HTML structure
- Easy to understand and modify

**Tradeoffs:**
- Manual updates to index.html for new posts
- No automatic post listings or tags
- No markdown support (pure HTML)

## Converting from Jekyll

If you want to use Jekyll (like the original colah.github.io), you can:
1. See the `_layouts/`, `_posts/`, and `_config.yml` files included in this repo
2. Install Ruby and run `bundle install`
3. Run `bundle exec jekyll serve` to build locally
4. Those files show how to set up Jekyll, but the simple HTML version is easier to start with

## License

Feel free to use this template for your own blog!