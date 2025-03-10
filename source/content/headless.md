---
title: Running WordPress and Drupal as a Backend API
description: Learn about headless development models for decoupled architecture on Pantheon.
categories: [develop]
tags: [modules, plugins]
contributors: [eabquina, rachelwhitton]
---
Pantheon supports running WordPress and Drupal as an API (Application Programming Interface) for the backend of headless sites, which enables the CMS to interact with external frontend applications over HTTP requests.

For example, a mobile application <Popover content="A separate and external frontend application that is not running on Pantheon." /> that uses the `GET`, `POST`, and `DELETE` HTTP methods to perform CRUD operations <Popover title="CRUD" content="Create, read, update and delete." /> on a CMS's database <Popover content="The Drupal or WordPress site running on Pantheon as the backend API." />.

## Decoupled Architecture Overview
WordPress and Drupal are traditionally monolithic CMSs, meaning they serve as the frontend and backend of a site. Decoupled architecture (**headless**) is a development model that uses a CMS to manage content in the backend with a completely separate frontend component to render that content in the browser.

Some key differences of decoupled architecture include:

<div class="flex-panel-group">

  <div id="headless" class="flex-panel-item">

  <div class="flex-panel-body">
   <p class="topic-info__description" >

   ![Decoupled Frontend](../images/decoupledcms-what-is-decoupled.png)

   **Decoupled Frontend**<br />
   Presentation can be handled in a variety of ways, from interactive JS frameworks like Angular, to static generators, to mobile apps, or even another CMS. Multiple frontends can peacefully coexist.
   </p>
 </div>
 </div>
 <div id="headless" class="flex-panel-item">
 <div class="flex-panel-body">
   <p class="topic-info__description" >

   ![Content Via Web Service API](../images/decoupledcms-what-is-content.png)

   **Content Via Web Service API**<br />
   The content for the site is accessible via a web-service API, usually in a RESTful manner and in a mashup-friendly format such as JSON.
   </p>
 </div>
 </div>
 <div id="headless" class="flex-panel-item">
 <div class="flex-panel-body">
   <p class="topic-info__description" >

   ![CMS Backend and Database](../images/decoupledcms-what-is-backend.png)

   **CMS Backend and Database**<br />
   There is a traditional database-driven CMS which editors use to maintain the content for the site, usually via the same admin interface as always.
   </p>
 </div>
 </div>
</div>

### Pantheon's Platform Benefits
Backend APIs running on Pantheon take advantage of the following platform features for optimal performance:

* [**Global CDN**](/guides/global-cdn): Cache backend API responses from WordPress or Drupal in 40+ global CHI metro POPs (points of presence).
* **Redis**: Leverage object caching for backend APIs that use the database-driven admin interface of the CMS to edit or add content. For details, see [Object Cache (formerly Redis) for Drupal or WordPress](/object-cache).
<!--todo: does solr belong here? help wanted describing the benefits of solr in context of decoupled site.]-->


## Exposing the Backend API
Running WordPress and Drupal as an API on Pantheon can be done on any Drupal or WordPress upstream. The process to [create](/create-sites), [update core](/core-updates), and [launch](/guides/launch) a backend API on Pantheon does not deviate from the standard procedures.

<TabList>

<Tab title="WordPress" id="wp-api" active={true}>

Since WordPress 4.7, the WordPress API is included as part of core. There's no action needed to expose the API on Pantheon. Explore default routes and endpoints like `/wp-json/wp/v2/posts` in your browser:

![default routes wp](../images/wp-json-posts.png)

We recommend using a trusted browser extension to format the JSON response from the API so it's easier to read.

Refer to the [Rest API Handbook](https://developer.wordpress.org/rest-api/) from WordPress.org's Developer Resources for full documentation on this web service.

</Tab>

<Tab title="Drupal 7" id="d7-api">

Web Services are implemented through various plugins in Drupal 7.

  - [RESTful](https://www.drupal.org/project/restful)
  - [RESTful Web Services](https://www.drupal.org/project/restws)
  - [Services](https://www.drupal.org/project/services)

The service module has several integration features, and other web service formats. It also has [several supporting modules](https://www.drupal.org/node/750036) that extend the Drupal 7 functionalities made available to the API.

<Alert title="Note" type="info">

While not a REST API service by itself, you can create a JSON view using the [Views Datasource](https://www.drupal.org/project/views_datasource) module.

</Alert>

</Tab>

</TabList>

## Frequently Asked Questions

### Can I use other frameworks or distributions?
You can use [custom upstreams](/guides/custom-upstream), [make your own build](/guides/build-tools) or [install distributions](/start-state/#public-distributions) that may serve as a backend API. For example, [Contenta](http://www.contentacms.org) can be used on the platform.

### How can I troubleshoot the backend API?
We recommend using one of the following Chrome extensions to debug HTTP requests:

* [Postman](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop?hl=en)
* [Dev HTTP Client](https://chrome.google.com/webstore/detail/dev-http-client/aejoelaoggembcahagimdiliamlcdmfm/related)
* [Restlet Client](https://chrome.google.com/webstore/detail/restlet-client-rest-api-t/aejoelaoggembcahagimdiliamlcdmfm)
