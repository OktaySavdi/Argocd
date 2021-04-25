**#Install Argocd on Openshift**
```
Red Hat  Openshift       : 4.7.x
Red Hat  Openshift Gitops: 1.1.0
```

## Install OpenShift GitOps

Log into OpenShift Web Console as a cluster admin and navigate to the  **Administrator**  perspective and then  **Operators**  →  **OperatorHub**.

In the  **OperatorHub**, search for  _OpenShift GitOps_  and follow the operator install flow to install it.

![image](https://user-images.githubusercontent.com/3519706/114406492-4212a680-9bb0-11eb-997c-5d4f5b09d917.png)

We proceed by clicking the Install button.

![image](https://user-images.githubusercontent.com/3519706/115990845-2b1b7d80-a5ce-11eb-924e-a22530d49562.png)

We select the relevant channel and the namespace to install and complete the installation.

![image](https://user-images.githubusercontent.com/3519706/114406712-6ec6be00-9bb0-11eb-9834-029aa1b3a82c.png)

It has been successfully installed.

![image](https://user-images.githubusercontent.com/3519706/115990885-65851a80-a5ce-11eb-92fc-5729a8203cf1.png)

Once OpenShift GitOps is installed, an instance of Argo CD is automatically installed on the cluster in the `openshift-gitops` namespace and link to this instance is added to the application launcher in OpenShift Web Console.

![image](https://user-images.githubusercontent.com/3519706/115990913-8baaba80-a5ce-11eb-9a76-ef940f9f2594.png)

![image](https://user-images.githubusercontent.com/3519706/115990972-d1678300-a5ce-11eb-850e-10025817db58.png)

After successfully creating the route, we can now login. If we want, we can use Openshift SSO here.

![image](https://user-images.githubusercontent.com/3519706/114407606-3a073680-9bb1-11eb-8be9-b7bf4ee190e2.png)

But first, I need to provide the admin password. In the ArgoCD project, I can get it from the secret section as follows.

![image](https://user-images.githubusercontent.com/3519706/115991036-11c70100-a5cf-11eb-8b22-b52371901d5b.png)

After providing the password, we can now log into the system with the admin user.

![image](https://user-images.githubusercontent.com/3519706/114407775-6cb12f00-9bb1-11eb-8a7b-7e2bbabe1fc4.png)

**ArgoCD CLI Setup**
After installing, we need to login to ArgoCD system.
```
VERSION=$(curl --silent "https://api.github.com/repos/argoproj/argo-cd/releases/latest" | grep '"tag_name"' | sed -E 's/.*"([^"]+)".*/\1/')
```
Then we can download our cli file.
```
curl -sSL -o /usr/local/bin/argocd https://github.com/argoproj/argo-cd/releases/download/$VERSION/argocd-linux-amd64
```
I am giving the execute right to make it executable.
```
chmod +x /usr/local/bin/argocd
```
Now we can manage argocd from the command line. Now we are making a login test.

**--- Get route ---**  
```
ARGOCD_ROUTE=$(oc -n openshift-gitops get route openshift-gitops-server -o jsonpath='{.spec.host}')
```
**--- Get Admin password ---**  
```
ARGOCD_SERVER_PASSWORD=$(oc get secret openshift-gitops-cluster -o jsonpath='{.data.admin\.password}' | base64 -d)
```
**--- Login to ArgoCD API ---**  
```
argocd --insecure --grpc-web login ${ARGOCD_ROUTE}:443 --username admin --password ${ARGOCD_SERVER_PASSWORD}
```

Before, I login to Openshift environment with an authorized service account.

![image](https://user-images.githubusercontent.com/3519706/115991518-74b99780-a5d1-11eb-940f-0c541713460c.png)

After installing, we need to login to ArgoCD system.

![image](https://user-images.githubusercontent.com/3519706/115991623-0de8ae00-a5d2-11eb-9ae6-8e2cf7dabb37.png)

After logging in, I run the following command to list my existing clusters.

![image](https://user-images.githubusercontent.com/3519706/115991672-4ab4a500-a5d2-11eb-90f5-aaeca8c372f8.png)

Now I add my cluster. First, I log in to Openshift environment with the "oc login" command.

![image](https://user-images.githubusercontent.com/3519706/115991736-86e80580-a5d2-11eb-909e-1db0834a9af2.png)

I'm listing my clusters again.

![image](https://user-images.githubusercontent.com/3519706/115991783-bdbe1b80-a5d2-11eb-8dfb-42f5d3e057f3.png)

Now I can deploy my application. I'm using the sample repo below for this article. You can fork and customize it for yourself.

![image](https://user-images.githubusercontent.com/3519706/114407896-8eaab180-9bb1-11eb-87ad-d9bcea5a8a0b.png)

**#example1**
```
Repository : https://github.com/OktaySavdi/gitops-example.git
Revision:  : HEAD
Path       : dev
Namespace  : gitops-dev
```
**#example2**
```
Repository : https://github.com/emreozkangit/gitops-examples.git
Revision:  : master
Path       : guestbook
Namespace  : default
```
