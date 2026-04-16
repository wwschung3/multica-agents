---
name: test-lpmm2
description: "Used to run unit tests or integration tests for the lpmm2 Magento 2 project."
---

# Skill: Testing lpmm2 Project (test-lpmm2)

Used to run unit tests or integration tests for the lpmm2 project.

## When to Use

- When running unit tests for Lpm modules.
- When running integration tests for Lpm modules.
- When needing to set up the integration test environment.
- When debugging test execution issues.

## Common Triggers

- test lpmm2
- run unit test
- run integration test
- phpunit lpmm2
- test Lpm modules

## Unit Testing

### Run All Unit Tests

```bash
vendor/bin/phpunit --configuration app/code/Lpm/phpunit_unit.xml
```

### Run Tests for Specific Module

```bash
vendor/bin/phpunit --configuration app/code/Lpm/phpunit_unit.xml app/code/Lpm/<ModulePath>/Test/Unit/
```

### Run a Specific Test File

```bash
vendor/bin/phpunit --configuration app/code/Lpm/phpunit_unit.xml app/code/Lpm/<ModulePath>/Test/Unit/Model/CustomTest.php
```

## Integration Testing

### Setup

1. Check `app/code/Lpm/phpunit_integration.xml`
2. Seek dev team for `install-config-mysql-lpm-local.php.dist` file, place it in `dev/tests/integration/etc/install-config-mysql-lpm-local.php`
3. Login db as root, create magento_integration_tests database:

```sql
CREATE DATABASE IF NOT EXISTS magento_integration_tests CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
GRANT PROCESS ON *.* TO 'dbuser'@'%';
GRANT ALL PRIVILEGES ON magento_integration_tests.* TO 'dbuser'@'%';
FLUSH PRIVILEGES;
SET GLOBAL log_bin_trust_function_creators = 1;
```

4. Duplicate the local lpm db to magento_integration_tests:

```bash
mysqldump -u dbuser -p{MYSQL_MAIN_PASSWORD} lpm | mysql -u dbuser -p{MYSQL_MAIN_PASSWORD} magento_integration_tests
```

### Run Tests

#### Run All Integration Tests

```bash
vendor/bin/phpunit --configuration app/code/Lpm/phpunit_integration.xml
```

#### Run Integration Tests for Specific Module

```bash
vendor/bin/phpunit --configuration app/code/Lpm/phpunit_integration.xml app/code/Lpm/<ModulePath>/Test/Integration/
```

#### Run a Specific Integration Test File

```bash
vendor/bin/phpunit --configuration app/code/Lpm/phpunit_integration.xml app/code/Lpm/<ModulePath>/Test/Integration/Model/CustomTest.php
```

## Debug

- Check for existence of `dev/tests/integration/etc/install-config-mysql-lpm-local.php`
- If db dump is not needed, ensure the `setup_dump_lpm_test.sql` file exists in `dev/tests/integration/tmp/sandbox-xxxx`, and the file is empty.

## Quick Reference

| Test Type | Configuration File |
|----------|-----------------|
| Unit | `app/code/Lpm/phpunit_unit.xml` |
| Integration | `app/code/Lpm/phpunit_integration.xml` |