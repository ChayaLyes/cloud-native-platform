# Envoy Gateway

Porte d'entree HTTP du cluster, via la Gateway API.

## Pourquoi pas ingress-nginx

Le projet ingress-nginx a ete retire par Kubernetes en mars 2026 : depot
archive, plus aucune release, aucun correctif de securite. Le comite de
securite de Kubernetes recommande explicitement de migrer vers la Gateway
API ou un controller activement maintenu.

## Pourquoi Envoy Gateway

- Envoy est le proxy de reference du cloud native (projet CNCF diplome),
  deja present sur ce cluster sous le nom cilium-envoy
- Gateway API est l'API officielle qui succede a Ingress
- Installation independante : aucune modification de k3s ni de Cilium

Alternative envisagee et reportee : Cilium Gateway API, plus elegant
(aucun composant supplementaire) mais impose de desactiver kube-proxy
dans k3s et de reconfigurer Cilium.

## Installation

Version epinglee : v1.8.3 (22 juillet 2026)

    helm install eg oci://docker.io/envoyproxy/gateway-helm \
      --version v1.8.3 \
      --namespace envoy-gateway-system \
      --create-namespace

Le chart installe aussi les CRD de la Gateway API.

## Verification

    kubectl -n envoy-gateway-system get pods
    kubectl get gatewayclass
