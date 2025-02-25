---
title: Quick Start
subtitle: Clone Live to Dev
description: In part six of our Quick Start guide, learn how to clone your content from Live to Dev.
contenttype: [guide]
innav: [false]
categories: [overview]
cms: [--]
audience: [development]
product: [--]
integration: [--]
tags: [dashboard, iterate, launch, webops, workflow]
showtoc: true
permalink: docs/guides/quickstart/clone-live-to-dev/
anchorid: clone-live-to-dev
editpath: quickstart/06-clone-live-to-dev.md
---

In this lesson, we’ll explore your Live site and add an article or post to simulate working on a real production site. Then we’ll clone your Live site “down” to your Dev site.

## Create an Article on the Site

1. Click the <Icon icon="new-window-alt" text="Site Admin"/> button to open your Live site in a new tab. You’ll need to log in before being directed to the site administration dashboard.

    <Alert title="Note" type="info">
      Your WordPress or Drupal username and password are the same set you
      created when you installed your Dev site for the first time.
    </Alert>

1. Create a new Drupal article or WordPress post. If you need help with this step, refer to the [WordPress Codex](https://codex.wordpress.org/Posts) or [Drupal Documentation](https://www.drupal.org/docs/8/administering-drupal-8-site/managing-content/) on how to add a post or article. When finished, visit the front page of your site and confirm that you can see the new content.

## Pull the Content Down to Dev (Clone Live to Dev)

1. Go back to your **Site Dashboard**, click the <Icon icon="wrench" text="Dev"/> tab, and open your Dev site by clicking <Icon icon="new-window-alt" text="Visit Development Site"/>.

    Notice that the content you just created on your Live site doesn’t appear on your Dev site. This is because each environment is a stand-alone copy of your site, with its own codebase, database, and files.

    It’s important to develop on a recent copy of your site with the newest content, so let’s clone your Live site—with its new content—to your Dev environment.

1. Consider creating a backup before proceeding. After the next step, you will not be able to recover Dev database and files without a backup:

    <Accordion id="create-backup" title="Create Backup (optional)">

    The Backups tab is where you manage all the details for your site's backup. A backup is composed of 3 separate archives for database, files, and code. Let’s create a backup now:

    1. Click <Icon icon="cloud-upload" text="Backups"/> on the <Icon icon="wrench" text="Dev"/> tab of your Site Dashboard.
    2. Click **Create New Backup**.

    </Accordion>

1. Navigate to your Site Dashboard, select the <Icon icon="wrench" text="Dev"/> tab, and then click <Icon icon="server" text="Database / Files"/>.

1. Select **Live** from the **From this Environment** list to clone the database and files from the Live site. 

    <Alert type="danger" title="Warning">

    As intended, this action will overwrite your Dev database and files. If you skipped the backup task you will be unable to recover this data hereafter.

    The Clone operation only copies the [files](/guides/filesystem) folder (`wp-content/uploads` or `sites/default/files`) and does not include core, theme, plugins or modules.

    </Alert>

1. Click **Clone the Database & files from Live into the Development Environment**.

1. Click <Icon icon="new-window-alt" text="Visit Development Site"/> when this is complete to confirm that the content you created on your Live site now appears on your Dev site.

Nice work! You added a page to your Live site, then cloned this environment "down" to Dev. Your Dev environment is a safe place for editing code, and now it's up-to-date with your latest content.