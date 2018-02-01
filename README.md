# [alwaysdata] Autodeploy Git Hook

A simple bash script to deploy on production using Git hooks.

This script simply checkout the last version of a given branch (e.g a _production_ branch) to a working directory. It updates your files and ensure your website / service is properly updated.


## Install

To get it working, create a _bare_ repository on your remote server and place the `post-receive` hook script in its hooks directory:

```shell
$ git init --bare ~/project.git
$ curl -L -o ~/project.git/hooks/post-receive https://raw.githubusercontent.com/alwaysdata/autodeploy-git-hook/master/post-receive
$ chmod +x project.git/hooks/post-receive
```


## Configure

The script embed some variables you need to define to get it working properly. They are declared at the top of the `post-receive` file, feel free to adapt them to your needs:

- `TARGET`: the directory where the files need to be deployed
- `GIT_DIR`: the current git bare repository path
- `BRANCH`: the branch to deploy (default to `production`)

In case you want to restart your app after deploy, you need to fill:

- `RESTART`: a boolean to enable restart (default to `false`)
- `API_KEY`: your api key you can find in your _profile_ section
- `ACCOUNT`: the account name your site is associated to
- `SITE_ID`: the reference ID of your site you can find in your _sites_ section


## Use

In your local repository, simply define a new remote, then push your _production_ (or the branch you set in config) to this remote:

```shell
$ cd project
$ git remote add deploy <account>@ssh-<account>.alwaysdata.net:~/project.git
$ git checkout production
$ git push deploy production
```

The script logs actions in your git terminal, so the Git `push` action will show you that your deploy is OK or not.


## Contribute

Feel free to contribute to the project by opening pull-requests, or fill issues that will let us improve it. Thanks :beers: !


## LICENSE

Release under [MIT LICENSE].


For more information, you can take a look at our blog post about [how to deploy using Git Hooks].

[alwaysdata]: https://www.alwaysdata.com
[how to deploy using git hooks]: https://blog.alwaysdata.com/
[mit license]: ./LICENSE
