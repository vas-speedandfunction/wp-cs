# Setup codesniffer (CS) in WordPress projects

Setup CS with composer:

```$ composer require squizlabs/php_codesniffer```

Setup WP coding standards:

```$ composer create-project wp-coding-standards/wpcs:dev-master --no-dev```

Do you want to remove the existing VCS (.git, .svn..) history? [Y,n]?
Answer Y

Make CS to use WP rules:

```$ vendor/bin/phpcs --config-set installed_paths wpcs```

Check codestandarts available in CS:

```$ vendor/bin/phpcs -i```

And you should see the following output (or something very similar):

```The installed coding standards are MySource, PEAR, PHPCS, PSR1, PSR2, Squiz, Zend, WordPress, WordPress-Core, WordPress-Docs, WordPress-Extra and WordPress-VIP```

Put the file 'pre-commit' in '.git/hooks/pre-commit'.

[Optional] Add in your '.gitignore' the line:

```vendor/```

## References

https://docs.lando.dev/guides/lando-101/lando-tooling.html
https://code.tutsplus.com/tutorials/using-php-codesniffer-with-wordpress-installing-and-using-the-wordpress-rules--cms-26443
https://dev.to/bdelespierre/how-to-setup-git-commit-hooks-for-php-42d1
https://github.com/WickedReports/phpcs-pre-commit-hook
