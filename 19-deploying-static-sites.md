#### [⇐ Previous](./18-twitter-bootstrap.md) | [Table of Contents](./readme.md) | [Next ⇒](./20-final-project.md)

# Deploying Static Sites

### Objectives

By the end of this chapter, you should be able to:

- Define what a static site is
- Deploy a static website to GitHub pages, BitBalloon or another tool
- Compare and contrast the providers below

### What's a Static Website?

A static website is a website that uses static files (helpful, right?). When your browser requests a file from a static site, that file is delivered exactly as it is stored on the server. As we'll see in the coming weeks, modern web applications tend to be highly _dynamic_ - rather than storing static files on the server, we use the server to generate things like HTML files on the fly. For very basic webpages, though, (e.g. simple personal sites, simple blogs, etc.), static sites are very common.

There are a number of tools you can use to deploy a static site. Here we'll cover two of the most popular options: GitHub Pages and BitBalloon.

### Static Site Providers

#### Using GitHub Pages - [https://pages.github.com/](https://pages.github.com/)

GitHub provides static site hosting services at no charge. You can check out the relevant documentation at [GitHub Pages](https://pages.github.com/), but the setup is relatively straightforward (just watch out for typos!).

There are two ways you can deploy a static site through GitHub Pages: you can create a user site or a project site. Each GitHub account can only have one user site, but you can have as many project sites as you want (one project site per repo you create). If your GitHub user name is _username_, then when you deploy your user site, it will live at _username_.github.io; similarly, if you have a repository called _repository_, you can create a project site for it that will live at _username_.github.io/_repository_.

Another big difference between these two types of sites is the _branching_ used to deploy them. The docs do a great job of walking you through the process of setting up your static site, but here's a brief overview:

##### GitHub Pages: User Site

To create a user site, create a new repository on GitHub and call it _username_.github.io. **Important:** Make sure you spell your username correctly in the repository name! If there's a mismatch, the user site won't work.

Once you've created the repo on GitHub, clone it locally and create an `index.html` file (don't get creative here - make sure the name of your file is `index.html`). Here's one you can use to get started:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>GitHub Pages</title>
</head>
<body>
  <h1>Hello World!</h1>
</body>
</html>
```

Once you've got an `index.html`, add your changes, then commit and push to master. Now when you go to _username_.github.io, you should see your `index.html` file on full display!

##### GitHub Pages: Project Site

Creating a user site is a great option for a personal web page, but what if you have a bunch of interesting things you've built that you'd like to share with potential employers? If you'd like to use GitHub Pages for multiple static sites, _project sites_ are the way to go.

To see how project sites work, create a directory called `project_site`. Insite of this new directory, initialize a git repository and add an `index.html` file. Then, on GitHub, create a repository called `project_site` and push your work up to this remote repo. (This is a great review of the material covered earlier in this unit; if you feel shaky on any of these steps, you should absolutely go back and review.) 

Once your `index.html` file is safely on GitHub, you're ready to create your project page. In order for project pages to work, GitHub expects the code for your project to be on a specific branch, called `gh-pages`. In the terminal, let's create this branch and push it to our remote repository. Since we're using `zsh`, we can complete these tasks as follows:

```bash
gcb gh-pages
git push origin gh-pages
```

To verify that this worked, visit _username_.github.io/project_site. You should see your `index.html` file!

You can have one project site per repository, so if you want some more practice on setting up project sites, just create a clean repository and practice away.

(For more details on setting up a project site, including using some built-in templates, check out the [docs](https://pages.github.com/).)

#### Using BitBalloon - [https://www.bitballoon.com/](https://www.bitballoon.com/)

Using BitBalloon is quite a breeze - simply drag and drop your files and you will quickly have a deployed website. 

### Gotchas with deployment

If you are serving any external files (images/videos/scripts etc.) and are using `http`, you need to change this to `https` to make these files load.

### Exercise

- Deploy the Bootstrap mocks that you just made!

### Additional Resources

#### [⇐ Previous](./18-twitter-bootstrap.md) | [Table of Contents](./readme.md) | [Next ⇒](./20-final-project.md)