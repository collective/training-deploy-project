# Ansible deployment

This Ansible implementation includes:

3 menu options:
* Build Development Environment
* Deploy Local Staging VM
* Deploy Remote Production VM

4 roles:
* deploy_local
* deploy_remote
* setup_client
* setup_host

For complete documentation, follow the complete README.md in this project's root.

For quick summary, these steps will create a 3-tiered Plone solution (dev, staging, production) using Docker images:
* replace DOCKER_HUB_USER_CHANGE_ME with your Docker Hub username
* edit the hosts file to match your desired configuration
* make clean && make setup
* make install + Choose menu option 1 to build the dev environment
* Manually build the backend and frontend, make start-images, make release-images
* make install + Choose option 2 for local deployment
* make install + Choose option 3 for remote deployment
