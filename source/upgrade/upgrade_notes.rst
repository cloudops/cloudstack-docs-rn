.. Licensed to the Apache Software Foundation (ASF) under one
   or more contributor license agreements.  See the NOTICE file
   distributed with this work for additional information#
   regarding copyright ownership.  The ASF licenses this file
   to you under the Apache License, Version 2.0 (the
   "License"); you may not use this file except in compliance
   with the License.  You may obtain a copy of the License at
   http://www.apache.org/licenses/LICENSE-2.0
   Unless required by applicable law or agreed to in writing,
   software distributed under the License is distributed on an
   "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
   KIND, either express or implied.  See the License for the
   specific language governing permissions and limitations
   under the License.


General Upgrade Notes
=====================


Java version upgraded to Java 1.7
---------------------------------

As of Apache CloudStack 4.4, Java version required is 1.7 for the 
management-server, cloudstack-usage, KVM agent and system-VMs.


OVS plug-in
-----------

OVS plug-in functionality is disrupted if ovsdaemon crashes

A critical functionality issue came out with `CLOUDSTACK-6779 <https://issues.apache.org/jira/browse/CLOUDSTACK-6779>`_. On XenServer it
is observed that on VIF unplug Ovs-Vswitchd is crashing resulting in loosing all
the openflow rules added to the bridge. Ovs daemon gets started and creates a
bridge but configure openflow rules are lost resulting in the disruption of
connectivity for the VM's on the host.


Active-Directory Authentication (LDAP)
--------------------------------------

If using Active-Directory (LDAP/LDAPs) as user authentication; Upgrading to 
4.3 and later require changes in Global Settings. After upgrading CloudStack
to 4.3 or latest, following Global Settings must be change:

.. cssclass:: table-striped table-bordered table-hover

======================= ============== ==============
Global Settings         Default        New
======================= ============== ==============
ldap.user.object        inetOrgPerson  user
ldap.username.attribute uid            sAMAccountName
======================= ============== ==============


SystemVM 32bit deprecated
-------------------------

32bit versions of systemvm templates are in the process of behing deprecated. Upgrade instructions from this Release Notes use 64bit templates. 32bit systemvm-templates are available for this version on `http://cloudstack.apt-get.eu/systemvm/4.4/ <http://cloudstack.apt-get.eu/systemvm/4.4/>`_. Follow the dev mailing list for further updates.


.. not confirmed 
   Build From Sources
   ------------------
   
   Since CloudStack 4.2.1 build packages from source using non opensource 
   modules param ``-nonoss`` changed to ``-   noredist``.

Other Notes
-----------

If you are experiencing CloudStack UI issues, please consider upgrading your
tomcat instance to version 6.0.43  (tested version, but earlier versions prior
to 6.0.37 might work as well), to address the tomcat response issues caused by
latency between the browser/client and CloudStack Management server.
