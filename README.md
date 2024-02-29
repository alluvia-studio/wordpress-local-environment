# A Containerized WordPress Environment for Local Development

## Getting Started

Spin up environment:

```
docker compose up -d
```

Grant permissions to <user> for ./wordpress:

For Linux

```
sudo useradd -G <groupname> <username>
sudo chmod -R g+rwx ./wordpress/
```

For macOS

```
sudo dseditgroup -o edit -a <username> -t user <groupname>
```

Create or copy them project to `./wordpress/wp-content/themes/<theme>`.

Tip: Add a symlink to the `<theme>` at the project's root directory.

Be sure to make your theme project an exception .gitignore

```
# .gitignore

wordpress/*
!wordpress/README.md
!wordpress/wp-content/

wordpress/wp-content/*
!wordpress/wp-content/themes/

wordpress/wp-content/themes/*
!wordpress/wp-content/themes/<theme>
```

To increase the maximum upload file size, make sure to have a copy of `.htaccess` in `./wordpress/` with the contents similar to the following:

```
php_value upload_max_filesize 256M
php_value post_max_size 256M
php_value max_execution_time 300
php_value max_input_time 300
```

## Working with roots/sage & pnpm

### Modify docker-compose.yml

Be sure to use a wordpress image that supports php 8.0 or higher.

```
# image: wordpress:latest
image: wordpress:6.2.0-php8.2
```

### Create a new theme using Sage

Inside `./wordpress/wp-content/themes/`, create a new project using composer:

```
composer create-project roots/sage <theme>
```

### Install Acorn

Move into the theme and install Acorn, which enables the use of Laravel components in WordPress.

```
composer require roots/acorn
```

### Modify Sage config

Remove `./wordpress/wp-content/themes/<theme>/yarn.lock`.
Move or copy `./pnpm_conf/.pnpmfile.cjs` to `./wordpress/wp-content/themes/<theme>/.pnpmfile.cjs`

Install Node modules with `pnpm`

```
pnpm install --public-hoist-pattern=*
```

Ref: `https://bud.js.org/guides/general-use/pnpm#pnpmfilecjs-compatibilty-shim`
