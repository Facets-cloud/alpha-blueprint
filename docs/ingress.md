# Ingress

## Schema Properties

|                                        | Type                                                         | Description                                                                                                                                                                                                                                                                                                                                                               | Required   |
|:---------------------------------------|:-------------------------------------------------------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:-----------|
| conditional_on_intent                  | string                                                       | Flag to enable the resource based on intent availability. eg mysql if mysql dashboard is required to be deployed. Note: Need to have the instance running beforehand to avail.                                                                                                                                                                                            | No         |
| depends_on                             | array                                                        | Dependencies on other resources. e.g. application x may depend on mysql                                                                                                                                                                                                                                                                                                   | No         |
| disabled                               | boolean                                                      | Flag to disable the resource                                                                                                                                                                                                                                                                                                                                              | No         |
| flavor                                 | enum: nginx_ingress_controller, aws_alb, azure_agic, gcp_alb | Implementation selector for the resource. e.g. for a resource type ingress, default, aws_alb, gcp_alb etc.                                                                                                                                                                                                                                                                | Yes        |
| kind                                   | enum: ingress                                                | Describes the type of resource. e.g. ingress, application, mysql etc. If not specified, fallback is the `folder_name`/instances                                                                                                                                                                                                                                           | Yes        |
| lifecycle                              | enum: ENVIRONMENT_BOOTSTRAP                                  | This field describes the phase in which the resource has to be invoked (`ENVIRONMENT_BOOTSTRAP`)                                                                                                                                                                                                                                                                          | No         |
| provided                               | boolean                                                      | Flag to tell if the resource should not be provisioned by facets                                                                                                                                                                                                                                                                                                          | No         |
| version                                | string                                                       | This field can be used to pin to a particular version                                                                                                                                                                                                                                                                                                                     | Yes        |
| metadata.name                          | string                                                       | Name of the resource                                                                                                                                                                                                                                                                                                                                                      | No         |
|                                        |                                                              |     - if not specified, fallback is the `filename`                                                                                                                                                                                                                                                                                                                        |            |
| spec                                   | object                                                       | Specification as per resource types schema                                                                                                                                                                                                                                                                                                                                | Yes        |
| spec.basicAuth                         | boolean                                                      | Enable or disable basic auth                                                                                                                                                                                                                                                                                                                                              | No         |
| spec.domains.KEY.alias                 | string                                                       | Alias naming for the domain                                                                                                                                                                                                                                                                                                                                               | Yes        |
| spec.domains.KEY.certificate_reference | string                                                       | Certificate reference name, if flavor is `aws_alb` then its the ACM ARN certificate reference else `gcp_alb` its the name of the managed certificate that you want facets to create in gcp. In case of `nginx_ingress_controller` its the uploaded k8s certificate referenced as secret. In case of `azure_agic` it is the secret key id of the secret in azure key vault | Yes        |
| spec.domains.KEY.domain                | string                                                       | The host name of the domain                                                                                                                                                                                                                                                                                                                                               | Yes        |
| spec.force_ssl_redirection             | boolean                                                      | Force SSL redirection from http to https                                                                                                                                                                                                                                                                                                                                  | Yes        |
| spec.grpc                              | boolean                                                      | Enable or Disable grpc support in nginx_ingress_controller                                                                                                                                                                                                                                                                                                                | No         |
| spec.ipv6_enabled                      | boolean                                                      | Enable/disable ipv6, this is a cloud specific check if your vpc has ipv6 support enabled                                                                                                                                                                                                                                                                                  | No         |
| spec.private                           | boolean                                                      | Make this load balancer private                                                                                                                                                                                                                                                                                                                                           | Yes        |
| spec.rules.KEY.domain_prefix           | string                                                       | Subdomain prefix for the service                                                                                                                                                                                                                                                                                                                                          | No         |
| spec.rules.KEY.path                    | string                                                       | path of the application                                                                                                                                                                                                                                                                                                                                                   | No         |
| spec.rules.KEY.port                    | string                                                       | Port number of the service                                                                                                                                                                                                                                                                                                                                                | No         |
| spec.rules.KEY.port_name               | string                                                       | Port name of the service                                                                                                                                                                                                                                                                                                                                                  | No         |
| spec.rules.KEY.priority                | integer                                                      | Priority number for the above rule ( this can be from 1 - 1000 ) and it should be unique for each rule - applicable only for `aws_alb` version `0.2`                                                                                                                                                                                                                      | No         |
| spec.rules.KEY.service_name            | string                                                       | The Kubernetes service name of the application                                                                                                                                                                                                                                                                                                                            | No         |

## Outputs

|                                      | Type   | Description                    | Required   | Referencing                                                   |
|:-------------------------------------|:-------|:-------------------------------|:-----------|:--------------------------------------------------------------|
| out.interfaces.KEY.username          | string | Username to connect (if any)   | No         | ${ingress.RESOURCE_NAME.out.interfaces.KEY.username}          |
| out.interfaces.KEY.password          | string | Password to connect (if any)   | No         | ${ingress.RESOURCE_NAME.out.interfaces.KEY.password}          |
| out.interfaces.KEY.host              | string | Host for service discovery     | No         | ${ingress.RESOURCE_NAME.out.interfaces.KEY.host}              |
| out.interfaces.KEY.port              | string | Port for service discovery     | No         | ${ingress.RESOURCE_NAME.out.interfaces.KEY.port}              |
| out.interfaces.KEY.name              | string | Name of interface, same as key | No         | ${ingress.RESOURCE_NAME.out.interfaces.KEY.name}              |
| out.interfaces.KEY.connection_string | string | Connection string to connect   | No         | ${ingress.RESOURCE_NAME.out.interfaces.KEY.connection_string} |
