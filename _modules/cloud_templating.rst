Lab 01. Cloud Templating
*************************

When using Cloud Assembly, you are able to take advantage of both cloud native services and cloud agnostic services. In this lab you will learn how to create a cloud agnostic template and how to use constraints to influence the placement decision.

.. note:: Whenever you see #TODO in a code sample, you need to replace the line with the appropriate syntax. Refer to the linked documents if you need assistance.

Template Creation
==================
Cloud Assembly provides both a visual canvas and a YAML editor to interact with. To begin, you'll use the canvas. Click on the Design tab to get started.

Create a new cloud template. Call it **Basic IaaS**, and add it to the **socialabs** project.

Create Cloud Agnostic Machine
-----------------------------
In the components panel, locate the Cloud Agnostic section and drag a Machine object onto the canvas. The generated YAML should appear like the block below.

.. code-block:: yaml
   :linenos:
   :emphasize-lines: 7,8

    formatVersion: 1
    inputs: {}
    resources:
      Cloud_Machine_1:
      type: Cloud.Machine
      properties:
        image: ''
        flavor: ''

What do you see when you click on ``properties``? Can you tell what data type it is?

What are the single quotes after ``image``? Click on ``image`` to determine what type is it.

1.  Modify the YAML so that the template uses the **ubuntu** image and the **medium** flavor
2.  At the end of the YAML block, under ``flavor`` start a new line (correctly indented) and begin typing ``constraints``

.. note:: You can type this out in its entirety or use the autocomplete.

3.  At the end of ``constraints``, start a new line and notice how it auto populates ``- tag:``
4.  Within the single quotes of ``- tag:`` add ``platform:aws`` for the placement decision

.. image:: ../_static/basic_iaas.gif

Sample YAML
-----------

.. code-block:: yaml
   :linenos:

    version: 1.0
    name: Basic IaaS
    formatVersion: 1
    resources:
    machine:
      type: Cloud.Machine
      properties:
        image: #TODO configure the template to use the ubuntu image
        flavor: #TODO configure the template to use the medium flavor
      constraints:
        - tag: #TODO configure the template placement decision for AWS

Deploy Template
----------------

1.  Click on the **Deploy** button down below
2.  For **Deployment Name** type *basic aws*
3.  Click on the **Deploy** button
4.  After a few minutes the deployment should be complete, click on the deployment name to view more details about the components

Can you identify the external and internal IP addresses of the workload you deployed?

Challenge
---------

1.  Edit the template to deploy to Azure.
2.  Apply a different capability tag to each of your AWS availability zones, and then use a matching constraint to control where they land. Availability zones can be found within the Cloud Zone.
3.  Add a new property to deploy 2 instances of the machine.

Attaching Networks
==================
Every machine that gets deployed, have a specific purpose and function. Many times, this is clearly represented by the network segments that these machines gets attached to. In this part of the lab, we will be attaching an existing network segment onto a machine in the template. 

Using the same VMware Cloud Template, **Basic IaaS**, drag a **Cloud Agnostic -> Network** resource component from the design canvas. The generated YAML should appear like the block below.

Create Cloud Agnostic Network
------------------------------

.. code-block:: yaml
   :linenos:
   :emphasize-lines: 7

    formatVersion: 1
    inputs: {}
    resources:
      Cloud_Network_1:
      type: Cloud.Network
      properties:
        name: 
        networkType: existing

What do you see when you click on ``networkType``? In this lab, we will be using ``networkType: existing``, which uses a discovered network or deployed network Origin type. 

So, what is the difference?

- **Discovered origin**: manually created network objects discovered through Cloud Assembly.
- **Deployed origin**: network objects provisioned by Cloud Assembly

.. note:: There are many other different networkTypes that Cloud Assembly supports. You can find out more `here <https://docs.vmware.com/en/VMware-Cloud-Assembly/services/Using-and-Managing/GUID-19347DB8-8BF9-4FD1-B5A3-97A900915B8E.html?hWord=N4IghgNiBcIHYFMAuB3A9gJwNYBUCeADggM4gC+QA>`__

1.  Modify the YAML so that the template has a network **name** and also **constraints** for placement decision
2.  At the end of ``properties``, start a new line and begin typing ``name``, you can give it any name (i.e. app-net, web-net, etc)
3.  At the end of the YAML block, under ``networkType`` start a new line (correctly indented) and begin typing ``constraints``
4.  At the end of ``constraints``, start a new line and notice how it auto populates ``- tag:``
5.  Within the single quotes of ``- tag:`` add ``function:app`` for the placement decision
6.  To connect the machine to the network, you can drag the connectors from the machine to the network using the visual canvas (see illustration below), or you can type in the YAML code syntax. 

.. image:: ../_static/cloud_template_connect_network.gif

Sample YAML
-----------

.. code-block:: yaml
   :linenos:

    version: 1.0
    name: Basic IaaS
    formatVersion: 1
    resources:
      machine:
        type: Cloud.Machine
        properties:
          image: ubuntu1604
          flavor: small
          constraints:
            - tag: 'platform:aws'
          networks:
            - network: '${resource.network.id}'
      network:
        type: Cloud.Network
        properties:
          name: #TODO configure the template to use the name app-net
          networkType: existing
          constraints:
            - tag: #TODO configure the template placement decision for app function

Deploy Template
----------------

1.  Click on the **Deploy** button down below
2.  For **Deployment Name** type *basic aws with network*
3.  Click on the **Deploy** button
4.  After a few minutes the deployment should be complete, click on the deployment name to view more details about the components

Are you able to observe if the machine and network attached belong to the same CIDR? 

Attaching Storage
==================
It is common to have any workloads to have additional storage volumes attached to them to store data. In this lab, we will be going through how can we provision a storage volume to the template.

.. note:: This section is WIP

Conclusion
==========

In this lab we explored how to create an agnostic template and use constraints to influence the placement decisions of compute, network and storage.

Congratulations! You have completed Lab 1. Feel free to play with your successful deployments or hang tight for the next demonstration.

Further Reading
================

1. `Create a simple template <https://docs.vmware.com/en/VMware-Cloud-Assembly/services/Using-and-Managing/GUID-1EE72CCE-A871-4E63-88E5-30C12246BBBF.html>`__
2. `How constraints work <https://docs.vmware.com/en/VMware-Cloud-Assembly/services/Using-and-Managing/GUID-C8C335F4-9623-401C-825E-6F5B2B3C6507.html>`__