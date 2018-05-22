Showoff
=======


[Showoff](https://github.com/puppetlabs/showoff) is presentation software for developer advocates. This is an example presentation using the IBM Code branding. Use this example to make your own IBM Code presentations.

Showoff runs as a server on your computer, then you present the slides from a web browser at [http://localhost:9090](http://localhost:9090). Attendees (if you allow them) can access your slides directly from the server on your laptop. You can also push your slides to github pages so everyone has access to them immediately.

Showoff has native support for code snippets with syntax highlighting, terminal session replay, and code driven diagrams. Showoff presentations are entirely plaintext, so they are easy to track using git. This presents a serious improvement over powerpoint.


Making a new presentation
=========================


Use these steps to make a new presentation called 'serverless-tutorial'

```shell
git clone git@github.ibm.com:skrum/ibm-showoff.git
mv ibm-showoff serverless-tutorial
git remote rm origin # this removes tracking of the template repo
# Make a new repository
git remote add https://github.com/ibm/serverless-tutorial
vim showoff.json # select which directories you want in the presentation, in what order
vim introduction/00_section.md  # Edit title slide
vim introduction/01_section.md # Edit rest of presentation
```


Showoff Authoring
-----------------


Showoff uses mostly Markdown formatting, which will be familiar if you're used to writing github readmes. See this example presentation for examples of how to make slides that pop. You also have full CSS control if you're web inclined. See styles.css for examples.



Examples:
---------


* https://github.ibm.com/skrum/talk_2018_k8s_and_istio_at_lfnw
* https://github.com/eggshell/rotisserie-talk/


Quickstart
----------


```shell
gem install showoff
showoff serve
```

Or you can use the executable [docker image](https://github.com/nibalizer/docker-showoff) already preloaded with showoff.



Publishing to GitHub Pages
---------------------------

If you would like to have a backup link to your presentation and not rely on
serving your presentation locally from your laptop, you can easily publish your
showoff presentation to GitHub Pages. Follow these steps once you have a version
of your presentation that your are happy with:

* Generate a static version of your presentation:

```shell
showoff github
```

* Create a branch called `gh-pages` off of `master`:

```shell
git checkout -b gh-pages
```

* Push your local `gh-pages` branch to a remote branch on GitHub:

```shell
git push origin gh-pages
```

That's it. A static version of your presentation is now viewable at
`https://YOUR_GITHUB_USERNAME.github.io/YOUR_PRESENTATION_REPO_NAME`. Note that
if you have a custom domain set up, that will be used instead of the default
github.io domain.



Contributing Back
-----------------

It not necessary to pull request into this repository. Your slides and content should live in the repository for the talk you are preparing. However, you can and should contribute back to this repository if you have made more css changes, or have examples of slides that are not currently covered in the examples in this repository. Construct the pull request in any way that makes sense for you, or just ping Spencer Krum on slack/twitter and he'll help you get your code in.

