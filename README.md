# Hi there

This is the source code for my personal blog built with [Hexo](https://hexo.io/) and using a customized version of the [Cactus](https://github.com/probberechts/hexo-theme-cactus) theme, added as a Git submodule.

## 🚀 Cloning the Repository

Since this project uses a submodule for the theme, make sure to **clone it recursively**:

```bash
git clone --recurse-submodules https://github.com/your-username/your-blog-repo.git
cd your-blog-repo
```

If you already cloned it without `--recurse-submodules`, run:

```bash
git submodule update --init --recursive
```

## 📝 Creating a New Post

To create a new blog post, run:

```bash
npx hexo new "your-post-title"
```

For example:

```bash
npx hexo new "Getting Started with Hexo"
```

This will create a new Markdown file under the `source/_posts/` directory. You can then edit the file and write your content in Markdown.

## 🎨 Updating the Theme (Cactus Submodule)

If you want to apply updates from your customized theme repo, run:

```bash
cd themes/cactus
git pull origin main
cd ../..
```

Then commit the updated submodule reference:

```bash
git add themes/cactus
git commit -m "Update cactus theme submodule"
git push
```

## 🧪 Local Development

To preview your blog locally:

```bash
npm install
npx hexo serve
```

Then open http://localhost:4000 in your browser.