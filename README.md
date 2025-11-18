# My Jekyll Blog

A simple, clean blog built with Jekyll for GitHub Pages, inspired by colah.github.io.

## Features

- Clean, minimalist design
- Grid layout for blog posts on the home page
- Responsive design (mobile-friendly)
- Easy to customize
- Ready for GitHub Pages deployment

## Local Development

To run this blog locally:

1. Install Ruby and Bundler if you haven't already
2. Create a `Gemfile` in the project root with the following content:

```ruby
source 'https://rubygems.org'
gem 'github-pages', group: :jekyll_plugins
```

3. Run `bundle install` to install dependencies
4. Run `bundle exec jekyll serve` to start the local server
5. Open your browser to `http://localhost:4000`

## Deploying to GitHub Pages

1. Create a new repository on GitHub named `yourusername.github.io`
2. Push this code to the repository:
   ```bash
   git init
   git add .
   git commit -m "Initial commit"
   git branch -M main
   git remote add origin https://github.com/yourusername/yourusername.github.io.git
   git push -u origin main
   ```
3. Go to your repository settings → Pages
4. Ensure the source is set to deploy from the `main` branch
5. Your site will be live at `https://yourusername.github.io`

## Adding New Blog Posts

1. Create a new file in the `_posts` directory
2. Name it with the format: `YYYY-MM-DD-title-of-post.md`
3. Add the front matter at the top:

```yaml
---
layout: post
title: "Your Post Title"
date: YYYY-MM-DD
image: /assets/images/your-image.jpg
excerpt: "A brief description of your post"
---
```

4. Write your content in Markdown below the front matter

## Customization

- Edit `_config.yml` to change the site title and description
- Modify `assets/css/style.css` to customize the appearance
- Update the colors, fonts, and layouts to match your style

## Adding Images

1. Place images in the `assets/images/` directory
2. Reference them in your posts using: `/assets/images/filename.jpg`
3. Add an `image` field in the post's front matter to show it on the home page

Note: For now, posts without images will show a gradient placeholder.

## Project Structure

```
.
├── _config.yml           # Site configuration
├── _layouts/             # Page layouts
│   ├── default.html     # Base layout
│   └── post.html        # Blog post layout
├── _posts/              # Blog posts
│   ├── 2024-01-15-welcome-to-my-blog.md
│   └── 2024-02-01-understanding-neural-networks.md
├── assets/
│   └── css/
│       └── style.css    # Site styles
├── index.html           # Home page
└── README.md           # This file
```

## License

Feel free to use this template for your own blog!