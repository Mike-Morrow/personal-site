+++
title = "Deploying Hugo Bear Blog on Netlify"
date = "2025-03-26T13:58:52-04:00"
# description = "documentation for my website"

tags = []
+++

This guide walks through the process of setting up a personal blog using the Hugo Bear Blog theme and deploying it on Netlify.

## 1. Create a New Hugo Site

Start by installing Hugo and creating a new site:

```toml
# Install Hugo (this varies by OS, example using Homebrew on macOS)
brew install hugo

# Create a new site
hugo new site my-bear-blog
cd my-bear-blog
```

## 2. Add the Bear Blog Theme

Add the Bear Blog theme as a git submodule:

```toml
# Initialize git repository
git init

# Add the theme as a submodule
git submodule add https://github.com/janraasch/hugo-bearblog.git themes/hugo-bearblog
```

## 3. Configure Your Site

Create a configuration file in the root directory. You can use either `hugo.toml` (for newer Hugo versions) or `config.toml`:

```toml
baseURL = "/"
languageCode = "en-us"
title = "My Personal Site"
theme = "hugo-bearblog"

# Additional Bear Blog theme settings
[params]
  description = "Your site description"
  author = "Your Name"
```

## 4. Create Content

Add some initial content to your site:

```toml
hugo new posts/my-first-post.md
```

Edit the newly created markdown file in `content/posts/my-first-post.md`.

## 5. Prepare for Netlify Deployment

Create a `netlify.toml` file in your project root:

```toml
[build]
  publish = "public"
  command = "hugo --gc --minify"

[build.environment]
  HUGO_VERSION = "0.123.0"  # Use a recent version (0.110.0 or newer for hugo.toml support)

[context.production.environment]
  HUGO_ENV = "production"
```

> **Note:** If you're using `hugo.toml` instead of `config.toml`, make sure to specify a Hugo version of 0.110.0 or newer in your `netlify.toml` file.

## 6. Set Up a Git Repository

Commit your changes and push to a new GitHub repository:

```toml
# Add all files
git add .
git commit -m "Initial commit with Bear Blog theme"

# Create a repository on GitHub first, then:
git remote add origin https://github.com/yourusername/your-repo-name.git
git branch -M main
git push -u origin main
```

If you get an error that the remote already exists, you can remove it first:

```toml
git remote remove origin
git remote add origin https://github.com/yourusername/your-repo-name.git
```

## 7. Deploy on Netlify

1. Go to [Netlify](https://app.netlify.com/) and log in
2. Click "New site from Git"
3. Select your Git provider (GitHub)
4. Authorize Netlify to access your repositories
5. Select your Hugo Bear Blog repository
6. Netlify should automatically detect Hugo settings from your netlify.toml file
7. Click "Deploy site"

## Troubleshooting

### "Unable to locate config file" Error

If you see an error like "Unable to locate config file or config directory":

1. Check that your config file (`hugo.toml` or `config.toml`) exists in the root directory
2. If using `hugo.toml`, ensure your `netlify.toml` specifies a modern Hugo version (0.110.0+)
3. Verify your repository structure is correct

### Theme Not Found

If Hugo can't find your theme:

1. Check that the theme is correctly referenced in your config file
2. Verify that the theme is properly installed as a submodule
3. Make sure the `.gitmodules` file is committed and pushed

## Additional Customization

To customize your Bear Blog theme:

1. Check the [theme documentation](https://github.com/janraasch/hugo-bearblog)
2. Create or modify content in the `content/` directory
3. Add custom CSS by creating a `assets/css/custom.css` file

## Next Steps

- Set up a custom domain in Netlify settings
- Enable HTTPS
- Add more content to your blog
- Customize the theme to your liking

