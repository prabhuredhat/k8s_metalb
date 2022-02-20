# k8s_metallb

Ingress and Metallb Setup in Kubernetes







# Setup Ingress Controller using Haproxy

Haproxy Link: https://haproxy-ingress.github.io/docs/getting-started/

$ helm repo add haproxy-ingress https://haproxy-ingress.github.io/charts

# Create a haproxy-ingress-values.yaml

controller:
  hostNetwork: true

# Install haproxy ingress using helm charts

$ helm install haproxy-ingress haproxy-ingress/haproxy-ingress\
  --create-namespace --namespace ingress-controller\
  --version 0.13.6\
  -f haproxy-ingress-values.yaml



# Metallb Documentation

https://metallb.universe.tf

Kubernetes does not offer an implementation of network load balancers (Services of type LoadBalancer) for bare-metal clusters. The implementations of network load balancers that Kubernetes does ship with are all glue code that calls out to various IaaS platforms (GCP, AWS, Azure…). If you’re not running on a supported IaaS platform (GCP, AWS, Azure…), LoadBalancers will remain in the “pending” state indefinitely when created.

Bare-metal cluster operators are left with two lesser tools to bring user traffic into their clusters, “NodePort” and “externalIPs” services. Both of these options have significant downsides for production use, which makes bare-metal clusters second-class citizens in the Kubernetes ecosystem.

MetalLB aims to redress this imbalance by offering a network load balancer implementation that integrates with standard network equipment, so that external services on bare-metal clusters also “just work” as much as possible.

