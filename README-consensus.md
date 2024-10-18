1. Steps following instructions from https://www.drupal.org/project/commerce_kickstart:

```
composer create-project -s dev centarro/commerce-kickstart-project ck4
```

2. Update composer.json to incorporate our changes supporting D10 on Aegir 3.

3. For D10.3.6, we had to additionally remove `vendor/symfony/console/Style`, to fix the error message:

> Drush command terminated abnormally due to an unrecoverable error. Error: Declaration of Symfony\Component\Console\Style\OutputStyle::write(iterable|string $messages, bool $newline = false, int $type = self::OUTPUT_NORMAL) must be compatible with Symfony\Component\Console\Output\OutputInterface::write($messages, $newline = false, $options = 0) in /var/aegir/platforms/ck4/vendor/symfony/console/Style/OutputStyle.php, line 49

Our addition to `composer.json`'s `post-install-cmd` and `post-update-cmd` stanzas:

```
rm -rf vendor/symfony/console/Style
```

4. Additionally, remove `vendor/symfony/console/Output`, to address the error message:

> Drush command terminated abnormally due to an unrecoverable error. Error: Declaration of Symfony\Component\Console\Style\OutputStyle::getVerbosity() must be compatible with Symfony\Component\Console\Output\OutputInterface::getVerbosity(): int in /var/aegir/.drush/provision/vendor/symfony/console/Style/OutputStyle.php, line 78

Our addition to `composer.json`'s `post-install-cmd` and `post-update-cmd` stanzas:

```
rm -rf vendor/symfony/console/Output
```

5. Now, we are seeing the following error:

```
Drush command terminated abnormally due to an unrecoverable error. Error: Declaration of Drush\Sql\Sqlmysql::command() must be compatible with Drush\Sql\SqlBase::command(): string in /usr/local/share/drush/lib/Drush/Sql/Sqlmysql.php, line 9
```

