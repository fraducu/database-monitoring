# Database monitoring
## Using ansible

- Role should run on Ubuntu Bionic
_I divided the task even further in more roles as they offer a more clear separation between the tasks and therefore can be used, tested and maintained separately._

- The ultimate purpose of this task is to display database operations in a Grafana dashboard.
_This is still under development and it's not working 100%. Even if the role is not completed successfully you can still log in and finish the grafana configuration manually. The are still couple of open points and bugs to be fixed but I really enjoyed the challenge._

- Use of `shell` (and `command`) Ansible modules are prohibited
_Command module is used only once in order to pass the configuration parameters for building the prometheus container. This could be avoided by building a custom image, more can be found information [here](https://prometheus.io/docs/prometheus/latest/installation/)_

- We expect the task to be completed in a tidy manner and to be fit for production use.
_At this point this is still in development so it's not quite production ready, but I took steps to develop it in a tidy manner._

1. Deploy a postgresql database in a container
_Done. Next steps: exted the functinality and deply docker networks and docker volumes._

2. Create a read and a write user for the database
_Done. Next steps: move the tasks from the main.yml in a separate yml file or even a new role and extend it with more tasks for creating more resources in PostgreSQL._

3. Deploy an exporter providing metrics from the database
_Done. Used the ansible-galaxy module found [here](https://galaxy.ansible.com/entercloudsuite/prometheus-exporter). Role seems to be reliable and has at this point: 193704Downloads. Next steps: dockerize the exporter, more information can be found [here](https://github.com/wrouesnel/postgres_exporter). The role is using the same resource to download the binary and run it as a service for the host machine._

4. Deploy in a container a prometheus instance gathering the metrics
_Done. Next steps: refactor the module and create custom docker image as described in the official documentation._

5. Deploy a grafana container with a dashboard for the database
_Forked from the ansible-galaxy module found [here](ansible-galaxy install ppadial.docker_grafana). Next steps: Fix remaining Bugs so all the tasks run successfully. Current bug is at the task: Check api status and retry until is available. Error: Invalid username or password._

6. Make some writing test against the database
_Only the initial DB was created. Next steps: introduce new tasks to postgres role using the Ansible modules (postgresql_db, postgresql_table, postgresql_query)_

7. Endpoints should be accessible through https _(example: https://0.0.0.0/prometheus, https://0.0.0.0/grafana)_
_At this moment the tools are accessible to the default unsecured http connection. Next step: check if prometheus and grafana have built in support for https and configure them. If not deploy nginx proxy and run the servers behind it._

8. Unsecured ports should not be accessible from internet
_Only the necessary ports are mapped from the docker container to the host machine. The host machine was deployed in AWS and the security group which contains the firewall rules was configured to allow only the specific ports. Firewall rules can be set on the host machine as well. Next steps: create a docker network and attach it to all the containers instead of using the default bridged network._

9. All data must be persistent
_All the containers have mounted volumes to ensure the date persistence. Next steps: Use docker volumes instead of bind mounts. Another approach is to use Docker data containers._
