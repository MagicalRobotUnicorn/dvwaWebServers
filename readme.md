<p align=”center”>

<img src="images/magical.png">
</p>
This project represents the documentation of the request by a client to have a web application deployed to redundant servers, updated through a secure jump box, and having the logs from those servers sent to a machine hosting the ELK stack (Elastic Search, Log Stash, and Kabana).

This project is hosted on Azure Web Services, the cloud services arm of Microsoft.

We began with creating a resource group for our virtual machines, called the RedTeamResourceGroup. In Azure, a resource group is defined as a logical grouping all resources used for a particular setup or group.

We next added a virtual network within our resource group. A virtual network is a collection of machines that can communicate with each other, and mimics a physical network.

We then created a security group to manage access to the virtual network. This network started out with all traffic being blocked as a safeguard against unwelcome guests.

After our network was set up, we created a jump box, from which our webservers would be updated. We allowed communication over SSH to our jump box by altering our security rules in our security group.

Our team then created three webservers, connected to the virtual network we outlined earlier.

The webservers were loaded with the DVWA, deployed using the ansible script 'pentest.yml', available in 'YAML Scripts' folder of this repository.

Red Team Security Group Final Security Rules:

<p align=”center”>
<img src="images/redTeamSG.jpg?raw=true">
</p>

Load Balancer for Web Servers

<p align=”center”>
<img src="images/LBHenry.png">
</p>

To monitor the logging information from these web applications, we created a webserver dedicated to a docker container running the ELK stack of technologies, also known as Elastic Search, Logstash, and Kibana. This webbox was created within a separate network security group, which contained a rule allowing our webservers to send diagnostic information to it.

Our log information on the webservers was exported using filebeat, which we deployed using our jumpbox and the filebeatPlaybook YML file, available under the 'YAML Scripts' file of our repository.

<p align=”center”>
<img src="images/elkSG.jpg?raw=true">
</p>
