.. _access_and_permissions:

======================
Access and Permissions
======================

Controlling access and permissions to the Rackspace and GCP control planes
(APIs and UIs) along with the resources you deploy at GCP are a critical
part of the overall security of your environment.

Rackspace Account Permissions
-----------------------------

You can grant other members of your company access to Billing and Payments
and Support Ticketing by clicking the Account dropdown in the top right
corner of the
`Managed Services for Google Cloud Platform Control Panel <https://manage.rackspace.com/gcp>`_
and selecting User Management. From there, you can add and manage existing
users, selecting which parts of the Rackspace Control Panel they should have
access to.

GCP Project Permissions
-----------------------

GCP project permissions are managed via
`Google Cloud Identity and Access Management <https://cloud.google.com/iam/>`_.
If you have questions regarding the permissions you should grant users in
your company, contact a member of your :ref:`support team <support>`.

Identity/IAM
------------

Both Google and Rackspace encourage the use of the least permissive model for
IAM. In essence, access should only be granted where necessary to accomplish
tasks. Due to our Google Deployment Manager (GDM) based infrastructure-as-code
deployment model, minimizing users beyond the account used to allow
Rackspace access for management is suggested. Using GDM to deploy
infrastructure means user accounts with permission to manually create/destroy
resources in Google Cloud Platform (GCP) is not supported, and instead the
GDM templates should be updated and used to deploy the infrastructure changes.

The top-down permissions model used by Google means users granted
organizational access have permissions that override more granular permissions
applied at service levels, for example. Rackspace’s policy to avoid granting
access unless necessary, and then grant it at the most granular level
possible is necessary to ensure unintentional access is not granted.

To ensure that your Aviator or Service Blocks projects meet this permissions model,
Rackspace might periodically audit the permissions being passed to the project
and require adjustments to use the least permissive model.

Service Accounts
^^^^^^^^^^^^^^^^

Rackspace adds a primary service account with these roles to each of your GCP projects that we manage:

- ``automation@rackspace-mgcp.iam.gserviceaccount.com``

  + Project Browser
  + Project Billing Manager
  + Project IAM Admin

Additionally, we grant these service accounts access with the following roles to enable support tooling for all Aviator and Service Blocks projects:

- ``resource-observer@rackspace-mgcp.iam.gserviceaccount.com``

  The Resource Observer collects project metadata for support inventory

  + Viewer

- ``smart-tickets@rackspace-mgcp.iam.gserviceaccount.com``

  Smart Tickets works with Watchman to provide automated diagnostics and additional context for monitoring alerts that are turned to tickets for Rackers to address

  + Viewer
  + IAP-secured Tunnel User
  + Compute Instance Admin
  + Compute Security Admin

- ``mgcp-operations@rackspace-mgcp.iam.gserviceaccount.com``

  MGCP Operations facilitates integration of Operations monitoring (formerly Stackdriver) with Watchman

  + Viewer
  + Monitoring Admin


Do not remove these accounts or alter their permissions in any way without first consulting with your
:ref:`support team <support>`.

We also temporarily add accounts from the
gcp.rackspace.com domain as Rackers and automations need access to your
projects, so do not remove those accounts or alter their permissions.


Google Organization Permissions
-------------------------------

Rackspace will also add our
``automation@rackspace-mgcp.iam.gserviceaccount.com`` service account with
the Project Creator role on your Google organization, allowing both you and
us to create additional projects for new applications, as needed.
