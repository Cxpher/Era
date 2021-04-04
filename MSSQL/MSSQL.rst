Deploy a Kubernetes Application on Karbon Platform Services
===========================================================

Karbon Platform Services (KPS) is a Kubernetes based multi-cloud PaaS
that enables rapid development and deployment of microservices-based
applications ranging from simple stateful containerized applications to
complex AI, IoT and hybrid applications across any cloud.

This tutorial will guide you through the deployment and update of a
sample Kubernetes Application using KPS. The application is deployed to
a KPS Service Domain for execution. This tutorial assumes your Service
Domain has already been deployed using steps from the Karbon Platform
Services Admin Guide and that direct network connectivity between the
Service Domain and your workstation is configured (to view sample web
app output). Access to the Admin Guide is provided via the My Nutanix
Portal and requires an account to login.

**For brevity, several component applications in this tutorial have been
combined into single deployment manifests (Kubernetes YAML or Helm
chart). This is not representative of a typical production deployment,
where all applications and services are deployed as separate apps using
API calls in a standard CI/CD pipeline.**

Accessing Karbon Platform Services
----------------------------------

1. Open https://my.nutanix.com/ in your browser. If you don't already
   have a My Nutanix account, follow steps to create one.
2. Scroll to the Cloud Services section and click Launch to access the
   Karbon Platform Services Cloud Management Console.

At this point you should have a dashboard with a default User (you),
Project, Category.

Application Design
------------------

The application deployed as part of this tutorial is a typical content
management system where users can post blogs, articles and others can
add comments to it. You will also add analytics like a wordcloud to tell
authors the most popular terms in the reviews for their posts.

Here are the components used to build the application:

-  Wordpress as the content management engine for creating the
   e-commerce application
-  MySQL database to support Wordpress
-  Debezium for getting change events from DB to Kafka
-  Kafka for streaming the orders other services like Recommendation
   Service
-  Recommendation Service receives the streams and updates the most
   bought product listing page
-  Loader which will simulate user behavior with artificially created
   data about products and pruchase history

Application Architecture
------------------------

.. figure:: img/woodkraft-app.png
   :alt: Woodkraft App

   Woodkraft App!
Application Deployment
----------------------

The following steps will explain how to deploy the Woodkraft application
on KPS.

