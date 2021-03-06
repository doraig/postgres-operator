---
title: "Configuration Reference"
date:
draft: false
weight: 40
---

# PostgreSQL Operator Installer Configuration

The [`pgo-deployer` container]({{< relref "/installation/postgres-operator" >}})
is launched by using a Kubernetes Job manifest and contains many configurable
options.

This section lists the options that you can configure to deploy the PostgreSQL
Operator in your environment. The following list of environmental variables can
be used in the [`postgres-operator.yml`](https://github.com/CrunchyData/postgres-operator/blob/v4.3.2/installers/kubectl/postgres-operator.yml)
manifest.

## General Configuration

These environmental variables affect the general configuration of the PostgreSQL
Operator.

| Name | Default | Required | Description |
|------|---------|----------|-------------|
| `ARCHIVE_MODE` | true | **Required** | Set to true enable archive logging on all newly created clusters. |
| `ARCHIVE_TIMEOUT` | 60 | **Required** | Set to a value in seconds to configure the timeout threshold for archiving. |
| `BACKREST` | true | **Required** | Set to true enable pgBackRest capabilities on all newly created cluster request.  This can be disabled by the client. |
| `BACKREST_AWS_S3_BUCKET` |  |  | Set to configure the *bucket* used by pgBackRest with Amazon Web Service S3 for backups and restoration in S3. |
| `BACKREST_AWS_S3_ENDPOINT` |  |  | Set to configure the *endpoint* used by pgBackRest with Amazon Web Service S3 for backups and restoration in S3. |
| `BACKREST_AWS_S3_KEY` |  |  | Set to configure the *key* used by pgBackRest with Amazon Web Service S3 for backups and restoration in S3. |
| `BACKREST_AWS_S3_REGION` |  |  | Set to configure the *region* used by pgBackRest with Amazon Web Service S3 for backups and restoration in S3. |
| `BACKREST_AWS_S3_SECRET` |  |  | Set to configure the *secret* used by pgBackRest with Amazon Web Service S3 for backups and restoration in S3. |
| `BACKREST_AWS_S3_URI_STYLE` |  |  | Set to configure whether “host” or “path” style URIs will be used when connecting to S3. |
| `BACKREST_AWS_S3_VERIFY_TLS` | true  |  | Set this value to true to enable TLS verification when making a pgBackRest connection to S3. |
| `BACKREST_PORT` | 2022 | **Required** | Defines the port where pgBackRest will run. |
| `BADGER` | false | **Required** | Set to true enable pgBadger capabilities on all newly created clusters. This can be disabled by the client. |
| `CCP_IMAGE_PREFIX` | crunchydata | **Required** | Configures the image prefix used when creating containers from Crunchy Container Suite. |
| `CCP_IMAGE_PULL_SECRET` |  |  | Name of a Secret containing credentials for container image registries. |
| `CCP_IMAGE_PULL_SECRET_MANIFEST` |  |  | Provide a path to the Secret manifest to be installed in each namespace. (optional) |
| `CCP_IMAGE_TAG` |  | **Required** | Configures the image tag (version) used when creating containers from Crunchy Container Suite. |
| `CREATE_RBAC` | true | **Required** | Set to true if the installer should create the RBAC resources required to run the PostgreSQL Operator. |
| `CRUNCHY_DEBUG` | false |  | Set to configure Operator to use debugging mode. Note: this can cause sensitive data such as passwords to appear in Operator logs. |
| `DB_NAME` |  |  | Set to a value to configure the default database name on all newly created clusters.  By default, the PostgreSQL Operator will set it to the name of the cluster that is being created. |
| `DB_PASSWORD_AGE_DAYS` | 0 |  | Set to a value in days to configure the expiration age on PostgreSQL role passwords on all newly created clusters. If set to "0", this is the same as saying the password never expires |
| `DB_PASSWORD_LENGTH` | 24 |  | Set to configure the size of passwords generated by the operator on all newly created roles. |
| `DB_PORT` | 5432 | **Required** | Set to configure the default port used on all newly created clusters. |
| `DB_REPLICAS` | 0 | **Required** | Set to configure the amount of replicas provisioned on all newly created clusters. |
| `DB_USER` | testuser | **Required** | Set to configure the username of the dedicated user account on all newly created clusters. |
| `DEFAULT_INSTANCE_MEMORY` | 128Mi |  | Represents the memory request for a PostgreSQL instance. |
| `DEFAULT_PGBACKREST_MEMORY` | 48Mi |  | Represents the memory request for a pgBackRest repository. |
| `DEFAULT_PGBOUNCER_MEMORY` | 24Mi |  | Represents the memory request for a pgBouncer instance. |
| `DELETE_METRICS_NAMESPACE` | false |  | Set to configure whether or not the metrics namespace (defined using variable `metrics_namespace`) is deleted when uninstalling the metrics infrastructure. |
| `DELETE_OPERATOR_NAMESPACE` | false |  | Set to configure whether or not the PGO operator namespace (defined using variable `pgo_operator_namespace`) is deleted when uninstalling the PGO. |
| `DELETE_WATCHED_NAMESPACES` | false |  | 	Set to configure whether or not the PGO watched namespaces (defined using variable `namespace`) are deleted when uninstalling the PGO. |
| `DISABLE_AUTO_FAILOVER` | false |  | If set, will disable autofail capabilities by default in any newly created cluster |
| `DISABLE_FSGROUP` | false |  | Set to `true` for deployments where you do not want to have the default PostgreSQL fsGroup (26) set. The typical usage is in OpenShift environments that have a `restricted` Security Context Constraints. |
| `DYNAMIC_RBAC` | false | | When using a `readonly` or `disabled` `NAMESPACE_MODE`, determines whether or not the PostgreSQL Operator itself will granted the permissions needed to create required RBAC within a target namespace. |
| `EXPORTERPORT` | 9187 | **Required** | Set to configure the default port used to connect to postgres exporter. |
| `GRAFANA_ADMIN_PASSWORD` |  |  | Set to configure the login password for the Grafana administrator. |
| `GRAFANA_ADMIN_USERNAME` | admin |  | Set to configure the login username for the Grafana administrator. |
| `GRAFANA_INSTALL` | false |  | Set to true to install Crunchy Grafana to visualize metrics. |
| `GRAFANA_STORAGE_ACCESS_MODE` | ReadWriteOnce |  | Set to the access mode used by the configured storage class for Grafana persistent volumes. |
| `GRAFANA_STORAGE_CLASS_NAME` | fast |  | Set to the name of the storage class used when creating Grafana persistent volumes. |
| `GRAFANA_SUPPLEMENTAL_GROUPS` | 65534 |  | Set to configure any supplemental groups that should be added to security contexts for Grafana. |
| `GRAFANA_VOLUME_SIZE` | 1G |  | Set to the size of persistent volume to create for Grafana. |
| `METRICS` | false | **Required** | Set to true enable performance metrics on all newly created clusters. This can be disabled by the client. |
| `METRICS_NAMESPACE` | `pgo` |  | Namespace in which the `metrics` deployments with be run. |
| `NAMESPACE` |  |  | Set to a comma delimited string of all the namespaces Operator will manage. |
| `NAMESPACE_MODE` | dynamic |  | When installing RBAC using 'create_rbac', the namespace mode determines what Cluster Roles are installed. Options: `dynamic`, `readonly`, and `disabled` |
| `PGBADGERPORT` | 10000 | **Required** | Set to configure the default port used to connect to pgbadger. |
| `PGO_ADD_OS_CA_STORE` | false | **Required** | When true, includes system default certificate authorities. |
| `PGO_ADMIN_PASSWORD` |  | **Required** | Configures the pgo administrator password. |
| `PGO_ADMIN_PERMS` | * | **Required** | Sets the access control rules provided by the PostgreSQL Operator RBAC resources for the PostgreSQL Operator administrative account that is created by this installer. Defaults to allowing all of the permissions, which is represented with the * |
| `PGO_ADMIN_ROLE_NAME` | pgoadmin | **Required** | Sets the name of the PostgreSQL Operator role that is utilized for administrative operations performed by the PostgreSQL Operator. |
| `PGO_ADMIN_USERNAME` | admin | **Required** | Configures the pgo administrator username. |
| `PGO_APISERVER_PORT` | 8443 |  | Set to configure the port used by the Crunchy PostgreSQL Operator apiserver. |
| `PGO_APISERVER_URL` | https://postgres-operator |  | Sets the `pgo_apiserver_url` for the `pgo-client` deployment. |
| `PGO_CLIENT_CERT_SECRET` | pgo.tls |  | Sets the secret that the `pgo-client` will use when connecting to the PostgreSQL Operator. |
| `PGO_CLIENT_CONTAINER_INSTALL` | false |  | Run the `pgo-client` deployment with the PostgreSQL Operator. |
| `PGO_CLUSTER_ADMIN` | false | **Required** | Determines whether or not the cluster-admin role is assigned to the PGO service account. Must be true to enable PGO namespace & role creation when installing in OpenShift. |
| `PGO_DISABLE_EVENTING` | false |  | Set to configure whether or not eventing should be enabled for the Crunchy PostgreSQL Operator installation. |
| `PGO_DISABLE_TLS` | false |  | Set to configure whether or not TLS should be enabled for the Crunchy PostgreSQL Operator apiserver. |
| `PGO_IMAGE_PREFIX` | crunchydata | **Required** | Configures the image prefix used when creating containers for the Crunchy PostgreSQL Operator (apiserver, operator, scheduler..etc). |
| `PGO_IMAGE_PULL_SECRET` |  |  | Name of a Secret containing credentials for container image registries. |
| `PGO_IMAGE_PULL_SECRET_MANIFEST` |  |  | Provide a path to the Secret manifest to be installed in each namespace. (optional) |
| `PGO_IMAGE_TAG` |  | **Required** | Configures the image tag used when creating containers for the Crunchy PostgreSQL Operator (apiserver, operator, scheduler..etc) |
| `PGO_INSTALLATION_NAME` | devtest | **Required** | The name of the PGO installation. |
| `PGO_NOAUTH_ROUTES` |  |  | Configures URL routes with mTLS and HTTP BasicAuth disabled. |
| `PGO_OPERATOR_NAMESPACE` | pgo | **Required** | Set to configure the namespace where Operator will be deployed. |
| `PGO_TLS_CA_STORE` |  |  | Set to add additional Certificate Authorities for Operator to trust (PEM-encoded file). |
| `PGO_TLS_NO_VERIFY` | false |  | Set to configure Operator to verify TLS certificates. |
| `PROMETHEUS_INSTALL` | false |  | Set to true to install Crunchy Grafana to visualize metrics. |
| `PROMETHEUS_STORAGE_ACCESS_MODE` | ReadWriteOnce |  | Set to the access mode used by the configured storage class for Prometheus persistent volumes. |
| `PROMETHEUS_STORAGE_CLASS_NAME` | fast |  | Set to the name of the storage class used when creating Prometheus persistent volumes. |
| `PROMETHEUS_SUPPLEMENTAL_GROUPS` | 65534 |  | Set to configure any supplemental groups that should be added to security contexts for Prometheus. |
| `PROMETHEUS_VOLUME_SIZE` | 1G |  | Set to the size of persistent volume to create for Prometheus. |
| `SCHEDULER_TIMEOUT` | 3600 | **Required** | Set to a value in seconds to configure the `pgo-scheduler` timeout threshold when waiting for schedules to complete. |
| `SERVICE_TYPE` | ClusterIP |  | Set to configure the type of Kubernetes service provisioned on all newly created clusters. |
| `SYNC_REPLICATION` | false |  | If set to `true` will automatically enable synchronous replication in new PostgreSQL clusters. |

## Storage Settings

The store configuration options defined in this section can be used to specify
the storage configurations that are used by the PostgreSQL Operator.

## Storage Configuration Options

Kubernetes and OpenShift offer support for a wide variety of different storage
types and we provide suggested configurations for different environments. These
storage types can be modified or removed as needed, while additional storage
configurations can also be added to meet the specific storage requirements for
your PostgreSQL clusters.

The following storage variables are utilized to add or modify operator storage
configurations in the with the installer:

| Name | Required | Description |
|------|----------|-------------|
| `storage<ID>_name` | Yes | Set to specify a name for the storage configuration. |
| `storage<ID>_access_mode` | Yes | Set to configure the access mode of the volumes created when using this storage definition. |
| `storage<ID>_size` | Yes | Set to configure the size of the volumes created when using this storage definition. |
| `storage<ID>_class` | Required when using the `dynamic` storage type | Set to configure the storage class name used when creating dynamic volumes. |
| `storage<ID>_supplemental_groups` | Required when using NFS storage | Set to configure any supplemental groups that should be added to security contexts on newly created clusters. |
| `storage<ID>_type` | Yes  | Set to either `create` or `dynamic` to configure the operator to create persistent volumes or have them created dynamically by a storage class. |

The ID portion of storage prefix for each variable name above should be an
integer that is used to group the various storage variables into a single
storage configuration.

### Example Storage Configuration

| Name | Value |
|------|-------|
| STORAGE3_NAME | nfsstorage |
| STORAGE3_ACCESS_MODE | ReadWriteMany |
| STORAGE3_SIZE | 1G |
| STORAGE3_TYPE | create |
| STORAGE3_SUPPLEMENTAL_GROUPS | 65534 |

As this example storage configuration shows, integer `3` is used as the ID for
each of the `storage` variables, which together form a single storage
configuration called `nfsstorage`. This approach allows different storage
configurations to be created by defining the proper `storage` variables with a
unique ID for each required storage configuration.

### PostgreSQL Cluster Storage Defaults

You can specify the default storage to use for PostgreSQL, pgBackRest, and other
elements that require storage that can outlast the lifetime of a Pod. While the
PostgreSQL Operator defaults to using `hostpathstorage` to work with
environments that are typically used to test, we recommend using one of the
other storage classes in production deployments.

| Name | Default | Required | Description |
|------|---------|----------|-------------|
| `BACKREST_STORAGE` | hostpathstorage | **Required** | Set the value of the storage configuration to use for the pgbackrest shared repository deployment created when a user specifies pgbackrest to be enabled on a cluster. |
| `BACKUP_STORAGE` | hostpathstorage | **Required** | Set the value of the storage configuration to use for backups, including the storage for pgbackrest repo volumes. |
| `PRIMARY_STORAGE` | hostpathstorage | **Required** | 	Set to configure which storage definition to use when creating volumes used by PostgreSQL primaries on all newly created clusters. |
| `REPLICA_STORAGE` | hostpathstorage | **Required** | Set to configure which storage definition to use when creating volumes used by PostgreSQL replicas on all newly created clusters. |
| `WAL_STORAGE` |  |  | Set to configure which storage definition to use when creating volumes used for PostgreSQL Write-Ahead Log |

### Storage Configuration Types

#### Host Path Storage

| Name | Value |
|------|-------|
| STORAGE1_NAME | hostpathstorage |
| STORAGE1_ACCESS_MODE | ReadWriteMany |
| STORAGE1_SIZE | 1G |
| STORAGE1_TYPE | create |

#### Replica Storage

| Name | Value |
|------|-------|
| STORAGE2_NAME | replicastorage |
| STORAGE2_ACCESS_MODE | ReadWriteMany |
| STORAGE2_SIZE | 1G |
| STORAGE2_TYPE | create |

#### NFS Storage

| Name | Value |
|------|-------|
| STORAGE3_NAME | nfsstorage |
| STORAGE3_ACCESS_MODE | ReadWriteMany |
| STORAGE3_SIZE | 1G |
| STORAGE3_TYPE | create |
| STORAGE3_SUPPLEMENTAL_GROUPS | 65534 |

#### NFS Storage Red

| Name | Value |
|------|-------|
| STORAGE4_NAME | nfsstoragered |
| STORAGE4_ACCESS_MODE | ReadWriteMany |
| STORAGE4_SIZE | 1G |
| STORAGE4_MATCH_LABELS | crunchyzone=red |
| STORAGE4_TYPE | create |
| STORAGE4_SUPPLEMENTAL_GROUPS | 65534 |

#### StorageOS

| Name | Value |
|------|-------|
| STORAGE5_NAME | storageos |
| STORAGE5_ACCESS_MODE | ReadWriteOnce |
| STORAGE5_SIZE | 5Gi |
| STORAGE5_TYPE | dynamic |
| STORAGE5_CLASS | fast |

#### Primary Site

| Name | Value |
|------|-------|
| STORAGE6_NAME | primarysite |
| STORAGE6_ACCESS_MODE | ReadWriteOnce |
| STORAGE6_SIZE | 4G |
| STORAGE6_TYPE | dynamic |
| STORAGE6_CLASS | primarysite |

#### Alternate Site

| Name | Value |
|------|-------|
| STORAGE7_NAME | alternatesite |
| STORAGE7_ACCESS_MODE | ReadWriteOnce |
| STORAGE7_SIZE | 4G |
| STORAGE7_TYPE | dynamic |
| STORAGE7_CLASS | alternatesite |

#### GCE

| Name | Value |
|------|-------|
| STORAGE8_NAME | gce |
| STORAGE8_ACCESS_MODE | ReadWriteOnce |
| STORAGE8_SIZE | 300M |
| STORAGE8_TYPE | dynamic |
| STORAGE8_CLASS | standard |

#### Rook

| Name | Value |
|------|-------|
| STORAGE9_NAME | rook |
| STORAGE9_ACCESS_MODE | ReadWriteOnce |
| STORAGE9_SIZE | 1Gi |
| STORAGE9_TYPE | dynamic |
| STORAGE9_CLASS | rook-ceph-block |


## Pod Anti-affinity Settings
This will set the default pod anti-affinity for the deployed PostgreSQL
clusters. Pod Anti-Affinity is set to determine where the PostgreSQL Pods are
deployed relative to each other There are three levels:

- required: Pods *must* be scheduled to different Nodes. If a Pod cannot be
  scheduled to a different Node from the other Pods in the anti-affinity
  group, then it will not be scheduled.
- preferred (default): Pods *should* be scheduled to different Nodes. There is
  a chance that two Pods in the same anti-affinity group could be scheduled to
  the same node
- disabled: Pods do not have any anti-affinity rules

The `POD_ANTI_AFFINITY` label sets the Pod anti-affinity for all of the Pods
that are managed by the Operator in a PostgreSQL cluster. In addition to the
PostgreSQL Pods, this also includes the pgBackRest repository and any
pgBouncer pods. By default, the pgBackRest and pgBouncer pods inherit the
value of `POD_ANTI_AFFINITY`, but one can override the default by setting
the `POD_ANTI_AFFINITY_PGBACKREST` and `POD_ANTI_AFFINITY_PGBOUNCER` variables
for pgBackRest and pgBouncer respectively

| Name | Default | Required | Description |
|------|---------|----------|-------------|
| `POD_ANTI_AFFINITY` | preferred |  | This will set the default pod anti-affinity for the deployed PostgreSQL clusters. |
| `POD_ANTI_AFFINITY_PGBACKREST` |  |  | This will set the default pod anti-affinity for the pgBackRest pods. |
| `POD_ANTI_AFFINITY_PGBOUNCER` |  |  | This will set the default pod anti-affinity for the pgBouncer pods. |
