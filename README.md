# Bitbucket Pipelines PHP 7.0 image

[![](https://images.microbadger.com/badges/version/edbizarro/bitbucket-pipelines-php7.svg)](https://microbadger.com/images/edbizarro/bitbucket-pipelines-php7 "Get your own version badge on microbadger.com") [![](https://images.microbadger.com/badges/image/edbizarro/bitbucket-pipelines-php7.svg)](https://microbadger.com/images/edbizarro/bitbucket-pipelines-php7 "Get your own image badge on microbadger.com")

[![forthebadge](http://forthebadge.com/images/badges/fuck-it-ship-it.svg)](http://forthebadge.com)

## Based on [Official PHP image](https://hub.docker.com/_/php/)

### Packages installed

- PHP 7.0 with `mcrypt`, `mongod`, `xdebug`, `zip`, `xml`, `mbstring`, `curl`, `json`, `imap`, `mysql`, `iconv`, `gd`, `pdo_mysql`, `opcache`, `intl`. `zip`, `bcmath` and `tokenizer`
- [Composer](https://getcomposer.org/)
- Node 7.x / NPM / Gulp / [Yarn](yarnpkg.com)
- Mysql 5.7

### `bitbucket-pipelines.yml` for test PHP

```YAML
image: edbizarro/bitbucket-pipelines-php7
pipelines:
  default:
    - step:
        script:
          - service mysql start # We need this here because bitbucket don't have MySQL service :/
          - mysql -h localhost -u root -proot -e "CREATE DATABASE test;"
          - composer install --no-interaction --no-progress --prefer-dist
          - yarn
          - gulp
          - ./vendor/phpunit/phpunit/phpunit -v --coverage-text --colors=never --stderr
```
