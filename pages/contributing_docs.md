---
id: contributing_docs
title: Contributing To This Documentation
sidebar: sidebar
permalink: contributing_docs.html
folder: pages
summary: This section exlains how to contribute to these docs.
---

## Introduction

These docs are made using [Jekyll](https://jekyllrb.com).

These docs use the theme created by [tomjoht](https://github.com/tomjoht/documentation-theme-jekyll).

## Setting Up The Docs Locally

If you would like to run the doc site locally, follow these steps.

Running the doc site locally allows you to see any changes you make before pushing to git:

1. Install [Jekyll](https://jekyllrb.com)
2. Clone this repository
3. `cd` into the folder containing the `Gemfile`
4. Run `bundle exec jekyll serve --baseUrl ""` to start the Jekyll server
5. Go to http://localhost:4000 and you should see the documentation site running locally

## How to Add Pages

Contributing to the docs generally consists of two steps:

1. Create a markdown page in the `/pages/` folder
2. Make sure to give the page an appropriate `key: value` pairs (i.e. `id`, `folder`, etc.) at the top of the page. You can check the existing pages for examples.
3. Next, open `_data/sidebars/sidebar.yml`
4. In this file, you will need to add the page you created to the sidebar. This ensures the page you created appears in the right place. You can take a look at existing pages to get an idea.
