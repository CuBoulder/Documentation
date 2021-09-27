# Alerts

## Performing Updates

1. Clone usb-d9-alerts down
```
git clone <git link from Pantheon>
```

2. Perform initial backups
```
terminus backup:create ucb-d9-alerts.dev --element all
terminus backup:create ucb-d9-alerts.prod --element all
```

3. Composer update

```
composer update
```

4. Add, commit, and push updates to repo
```
git add -A
git commit -m "Composer update"
git push
```

5. Perform DB updates and clear cache

```
terminus drush -- updb -y
terminus drush -- cr
```

6. Log in and confirm updated site is working as expected.

```
terminus drush -- uli
```

7. Perform final backups
```
terminus backup:create ucb-d9-alerts.dev --element all
terminus backup:create ucb-d9-alerts.prod --element all
```
