---
title: Legacy Dashboard
subtitle: Create A Site
description: Create a new Drupal or WordPress site on Pantheon.
tags: [site, dashboard]
layout: guide
showtoc: true
reviewed: "2022-12-13"
permalink: docs/guides/legacy-dashboard/create-sites
anchorid: create-sites
editpath: legacy-dashboard/02-create-sites.md
contenttype: [guide]
innav: [false]
categories: [create, dashboard, accounts]
cms: [wordpress, drupal]
audience: [agency, development]
product: [dashboard]
integration: [--]
---

The Pantheon Dashboard provides a quick "click to install" method of creating new sites. In less than five minutes, you'll have a new site up and running on the platform.

## Create a Site

1. From your User or Organization's Dashboard, click **Create New Site** to be brought to the **Create Your Pantheon Site** page:

  ![Create Your Pantheon Site page](../../../images/dashboard/create-pantheon-site.png)

1. Name the site.

  <Alert title="Note" type="info">

  The site name will be prefixed to all [Platform URLs](/guides/domains), which are automatically configured as subdomains of `pantheonsite.io`.

  This name cannot be changed once set.

  </Alert>

1. Optionally, if you have access to [organizations](/guides/legacy-dashboard/org-dashboard/#new-sites), choose a workspace to affiliate the site with.
1. Choose a [Region](/regions) for the Site.
1. Click **Continue** and wait a few moments for the Site to be created:

1. On the **Choose Your CMS** page, click **Deploy** to install WordPress, Drupal (Latest Version), or Drupal 7. See [Choosing Your Start State](/start-state) for more information.

   Wait while the platform provisions the site with the start state you selected.

1. Click **Visit your Pantheon Site Dashboard** to transfer to the [Site Dashboard](/guides/quickstart/workflow/).
1. Click **Visit Development Site** and complete the installation process for the selected framework.

  ![Site Dashboard in the Dev tab shows the Visit Development Site button](../../../images/dashboard/site-dashboard-dev.png)

## Sandbox Sites

Sandbox sites are useful for trying out the Pantheon platform, creating sandboxes for development, or for starting a new client project. Pantheon allocates two Sandbox sites for all user accounts. If you've reached your limit of Sandbox sites, delete an unused site, take a site live, or join an organization. If you're building sites for third parties, join the [Pantheon Partner Program](https://pantheon.io/plans/partner-program?docs) for more Sandbox sites, Multidev environments, and other features. If you're at an educational institution, sign up for [Pantheon for EDU](https://pantheon.io/edu?docs).

### Sandbox Resources

| **Sandbox**                                    | **Support**         | 
|------------------------------------------------|---------------------|
| Application Containers                     | 1                       | 
| PHP Workers                                | 4                       |         
| PHP Memory Limit                           | 256MB             |                              |Storage                                     | 20 GB    |
| Custom Domain Limit (per site) <Popover   content = "For details, see <a href='/guides/domains'>Domains and Redirects</a>."  />  | 0                                         | 
| Free and managed HTTPS <Popover   content = "For details, see <a href='/guides/global-cdn/https/'>HTTPS on Pantheon's Global CDN</a>."  />   | <span  style= " color:green " > ✔ </span> |  
| New Relic <Popover   content = "For details, see <a href='/new-relic/'>New Relic APM Pro</a>."  />  | <span  style= " color:green " > ✔ </span> |
| Object Cache <Popover   content = "For details, see <a href='/guides/object-cache/'>Object Cache (formerly Redis) for Drupal or WordPress</a>."  /> | <span  style= " color:green " > ✔ </span> | 
| Pantheon Search (Solr) <Popover   content = "For details, see <a href='/solr/'>Pantheon Search (formerly Pantheon Solr)</a>."  />  | <span  style= " color:green " > ✔ </span> | 

## Your Pantheon Account

Your account is your own individual account, and every account can manage multiple projects or sites at a time. Pantheon doesn't recommend sharing your account with other people. If you're collaborating on a project or handing over ownership to a client, use our [team management](/guides/account-mgmt/workspace-sites-teams/teams) and [ownership transfer](/guides/account-mgmt/#billing-tasks) tools.

## Frequently Asked Questions (FAQs)

### Can I rename my Pantheon site after creation?

No. Site names and Platform URLs are permanent and cannot be changed. As a workaround, you can export your existing site and import it to a new site with the correct name. See [Migrate Sites to Pantheon FAQs](/guides/guided/#how-do-i-clone-an-existing-pantheon-site).

### What if my site name is already taken?

Site names must be unique across all Pantheon sites, including [frozen](/guides/platform-considerations/platform-site-info/#inactive-site-freezing) sites. Choose another site name, and remember that the name you choose in the Pantheon Dashboard is only visible to the public in your [platform domain](/guides/domains).

## Next Steps

 - [Developing Directly with SFTP](/guides/sftp)
 - [Starting with Git](/guides/git/git-config)