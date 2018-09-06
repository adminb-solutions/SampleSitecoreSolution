# Sitecore Sample Solution

Example of a simple Sitecore solution configured to be deployed, during development, to a docker instance.

## Prerequisites

As Sitecore does not provide a set of docker images you need to first build them using the instructions in the [_sitecore-docker_ repo](https://github.com/adminb-solutions/sitecore-docker).

## Usage

1. Open the solution in Visual Studio and invoke the publish operation on the _SampleSite_ project. This will build the project and output its content to the ```.artifacts``` folder. 

1. Create the folders ```.logs\sitecore``` and ```.logs\xconnect``` in the root of the solution.

1. Invoke ```docker-compose up -d```. This will bring Sitecore up, the files from the ```.artifacts``` folder are copied to the webroot of Sitecore. Logs are output in the ```.logs``` folder.

1. Sitecore should be available under ```http://sitecore/```. 

1. If you are using Unicorn, you don't need to change the default serialization folder. Serialized items are picked from the ```serialization``` folder. Open the ```http://sitecore/unicorn.aspx``` page and either serialize or sync.

1. When you no longer need Sitecore running, you can do ```docker-compose stop``` to stop all the containers, but maintain their state.

1. If at any point you need to remove the Sitecore instance simply do a ```docker-compose down```. You can always deploy again from scratch invoking ```docker-compose up -d``` again.

## Known issues

* Debugging is not yet available
* Windows containers are quite resource intensive. Adjust the cpu_count and memory values in the ```docker-compose.yml``` file if necessary. Eventually SOLR and MSSQL should be moved to Linux containers.
* Sitecore Rocks is not enabled by default. You need to copy the files to the root of sitecore. You could temporarily place them in the ```.artifacts``` folder for them to get copied to the site root.

