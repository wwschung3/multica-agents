---
name: understand-project-lpmm2
description: Use this skill when working with the lpmm2 Magento2 project
---

This repo is only part of the Magento2 system.

## Key Information

- The actual system runs in Docker container `lpmm2-server`
- To run code or tests (unit tests, integration tests, etc.), it must be run inside the container
- PHP is installed inside the container, not on the host

## How to Run Commands

- All PHP commands must be executed inside the Docker container `lpmm2-server`
- Use `docker exec` to run commands inside the container
- Do NOT try to run PHP commands on the host machine