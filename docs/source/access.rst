.. _access:

How to access Vision
====================

To access Vision, users should use SSH connect to the frontend frontend(management node) of the Vision, which allows them to access their data, submit jobs and check job status.

To access Vision via SSH, you should use the following settings:

 - hostname: ``main.vision.xdi.uevora.pt``
 - port: ``22``
 - username: provided by the user
 - password: provided by Vision administrators

Example
-------

.. code-block:: console

  $: ssh user@vision.xdi.uevora.pt
  [user@frontend ~]$

.. note::
  Please note that users can only access Vision from the computer with the IP address provided by the user.
