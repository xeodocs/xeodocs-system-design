---
title: Architecture and Components
description: Backend API, CLI, git strategy, and special file management.
---

## 1. Backend & API

- **Source of Truth:** The database maintains the state of each file (`pending`, `translated`, `outdated`).
- **REST API:** Provides endpoints for the CLI and Frontend to query project status and report progress.
- **Authentication:**
  - Administrators authenticate via username/password; internally uses JWT stored in HTTPOnly Secure Cookies.
  - XeoDocs CLI authenticates via an API Key assigned to an administrator.
- **Dashboard:** Requires endpoints for status data and relevant updates.
- **CRUD:** Requires CRUD endpoints for all system resources.

## 2. XeoDocs-CLI (Translator's Local Tool)

A lightweight tool developed in Go installed in the translator's local environment. Its function is to abstract Git complexity and generate context for the AI "on the fly".

- **Key Commands:** `xeodocs login`, `xeodocs clone`, `xeodocs sync`, `xeodocs status`, `xeodocs list`, `xeodocs next`, `xeodocs submit`, `xeodocs logout`, `xeodocs --help`, `xeodocs --version`.

## 3. Git Repository Strategy

- **`main` Branch:** Exact mirror of the *upstream* (English/original).
- **`[lang_code]` Branch:** Production branch for the target language (e.g., Spanish).
- **`local-[lang_code]` Branch:** Translator's working branch.

## 4. Special File Management

Configuration resides primarily in the Database, and the API and XeoDocs CLI consider them automatically.

- **Ignored Files:** Functionality similar to `.gitignore` but used to ignore files and directories for translation.
- **Special Editing Files:** (e.g., disabling Analytics). These rules are configured in the Admin Panel, and `xeodocs-cli` can inject specific *prompts* to remind the AI to apply them.

## 5. Additional System Features

- **XeoDocs CLI** provides a prompt to insert the script that loads a floating XeoDocs Toolbar.
- **XeoDocs CLI** provides a prompt to create or update, in the root of the website's public directory, a translation metadata file for consumption by the XeoDocs Toolbar.
- **XeoDocs CLI** provides a prompt to insert banners in the content, identified for future replacement if necessary.

## 6. Configuration

### Administrator Configuration
- Stored in a database table as key/value records.
- Primarily used by the Admin Panel frontend to store Administrator preferences (e.g., theme, table columns, sorting).

### System Configuration
- Stored in a database table as key/value records.
- Used to store general configuration values, such as prompt templates.
