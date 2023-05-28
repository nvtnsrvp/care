### SET UP

```
# Install `node` and `npm`
brew install node

# Install `postgres` and set up a local postgres instance.
brew install postgresql
brew services start postgresql
# Optionally run `brew services stop postgresql` and then restart if start fails.
# Create database:
createdb core
# Log in and log out with <ctrl>-d
psql -d core

# Set up the (very simple) database schema.
psql -d core < model/schema/roles.sql
psql -d core < model/schema/core.sql

```

#### `nginx`

`nginx` is a "reverse proxy", which means that it allows you to manage incoming http requests in a variety of highly useful ways. In our case, we'll be running our backend server on port 3000, and will use `nginx` to redirect port 80 there (i.e., so that we can reference http://localhost instead of http://localhost:3000). The nice thing about `nginx` (particularly in comparison to `apache`) is that its configuration files are typically fairly straightforward.

```
brew install nginx
cp conf/nginx.conf /usr/local/etc/nginx
# NOTE: you will need to alter the "root" variable in nginx.conf to point to the right directory for your system
sudo nginx
```

#### `nodemon`

`nodemon` will manage our `node` process - restarting it when necessary, and watching for code changes.

```
npm install nodemon -g
```