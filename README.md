### Forked in order to add graphicsmagick to the image


## Features:

 * Meteor 1.x package/bundle support
 * Git-based repository + branch/tag via environment variables (`REPO` and `BRANCH`)
 * Bundle URL via environment variable (`BUNDLE_URL`)
 * Bind-mount, volume, Dockerfile `ADD` via environment variable (`APP_DIR`)
 * Uses docker-linked MongoDB (i.e. `MONGO_PORT`...) or explicit setting via environment variable (`MONGO_URL`)
 * NOTE: This does NOT set `MONGO_OPLOG_URL`.  There were too many potention complications.  As a result, unless you explicitly set `MONGO_OPLOG_URL`, Meteor will fall back to a polling-based approach to database synchronization.  Note that oplog tailing requires a working replica set on your MongoDB server as well as access to the `local` database.
 * Optionally specify the port on which the web server should run (`PORT`); defaults to 80
 * Deploy-key support (set `DEPLOY_KEY` to the location of your SSH key file)
   * old `GITHUB_DEPLOY_KEY` is also supported but deprecated
 * Non-root location of Meteor tree; the script will search for the first .meteor directory
 * _NOTE_: PhantomJS is no longer pre-installed.  This package was swelling the size of the image by 50%, and it is not maintainable with the standard Docker Node images.  Instead, please use one of the docker-friendly (read port-based) spiderable packages on Meteor, such as `ongoworks:spiderable`;  if there is demand, please create an issue on Github, and I'll see about managing a separate branch for it.

## Versions:

Regardless of the version number of the tool included in this package, your application will run
on whatever version of Meteor it is configured to run under.

## Examples:

### git repo with non-default (master) branch
`docker run --rm -e ROOT_URL=http://testsite.com -e REPO=https://github.com/yourName/testsite -e BRANCH=testing -e MONGO_URL=mongodb://mymongoserver.com:27017 ulexus/meteor`

### local directory on host (/home/user/myapp)
`docker run --rm -e ROOT_URL=http://testsite.com -e APP_DIR=/app -v /home/user/myapp:/app -e MONGO_URL=mongodb:/mymongoserver.com:27017 ulexus/meteor`

### Unit file

There is also a sample systemd [unit file](meteor@.service) in the Github repository.

