# kubernetes-best-practices

With every new technology that emerges, comes its own set of challenges. The latest trend in the market i.e be it containers or Kubernetes isn’t an exception. Discussions galore around this topic and are still being done on what is considered as ‘Production Ready’ in this relatively new landscape. In regards to this paradigm shift, more often than not we find ourselves caught between the common do’s and don’t to which we would like to present a list of ‘things to take care of’ as a coherent set of ‘Best Practices’ that we have learned as part of our experience of deploying and managing Kubernetes in production.

We have grouped these best practices into four different groups for better categorisation and to have a clear understanding of ownership around them. That being said, always remember,

Security is not an individual’s responsibility it’s always the outcome of a joint effort.
Without any further ado, here are the four categories:

• General: Tasks that is common to both the primary teams (Dev & Ops) in the Delivery chain.

• Security: Tasks that can directly affect the overall cluster and infrastructure security.

• Developers: Tasks that should be taken in account by the developers at time of building the Docker image itself.

•Operations: Tasks that falls under the responsibility of the Ops team.

1. General
— — —

• Make sure to use the multi-stage build for your Docker images as much as possible

• Log and monitor everything you care about and remember: If its not monitored it doesn’t exist
• Leverage the Build cache and use the builder pattern to decrease your build time through faster build process

• Always use small base image keeping the number of layers minimised so that you build small images with less attack surface

• Always tag your images and don’t use the latest tag

2. Security
— — —

• Make sure to always scan all your Docker Images and Containers for potential threats
• Never use any random Docker Image(s) and always use authorised images in your environment

• Categorise and accordingly split up your cluster through Namespace

• Use Network Policies to implement proper network segmentation and Role Based Access Control(RBAC) to create administrative boundaries between resources for proper segregation and control

• Limit SSH access to Kubernetes nodes, and Ask users to use kubectl exec instead.

• Never use Passwords, or API tokens in plain text or as environment variables, use secrets instead
• Use non-root user inside container with proper host to container, UID and GID mapping

3. Developers
— — —

• In case of failure don’t just restart, rather crash cleanly

• Log your application to container’s stdout & stderr

• Each container should have only one concern and Try as much as possible to have only one process per container
• Use a process manager such as dumb-init to prevent zombie processes

• Make sure to always use Readiness & Liveness probes

4. Operations
— — —

• Ensure that all logs are stored in a central log hub

• Use the ‘record’ option whenever performing updates for easier rollbacks

• For the purpose of bootstrapping don’t use sidecar, Use init container instead

• Ensure that the Readiness & Liveness probes are always properly utilised and monitored
