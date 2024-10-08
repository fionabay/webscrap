# IntraDay Volume Forecast by MLFlow on EKS

<img width="184" alt="image" src="https://github.com/user-attachments/assets/c9398fb6-9479-4746-901c-51f0920d0e89">


- Step 1 ) Create a cluster, e.g. EKS, by
   - kind create cluster --config=kind-local.yaml
- Step 2 )  KubeFlow componets such as KNative following below instructions 
   - https://github.com/kubeflow/manifests?tab=readme-ov-file#install-individual-components)
- Step 3) Install network layer Istio
   - https://knative.dev/docs/install/installing-istio/
- Step 4) Install cert manager
   - kubectl apply -f https://github.com/cert-manager/cert-manager/releases/download/v1.15.3/cert-manager.yaml
- Step 5) Install KServ and KServ Runtime
   - kubectl apply -f https://github.com/kserve/kserve/releases/download/v0.10.0/kserve.yaml
   - kubectl apply -f https://github.com/kserve/kserve/releases/download/v0.10.0/kserve-runtimes.yaml
- Step 6 ) Initialize a Python project by Poetry and add dependencies in pyproject.toml 
- Step 7 ) Subclass Kserve.Model,buildpack the custom model to a Docker image 
- Step 8)  Deploy by kubectl apply -f deployment.yaml
- Step 9)  In a bad scenario, one probably will see Internal error occurred: failed calling webhook "inferenceservice.kserve-webhook-server.defaulter": failed to call webhook: Post "https://kserve-webhook-server-service.kserve.svc:443/mutate-serving-kserve-io-v1beta1-inferenceservice?timeout=10s": dial tcp X.X.X.192:443: connect: connection refused
- Step 10) A quick workaround is to delete webhook config as below
  - kubectl delete mutatingwebhookconfigurations.admissionregistra  inferenceservice.serving.kserve.io
  - kubectl delete validatingwebhookconfigurations.admissionregistration.k8s.io  inferenceservice.serving.kserve.io
