# istio_template


Read this [blog](https://mitul-shahriyar.hashnode.dev/kubernetes-101-part-6#heading-istio) for service mesh concept


start minikube
 minikube start

Enable ingress

minikube addons enable ingress

Download using this
curl -L https://istio.io/downloadIstio | sh -


Then enter into the istio file

cd istio-<version>

ls

We will find these in the folder

bin  LICENSE  manifests  manifest.yaml  README.md  samples  tools

Finally add istio to our  path

export PATH=$PWD/bin:$PATH


Check if Istioctl is installed

istioctl version


Install istio on your cluster

istioctl install --set profile=demo -y


Run this to check if istio-egressgateway, istio-ingressgateway and istiod is running

kubectl get pods -n istio-system

If you want to enable istio in a namespace , you can check if that's enabled or not by this

istioctl analyze

It checks if the default namespace has istio labeled  or not. If that's enabled, whenever one runs a pod, a proxy will also run with it

kubectl label namespace default istio-injection=enabled

Apply this to add istio in the default namespace.



## Install Kiali to visualize service mesh

from your istio-<version folder> apply this code

kubectl apply -f  samples/addons

KIALI will also get installed as an addon

You may see something like this in the output

serviceaccount/kiali created
configmap/kiali created
clusterrole.rbac.authorization.k8s.io/kiali created
clusterrolebinding.rbac.authorization.k8s.io/kiali created
service/kiali created
deployment.apps/kiali created

Check if the kiali deployment is running on istio-system namespace

kubectl rollout status deployment/kiali -n istio-system

kubectl -n istio-system get svc kiali



Then run the KIALI daskboard 
istioctl dashboard kiali
