Lab 01. Cloud Templating
*************************
Different organisations have different models by which they operate. In fact, many organisations have multiple operating models running concurrently. Do you use a shared vCenter for your private cloud workloads? What about AWS, one account per organisation, or per project?

Projects are the way ensure people are using the right set of infrastructure services. This could be through the use of explicitly mapping Cloud Zones to a given project, or through the application of Constraints to inform the placement algorithm in a desired manner.

Agnostic constructs are the means by which we map the specific details of an image, flavor, storage, or network through to a reusable common name.

.. code-block:: json
   :linenos:

   {
    "toilet": {
      "singapore": "wash room",
      "australia": "dunny",
      "america": "does anyone care?",
      "england": "loo"
    }
   }

.. note:: Whenever you see #TODO in a code sample, you need to replace the line with the appropriate syntax. Refer to the linked documents if you need assistance.

To begin, click on the Infrastructure tab to get started.

Project Creation
================

Configure Agnostic Constructs
=============================

Further Reading
================
1.  `Adding cloud zones that define placement regions or data centers <https://docs.vmware.com/en/VMware-Cloud-Assembly/services/Using-and-Managing/GUID-87FF38A3-CEAD-4B15-BC85-07568EA4CF1C.html>`__
2.  `Adding and managing projects <https://docs.vmware.com/en/VMware-Cloud-Assembly/services/Using-and-Managing/GUID-082C0945-4A69-4847-9EA3-D11A332FA6D2.html>`__
3.  `Adding flavor mappings to create common machine sizes <https://docs.vmware.com/en/VMware-Cloud-Assembly/services/Using-and-Managing/GUID-C8DEE9D3-A55A-4720-B123-C2640C74CB5E.html>`__
4.  `Adding image mappings to create common operating systems <https://docs.vmware.com/en/VMware-Cloud-Assembly/services/Using-and-Managing/GUID-E8F94989-C006-4D9D-9536-F85EB0B53512.html>`__
5.  `Adding network profiles that account for different capabilities <https://docs.vmware.com/en/VMware-Cloud-Assembly/services/Using-and-Managing/GUID-5E3523F9-3995-46E1-9C72-04F81CD02AAF.html>`__