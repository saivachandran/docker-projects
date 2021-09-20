docker 
======

Hypervisor
----------

A hypervisor is a software that makes virtualization possible. It is also called Virtual Machine Monitor. It divides the host system and allocates the resources to each divided virtual environment. You can basically have multiple OS on a single host system. There are two types of Hypervisors:

    Type 1: It’s also called Native Hypervisor or Bare metal Hypervisor. It runs directly on the underlying host system. It has direct access to your host’s system hardware and hence does not require a base server operating system.

    Type 2: This kind of hypervisor makes use of the underlying host operating system. It’s also called Hosted Hypervisor.

---------------

Virtualization
--------------

Virtualization is the process of creating a software-based, virtual version of something(compute storage, servers, application, etc.). These virtual versions or environments are created from a single physical hardware system. Virtualization lets you split one system into many different sections which act like separate, distinct individual systems. A software called Hypervisor makes this kind of splitting possible. The virtual environment created by the hypervisor is called Virtual Machine.

----------------------

containerzation
---------------

Containerization is the process of packaging software code, its required dependencies, configurations, and other detail to be easily deployed in the same or another computing environment. In simpler terms, containerization is the encapsulation of an application and its required environment

------------------------------------------------------------------------------------------------------------------
Difference between virtualization and containerization
-----------------------------------------------------

Virtualization enables you to run multiple operating systems on the hardware of a single physical server, while containerization enables you to deploy multiple applications using the same operating system on a single virtual machine or server.

-------------------------------------------------------------------------------------------------------------------

What is Docker

Since its a Docker interview, there will be an obvious question about what is Docker. Start with a small definition.

Docker is a containerization platform which packages your application and all its dependencies together in the form of containers so as to ensure that your application works seamlessly in any environment, be it development, test or production. Docker containers, wrap a piece of software in a complete filesystem that contains everything needed to run: code, runtime, system tools, system libraries, etc. It wraps basically anything that can be installed on a server. This guarantees that the software will always run the same, regardless of its environment.

------------------------------------------------------------------------------

Docker image
------------

A Docker image is a read-only template that contains a set of instructions for creating a container that can run on the Docker platform. It provides a convenient way to package up applications and preconfigured server environments, which you can use for your own private use or share publicly with other Docker users

Docker image is the source of Docker container. In other words, Docker images are used to create containers. When a user runs a Docker image, an instance of a container is created. These docker images can be deployed to any Docker environment.

-----------------------------------------------------------------------------------------------------------------
what is dockerfile
------------------

 Dockerfile is a text file that contains a list of commands (instructions), which describes how a Docker image is built based on them. The command docker build tells Docker to build the image by following the content (instructions) inside the Dockerfile

-----------------------------------------------------------------------------------------------

what is docker compose
----------------------

Compose is a tool for defining and running multi-container Docker applications. With Compose, you use a YAML file to configure your application's services. Then, with a single command, you create and start all the services from your configuration.

------------------------------------------------------------------------------------------------------------------

What is a Docker Namespace
--------------------------

A namespace is one of the Linux features and an important concept of containers. Namespace adds a layer of isolation in containers. Docker provides various namespaces in order to stay portable and not affect the underlying host system. Few namespace types supported by Docker – PID, Mount, IPC, User, Network


what dockerfile
---------------
Docker can build images automatically by reading the instructions from a Dockerfile. A Dockerfile is a text document that contains all the commands a user could call on the command line to assemble an image. Using docker build users can create an automated build that executes several command-line instructions in succession.

what is dockercompose
---------------------

Compose is a tool for defining and running multi-container Docker applications. With Compose, you use a YAML file to configure your application’s services. Then, with a single command, you create and start all the services from your configuration





