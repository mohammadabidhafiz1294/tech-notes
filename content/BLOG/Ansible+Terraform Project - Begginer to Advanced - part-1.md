## Topics

-  [[#Introduction]]
*  [[#Overview of Automation in IT]]
*  [[#Introduction to Ansible and Terraform]]
*  [[#Target Audience and Prerequisites]]
* [[#**Understanding Ansible**]]
	-  [[#What is Ansible?]]
	- [[#How its work?]]
	- [[# Key Features and Benefits]]
	-  [[#Core Components of Ansible]]
		-  [[#Inventory]]
			- [[#Statics Inventory]]
			- [[#Dynamic Inventory]]
		-  [[#Playbooks]]
		- [[#Modules]]
		- [[#Tasks]]
		- [[#Roles]]
			- [[#Why Use Ansible Roles?]]
		- [[#Collections]]
	-  [[#Installation and Setup]]
-  [[#**Understanding Terraform**]]
	-  What is Terraform?
	-  Key Features and Benefits
	- Core Components of Terraform
	-  Providers
	-  Modules
	- State Management
	- Provisioning
	- Installation and Setup
- Ansible and Terraform - A Comparative Overview
- Use Cases for Each Tool
-  Complementarity of Ansible and Terraform
-  Conceptual Understanding of IaC (Infrastructure as Code)
- Building a Basic Project with Ansible
- Setting Up a Development Environment
-  Writing a Simple Playbook
- Using Ansible Modules
- Managing Inventory and Configurations
- Building a Basic Project with Terraform
-  Setting Up a Development Environment
- Writing a Basic Terraform Configuration
- Using Terraform Providers and Resources
- Managing Terraform State
- Advanced Ansible Techniques
-  Role-Based Project Structure
- Error Handling and Debugging Tips
-  Optimizing Ansible Playbooks
-  Integration with Other Tools
-  Advanced Terraform Techniques
-  Terraform Modules for Reusability
-  State Management Best Practices
- Using Workspaces for Environments
- Advanced Provisioning with Terraform
-  Integrating Ansible and Terraform
- Use Cases for Combining Both Tools
- Workflow Automation with Ansible and Terraform
- Real-World Scenario: Deploy a Web Application
- Practices and Hands-On Exercises
- End-to-End Project: Automate Infrastructure and Configuration
- Sample Exercises and Challenges
- Common Pitfalls and How to Avoid Them
- Conclusion
- Recap of Key Learnings
- Future Trends in IT Automation
- Additional Resources and Next Steps

## Introduction
Here , We will create a awesome hands-on experience in ansible with terraform project. Wordpress setup with separated database & web-contact on docker containerization.

## Overview of Automation in IT
IT automation refers to the use of software to create repeatable instructions and processes to replace or reduce human interaction with IT systems. Automation helps:

- Increase efficiency and consistency
- Reduce human errors
- Accelerate deployment cycles
- Enable scalability
- Improve compliance and auditability

## Introduction to Ansible and Terraform
**Ansible** is an open-source automation tool focused on configuration management, application deployment, and task automation. It uses a simple YAML-based language (playbooks) to describe automation jobs.

**Terraform** is an infrastructure as code (IaC) tool that enables you to safely and predictably create, change, and improve infrastructure. It uses declarative configuration files to manage cloud and on-prem resources.

## Target Audience and Prerequisites
This guide is designed for:

- DevOps engineers
- System administrators
- Cloud engineers
- IT professionals looking to automate infrastructure

Prerequisites:

- Basic Linux command line knowledge
- Understanding of cloud concepts
- Familiarity with YAML and JSON formats
- Virtualization basics

##  **Understanding Ansible**

### What is ansible ??
Ansible is an open source IT automation engine that automates

- provisioning
- configuration management
- application deployment
- orchestration

and many other IT processes. It is free to use, and the project benefits from the experience and intelligence of its thousands of contributors.

### How its work?
Ansible is agentless in nature, which means you don't need install any software on the manage nodes.

For automating Linux and Windows, Ansible connects to managed nodes and pushes out small programs—called Ansible modules—to them. These programs are written to be resource models of the desired state of the system. Ansible then executes these modules (over SSH by default), and removes them when finished. These modules are designed to be idempotent when possible, so that they only make changes to a system when necessary.

For automating network devices and other IT appliances where modules cannot be executed, Ansible runs on the control node. Since Ansible is agentless, it can still communicate with devices without requiring an application or service to be installed on the managed node.

### Key Features and Benefits

- **Agentless architecture**: No need to install agents on managed nodes.
- **Idempotency**: Ensures the same result regardless of how many times you run it.
- **Simple YAML syntax**: Easy-to-read playbooks.
- **Extensive module library**: Over 3,000 modules for various tasks.
- **Push-based execution**: Changes are pushed from the control node.

### Core Components of Ansible
#### Inventory
Ansible inventory file is a fundamental component of Ansible that defines the hosts (remote systems) that you want to manage and the groups those hosts belong to. The inventory file can be static (a simple text file) or dynamic (generated by a script). It provides Ansible with the information about the remote nodes to communicate with during its operations.

##### Static Inventory
A static inventory file is typically a plain text file (usually named hosts or inventory) and is structured in INI or YAML format. Here are examples of both formats:
```INI
# inventory file: hosts

[webservers]
web1.example.com
web2.example.com

[dbservers]
db1.example.com
db2.example.com

[all:vars]
ansible_user=admin
ansible_ssh_private_key_file=/path/to/key
```

```YAML
# inventory file: hosts.yaml

all:
  vars:
    ansible_user: admin
    ansible_ssh_private_key_file: /path/to/key
  children:
    webservers:
      hosts:
        web1.example.com:
        web2.example.com:
    dbservers:
      hosts:
        db1.example.com:
        db2.example.com:
```

#### Dynamics Inventory
A dynamic inventory is generated by a script or plugin and can be used for environments where hosts are constantly changing (e.g., cloud environments). The script or plugin fetches the list of hosts from a source like AWS, GCP, or any other dynamic source.

Here is an example of a dynamic inventory script for AWS EC2:
```python
#!/usr/bin/env python

import json
import boto3

def get_aws_ec2_inventory():
    ec2 = boto3.client('ec2')
    instances = ec2.describe_instances()
    inventory = {
        'all': {
            'hosts': [],
            'vars': {
                'ansible_user': 'ec2-user',
                'ansible_ssh_private_key_file': '/path/to/key'
            }
        },
        '_meta': {
            'hostvars': {}
        }
    }

    for reservation in instances['Reservations']:
        for instance in reservation['Instances']:
            if instance['State']['Name'] == 'running':
                public_ip = instance['PublicIpAddress']
                inventory['all']['hosts'].append(public_ip)
                inventory['_meta']['hostvars'][public_ip] = {
                    'ansible_host': public_ip
                }

    print(json.dumps(inventory, indent=2))

if __name__ == '__main__':
    get_aws_ec2_inventory()
```

--> Usage case inventory, 
```bash
ansible-playbook -i inventory <Adhoc command or Playbook.yml>
```

#### Playbooks
A **Playbook** is a YAML file that defines a series of actions to be executed on managed nodes. It contains one or more "plays" that map groups of hosts to roles.

**Example**:
```yaml
- name: Update web servers
  hosts: webservers
  remote_user: root

  tasks:
  - name: Ensure apache is at the latest version
    ansible.builtin.yum:
      name: httpd
      state: latest

  - name: Write the apache config file
    ansible.builtin.template:
      src: /srv/httpd.j2
      dest: /etc/httpd.conf

- name: Update db servers
  hosts: databases
  remote_user: root

  tasks:
  - name: Ensure postgresql is at the latest version
    ansible.builtin.yum:
      name: postgresql
      state: latest

  - name: Ensure that postgresql is started
    ansible.builtin.service:
      name: postgresql
      state: started
```

- **Play**: A Play is a single, complete execution unit within a playbook. It specifies which hosts to target and what tasks to execute on those hosts. Plays are used to group related tasks and execute them in a specific order.

```yml
- name: Install and configure Nginx
  hosts: webservers
  tasks:
    - name: Install Nginx
      apt:
        name: nginx
        state: present
```
#### Modules
Modules are the building blocks of Ansible tasks. They are small programs that perform a specific action on a managed node, such as installing a package, copying a file, or managing services.

**Example**:
The apt module used in a task to install a package:
```yaml 
- name: Install Nginx
  apt:
    name: nginx
    state: present
```

#### Tasks
Tasks are individual actions within a play that use modules to perform operations on managed nodes. Each task is executed in order and can include conditionals, loops, and handlers.
**Example**:
```yaml
- name: Install Nginx
  apt:
    name: nginx
    state: present

- name: Start Nginx service
  service:
    name: nginx
    state: started
```

#### Collections
Collections are a distribution format for Ansible content. They bundle together multiple roles, modules, plugins, and other Ansible artifacts. Collections make it easier to share and reuse Ansible content.
Example

A collection structure might look like this:
```structure
my_collection/
├── roles/
│   └── my_role/
│       └── tasks/
│           └── main.yml
├── plugins/
│   └── modules/
│       └── my_module.py
└── README.md
```

--> Using a collection in PlayBooks ,**Example**:
```yaml
- name: Use a custom module from a collection
  community.general.my_module:
    option: value
```

#### Roles
An Ansible role is a reusable, self-contained unit of automation that is used to organize and manage tasks, variables, files, templates, and handlers in a structured way.

Roles help to encapsulate and modularize the logic and configuration needed to manage a particular system or application component.

This modular approach promotes reusability, maintainability, and consistency across different playbooks and environments.

---> **Key components of an ansible role**:

==> *Tasks*
The main list of actions that the role performs.
==> *Handlers*
Tasks that are triggered by changes in other tasks, typically used for actions like restarting services.
==> *Files*
Static files that need to be transferred to managed hosts.
==> *Templates*
Jinja2 templates that can be rendered and transferred to managed hosts.
==> *Vars*
Variables that are used within the role.
==> *Defaults*
Default variables for the role, which can be overridden.
==> *Meta*
Metadata about the role, including dependencies on other roles.
==> *Library*
Custom modules or plugins used within the role.
==> *Module_defaults*
Default module parameters for the role.
==> *Lookup_plugins*
Custom lookup plugins for the role.

---> Directory structure of Ansible role
An Ansible role follows a specific directory structure:
```Structure
<role_name>/
  ├── defaults/
  │   └── main.yml
  ├── files/
  ├── handlers/
  │   └── main.yml
  ├── meta/
  │   └── main.yml
  ├── tasks/
  │   └── main.yml
  ├── templates/
  ├── vars/
      └── main.yml
```
##### Why Use Ansible Roles?
**Modularity**
Roles allow you to break down complex playbooks into smaller, reusable components. Each role handles a specific part of the configuration or setup.
- **Reusability**
Once created, roles can be reused across different playbooks and projects. This saves time and effort in writing redundant code.

- **Maintainability**
By organizing related tasks into roles, it becomes easier to manage and maintain the code. Changes can be made in one place and applied consistently wherever the role is used.

- **Readability**
Roles make playbooks cleaner and easier to read by abstracting away the details into logically named roles.

- **Collaboration**
Roles facilitate collaboration among team members by allowing them to work on different parts
of the infrastructure independently.

- **Consistency**
Using roles ensures that the same setup and configuration procedures are applied uniformly across multiple environments, reducing the risk of configuration drift.
#### Installation and Setup
For installation & setup,Details in this webpage: [Ansible Documentation](https://docs.ansible.com/)

### Understanding the Terraform

#### What is Terraform?? 
Terraform is an infrastructure as code tool that allows you to define and provision data center infrastructure using a declarative configuration language.
#### Key Features and Benefits

- **Multi-cloud support**: Works with AWS, Azure, GCP, and others
    
- **Resource graph**: Creates and modifies resources efficiently
    
- **Change automation**: Applies complex changesets with minimal human interaction
    
- **State management**: Tracks resource state for modification and deletion
    
- **Declarative syntax**: Describes what infrastructure should look like

#### IaC??
Before the advent of IaC, infrastructure management was typically a manual and time-consuming process. System administrators and operations teams had to:

1. Manually Configure Servers: Servers and other infrastructure components were often set up and configured manually, which could lead to inconsistencies and errors.
2. Lack of Version Control: Infrastructure configurations were not typically version-controlled, making it difficult to track changes or revert to previous states.
3. Documentation Heavy: Organizations relied heavily on documentation to record the steps and configurations required for different infrastructure setups. This documentation could become outdated quickly.
4. Limited Automation: Automation was limited to basic scripting, often lacking the robustness and flexibility offered by modern IaC tools.
5. Slow Provisioning: Provisioning new resources or environments was a time-consuming process that involved multiple manual steps, leading to delays in project delivery.
    
IaC addresses these challenges by providing a systematic, automated, and code-driven approach to infrastructure management. Popular IaC tools include Terraform, AWS CloudFormation, Azure Resource Manager templates others.

These tools enable organizations to define, deploy, and manage their infrastructure efficiently and consistently, making it easier to adapt to the dynamic needs of modern applications and services.

#### Why Terraform??

There are multiple reasons why Terraform is used over the other IaC tools but below are the main reasons.

1. **Multi-Cloud Support**: Terraform is known for its multi-cloud support. It allows you to define infrastructure in a cloud-agnostic way, meaning you can use the same configuration code to provision resources on various cloud providers (AWS, Azure, Google Cloud, etc.) and even on-premises infrastructure. This flexibility can be beneficial if your organization uses multiple cloud providers or plans to migrate between them.
2. **Large Ecosystem**: Terraform has a vast ecosystem of providers and modules contributed by both HashiCorp (the company behind Terraform) and the community. This means you can find pre-built modules and configurations for a wide range of services and infrastructure components, saving you time and effort in writing custom configurations.
3. **Declarative Syntax**: Terraform uses a declarative syntax, allowing you to specify the desired end-state of your infrastructure. This makes it easier to understand and maintain your code compared to imperative scripting languages.
4. **State Management**: Terraform maintains a state file that tracks the current state of your infrastructure. This state file helps Terraform understand the differences between the desired and actual states of your infrastructure, enabling it to make informed decisions when you apply changes.
5. **Plan and Apply**: Terraform's "plan" and "apply" workflow allows you to preview changes before applying them. This helps prevent unexpected modifications to your infrastructure and provides an opportunity to review and approve changes before they are implemented.
6. **Community Support**: Terraform has a large and active user community, which means you can find answers to common questions, troubleshooting tips, and a wealth of documentation and tutorials online.
7. **Integration with Other Tools**: Terraform can be integrated with other DevOps and automation tools, such as Docker, Kubernetes, Ansible, and Jenkins, allowing you to create comprehensive automation pipelines.
8. **HCL Language**: Terraform uses HashiCorp Configuration Language (HCL), which is designed specifically for defining infrastructure. It's human-readable and expressive, making it easier for both developers and operators to work with.
#### Core Components of Terraform

##### Providers
Providers are plugins that interact with APIs to manage resources. Example providers:
- AWS
- Azure
- Google Cloud
- VMware
- Docker
##### Modules
Modules are containers for multiple resources that are used together. They can be reused across configurations.
##### State Management
Terraform maintains a state file (terraform.tfstate) that maps real-world resources to your configuration.
##### Provisioning
Terraform can provision infrastructure and then bootstrap it using provisioners (though Ansible is often better for configuration management).
