---
layout: post
title:  "Enable Blogging Capabilities with Material for MkDocs"
date:   2021-11-02 10:41:08 +0300
categories: dirigible
icon: fa-check
hide: true
---
In this blog, we're going to discuss how to add blogging capabilities to [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/). Here's what we refer to as blogging capabilities: 

- author's GitHub avatar, name, and link to GitHub profile
- a calendar icon with a publishing date next to it
- a clock icon with a value for time to read next to it

You can also see the above mentioned capabilities under the title of this blog.

In particular, we'll look at:

- What kind of metadata key-value pairs you need to define in your `.md` file and how.
- How to override a specific block in the `main.html` file that [MkDocs](https://www.mkdocs.org/) uses as a template when building the HTML output from your `.md` source, so that the metadata values provided in your `.md` file are reflected in the HTML output.


As a result, a blog author will just have to provide sufficient metadata in the frontmatter of their `.md` file and data about author, publishing date, and reading time will be displayed as part of their blog. Cool, right?

> This can also be done manually by including a piece of HTML code in each `.md` file but we wanted to have everything set up for blog authors in a way that they can focus on the writing itself.

### Adding Metadata to Your Blog

Metadata about an `.md` file (also called frontmatter) is declared within a specific block in the beginning of the `.md` file itself and is denoted by the triple dashes at the start and end of the block. Usually, the metadata is not processed when generating HTML output from the `.md` file. With MkDocs, metadata can be displayed on the page or used to control the page rendering, but only if this is supported by the theme you're using with MkDocs. For more details, checkout the [MkDocs documentation](https://www.mkdocs.org/user-guide/writing-your-docs/#meta-data).

We have to determine what metadata key-value pairs are needed for the blogging capabilities. As mentioned above, we want to have name, GitHub avatar, and link to GitHub profile of the author, as well as publishing date and reading time. 

Open your `.md` file and add the following lines:

```yaml
---
author: <Your Name>
author_gh_user: <Your GitHub User>
read_time: <Reading Time>
publish_date: <Date of Publishing>
---
```
It's quite self-explanatory which metadata key-value pairs are responsible for which of the blogging capabilities. You can find more details in step 5 of [Overriding the Content Block](#overriding-the-content-block). The more interesting one is `author_gh_user`. This value will be used for both getting the author's GitHub avatar and creating a hyperlink to their GitHub profile. 

> Setting the title in the metadata will help position the blogging capabilities in the right place - under the title and before the rest of your blog.

>   ```title: <Your Blog Title>```

>   When the title is set in the metadata, use ``Heading 2`` level (`## This is a heading 2`) as the highest heading level in your blog. Otherwise, the first `Heading 1` you use will overwrite the title from the frontmatter and cause formatting issues.

