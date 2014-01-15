Protocol
========

A guide for getting things done.

Set up laptop
-------------

Install the latest version of Xcode from the App Store.

Set up your laptop with [this script](https://github.com/thoughtbot/laptop)
and [these dotfiles](https://github.com/thoughtbot/dotfiles).

Create Rails app
----------------

Get Suspenders.

    gem install suspenders

Create the app.

    suspenders app --heroku true --github organization/app

Create iOS app
--------------

Create a new project in Xcode with these settings:

* Check 'Create local git repository for this project'.
* Check 'Use Automatic Reference Counting'.
* Set an appropriate 2 or 3 letter class prefix.
* Set the Base SDK to 'Latest iOS'.
* Set the iOS Deployment Target to 6.0.
* Use the Apple LLVM compiler.

Get liftoff.

    gem install liftoff

Run liftoff in the project directory.

    liftoff

Set up Rails app
----------------

Get the code.

    git clone git@github.com:organization/app.git

Set up the app's dependencies.

    cd project
    ./bin/setup

Use [Heroku config](https://github.com/ddollar/heroku-config) to get `ENV`
variables.

    heroku config:pull --remote staging

Delete extra lines in `.env`, leaving only those needed for app to function
properly. For example: `BRAINTREE_MERCHANT_ID` and `S3_SECRET`.

Use [Powder](https://github.com/Rodreegez/powder) to run the app locally.

    powder link
    powder open

It uses [Pow](http://pow.cx/), [Foreman](https://github.com/ddollar/foreman), your `.env` file and `Procfile` to run processes just like Heroku's
[Cedar](https://devcenter.heroku.com/articles/cedar/) stack.

Maintain a Rails app
--------------------

* Avoid including files in source control that are specific to your
  development machine or process.
* Delete local and remote feature branches after merging.
* Perform work in a feature branch.
* Merge frequently to incorporate upstream changes.
* Use a [pull request] for code reviews.

[pull request]: https://help.github.com/articles/using-pull-requests/

Write a feature
---------------

Create a local feature branch based off master.

    git checkout master
    git pull
    git checkout -b <branch-name>

Prefix the branch name with your initials.  The rest of the name should be 
related to what is being done: 'jk-upgrading-rails-4-2'

Merge frequently to incorporate upstream changes.

    git fetch origin
    git merge origin/master

Resolve conflicts. When feature is complete and tests pass, stage the changes.

    rake
    git add --all

When you've staged the changes, commit them.  Use git has a journal.  Commit early and often.

    git status
    git commit --verbose

Write a [good commit message]. Example format:

    Present-tense summary under 50 characters

    * More information about commit (under 72 characters).
    * More information about commit (under 72 characters).

    http:://project.management-system.com/ticket/123

Share your branch.

    git push origin <branch-name>

Submit a [GitHub pull request].

Ask for a code review in [Campfire](https://campfirenow.com/).

[good commit message]: http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html
[GitHub pull request]: https://help.github.com/articles/using-pull-requests/

Review code
-----------

A team member other than the author reviews the pull request. They follow
[Code Review](../code-review) guidelines to avoid
miscommunication.

They make comments and ask questions directly on lines of code in the Github
web interface or in Campfire.

For changes which they can make themselves, they check out the branch.

    git checkout <branch-name>
    rake db:migrate
    rake
    git diff staging/master..HEAD

They make small changes right in the branch, test the feature in browser,
run tests, commit, and push.

When satisfied, they comment on the pull request `Ready to merge.`

Merge
-----

Use Github to merge the pull request.

Use Github to delete the feature branch after merging.

Prune non-existant remote branches

    git fetch -p

Delete your local feature branch.

    git branch --delete <branch-name>

Deploy
------

View a list of new commits. View changed files. Deploy to
[Heroku](https://devcenter.heroku.com/articles/quickstart) staging.

    <TBD>

[Introspect](http://blog.heroku.com/archives/2011/6/24/the_new_heroku_3_visibility_introspection/) to make sure everything's ok.

    watch heroku ps --remote staging

Test the feature in browser.

Deploy to production.

    <TBD>

Watch logs and metrics dashboards.


Set Up Production Environment
-----------------------------

* Make sure that your [`Procfile`] is set up to run Unicorn.
* Make sure the PG Backups add-on is enabled.
* Create a read-only [Heroku Follower] for your production database. If a Heroku
  database outage occurs, Heroku can use the follower to get your app back up
  and running faster.

[Heroku Follower]: https://devcenter.heroku.com/articles/improving-heroku-postgres-availability-with-followers
[`Procfile`]: https://devcenter.heroku.com/articles/procfile
