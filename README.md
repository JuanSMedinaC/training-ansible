# Juan Sebastián Medina Cordero
# A00371957
# Ansible Training

The following practice consists of using terraform to deploy a virtual machine in Azure and with ansible running remotely the deployment of a game.

We use the following base code consisting of an inventory which has a hosts.ini file containing what will be our IP and the password assigned to it.

![](images/image20.png)

![](images/image1.png)

We also have some playbooks that redirect to roles which have the execution steps for the installation of docker and the execution of the service.

What we have to do then is to add a terraform file that creates a virtual machine in the Azure cloud.

![](images/image8.png)

And we do some changes the addition of an admin password reference, and the replacement of key authentication to password authentication when running ssh.

![](images/image2.png)

We can initialize the VM mounting process by executing terraform init, this brings our needed dependencies.

![](images/image18.png)

Then we run terraform plan which will create a plan file and will ask for our administrator password as it is needed for the deployment of the VM.

![](images/image17.png)

And finally we apply using our plan file, this starts the process of deployment.

![](images/image22.png)

Finally we get our machine's public IP address.

![](images/image9.png)

And we can check in the Azure portal that it is indeed active.

![](images/image19.png)

We have to connect to the vm initially so it gets added to the known hosts.

And we replace the values defined on the hosts.ini file.

![](images/image7.png)

After that we can check the ansible connection with the vm with the following command.

![](images/image13.png)

After we have proven there is connection with the machine using ansible we can run the ansible playbook for installing docker in the vm by referencing the hosts.ini file and and the playbook we want to run.

![](images/image14.png)

Then we ran our run container playbook. We can see that there is a problem when running this playbook referring to the absence of docker in the python libraries.

![](images/image3.png)

The way of fixing this problem is to connect to the virtual machine with ssh and running the command shown in the error message.

![](images/image15.png)

When we try running it back it worked.

![](images/image10.png)

Now we find another problem, when checking the docker container roles file we can notice the service should be running on the port 8787

![](images/image16.png)

But when accessing it it does not respond.

![](images/image21.png)

After checking the security rules of the vm the only open port for ingress is ssh port 22.

![](images/image6.png)

We have to add a rule to enable TCP access on port 8787.

![](images/image5.png)

And lastly we can access our game.

![](images/image11.png)

We have to remember to stop our service from running and our infrastructure elements.

![](images/image12.png)

And it dismounts everything we had built.

![](images/image4.png)
