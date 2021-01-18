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

Now CS run on each commit command and check files.

For example you can add tailing space in line

```define( 'WP_USE_THEMES', true ); ```

in your index.php file.
If you try to commit it you can see:

```
$ git add index.php
$ git commit -m "change index.php"
Checking PHP Lint...
No syntax errors detected in /.../index.php
Running Code Sniffer. Code standard WordPress.
E 1 / 1 (100%)



FILE: /.../index.php
----------------------------------------------------------------------
FOUND 1 ERROR AFFECTING 1 LINE
----------------------------------------------------------------------
 14 | ERROR | [x] Whitespace found at end of line
----------------------------------------------------------------------
PHPCBF CAN FIX THE 1 MARKED SNIFF VIOLATIONS AUTOMATICALLY
----------------------------------------------------------------------

Time: 219ms; Memory: 8MB

Fix the error before commit!
Run
  ./vendor/bin/phpcbf --standard=WordPress  /.../index.php
for automatic fix or fix it manually.
```

[Optional] Add in your '.gitignore' the line:

```vendor/```

[Optional] If you need to check not only .php files, please fix the 4th line in pre-commit file to:

STAGED_FILES_CMD=`git diff --cached --name-only --diff-filter=ACMR HEAD | grep \\\\.*`

## References

https://docs.lando.dev/guides/lando-101/lando-tooling.html

https://code.tutsplus.com/tutorials/using-php-codesniffer-with-wordpress-installing-and-using-the-wordpress-rules--cms-26443

https://dev.to/bdelespierre/how-to-setup-git-commit-hooks-for-php-42d1

https://github.com/WickedReports/phpcs-pre-commit-hook
