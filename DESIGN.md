# Architecture
- One Odoo pod connects to a CloudNativePG database cluster with 3 replicas. The cluster is behind a pooler with 3 instances.
- I have assumed that Traefik is used as the ingress controller, but the repo itself doesn't include any chart to deploy Traefik.
- cert-manager is used for automatic certificate issuing and renewal, but so far only to provide a Let's Encrypt certificate for the ingress (not counting the certificates shipped with Barman Cloud Helm chart).
- Infisical is used for secrets management. It's not reachable through the ingress but has to configured through port-forwarding.
- Logs from all containers are shipped to a VictoriaLogs database with the help of the VictoriaLogs Collector.
- The kube-prometheus-stack Helm chart is used to provide Prometheus monitoring and Grafana dashboards.
# Repo folder structure
```
odoo-deploy
└───helm-charts
    └───application                     # Charts to deploy Odoo itself and its database.
    |   |
    |   └───odoo                        # A general chart to deploy an Odoo instance. Note that
    |   |                               # the chart is not meant to be installed on its own but used
    |   |                               # as a dependency in an "odoo-instances" chart.
    |   |
    |   └───odoo-instances              # This folder is meant to contain charts for deploying specific
    |   |   |                           # Odoo instances. Each Odoo instance has its own subfolder with
    |   |   |                           # its own charts.
    |   |   |
    |   |   └───odoo-instance-1         # An example Odoo instance.
    |   |       |
    |   |       └───odoo                # The chart to deploy Odoo for the example instance.
    |   |       |
    |   |       └───postgres            # The chart to deploy a CloudNativePG cluster for the example instance.
    |   |   
    |   └───postgres                    # A general chart to deploy a CloudNativePG cluster. The note from
    |                                   # the "odoo" chart applies here too.
    |
    └───infra                           # Charts to deploy supporting infrastructure.
        |
        └───cert-manager                # cert-manager and a cluster issuer.
        |
        └───cloudnative-pg              # CloudNativePG and the Barman Cloud CNPG-I plugin.
        |
        └───infisical                   # The core Infisical platform and the Kubernetes Secrets Operator.
        |
        └───infisical-connection        # The components used by the Infisical Operator to connect to and
        |                               # authenticate with the Infisical instance.
        |
        └───infisical-service-accounts  # The service accounts, RBAC, and tokens needed to set up the       
        |                               # Infisical Kubernetes operator.
        |
        └───kube-prometheus-stack       # Monitoring with Prometheus and Grafana.
        |
        └───victoria-logs               # Log collection and storage with VictoriaLogs.
```
# Installation
## Infrastructure
1. Install the Infisical chart
2. Create an Infisical machine identity by following the instructions on https://infisical.com/docs/documentation/guides/kubernetes-operator#create-a-machine-identity.
3. Install the Infisical service accounts chart.
4. Set up the Kubernetes Auth method by following the instructions on https://infisical.com/docs/documentation/guides/kubernetes-operator#wire-up-the-kubernetes-auth-method.
5. Install the Infisical connection chart
6. Install the remaining infrastructure charts
## Odoo server and PostgreSQL
1. Create an Infisical project and add secrets by following the instructions on https://infisical.com/docs/documentation/guides/kubernetes-operator#create-a-project-and-add-a-secret. The following secrets are needed:
    1. `username` (PostgreSQL username)
    2. `password` (PostgreSQL password)
    3. `ACCESS_KEY_ID` (for S3-compatible bucket)
    4. `ACCESS_SECRET_KEY` (for S3-compatible bucket)
    5. `SSE_C_KEY` (for S3-compatible bucket)
2. Install the PostgreSQL chart
3. Install the Odoo chart
# Future
There are a number of improvements that should be made, but which I had to skip for now due to the time constraints:
- Use multiple replicas for Odoo. The Odoo pod is right now a single point of failure.
- Take Odoo file backups in addition to the database backups. Velero could be used for this.
- Create a self-signed CA with cert-manager and enable TLS within the Kubernetes cluster.
- Create network policies to restrict access to the different components.
- Set up automated bootstrapping of Infisical to avoid using the GUI. See https://infisical.com/docs/self-hosting/guides/automated-bootstrapping.
