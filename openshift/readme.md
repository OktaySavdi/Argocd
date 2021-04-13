**#Install Argocd on Openshift**

We start the installation by creating a new project called Argocd.

![image](https://user-images.githubusercontent.com/3519706/114538510-24028000-9c5c-11eb-9d61-3a19749e1594.png)

Then we easily install ArgoCD operator on OperatorHub.

![image](https://user-images.githubusercontent.com/3519706/114406492-4212a680-9bb0-11eb-997c-5d4f5b09d917.png)

We proceed by clicking the Install button.

![image](https://user-images.githubusercontent.com/3519706/114406579-548ce000-9bb0-11eb-99c1-57211381ab89.png)

We select the relevant channel and the namespace to install and complete the installation.

![image](https://user-images.githubusercontent.com/3519706/114406712-6ec6be00-9bb0-11eb-9834-029aa1b3a82c.png)

It has been successfully installed.

![image](https://user-images.githubusercontent.com/3519706/114406901-93229a80-9bb0-11eb-802e-a3baa7d20433.png)

Now we can go inside the operator and create the ArgoCD Instance.

![image](https://user-images.githubusercontent.com/3519706/114407004-a9305b00-9bb0-11eb-8790-9864824ea76b.png)

I leave it as default and create Instance.

![image](https://user-images.githubusercontent.com/3519706/114407236-dd0b8080-9bb0-11eb-9175-304e132831db.png)

The basic applications required for ArgoCD have been up and running.

![image](https://user-images.githubusercontent.com/3519706/114538645-46949900-9c5c-11eb-9b10-0d4507a02730.png)

![image](https://user-images.githubusercontent.com/3519706/114407484-1c39d180-9bb1-11eb-9fc2-d5cecd6ec925.png)

After successfully creating the route, we can now login. If we want, we can use Openshift SSO here.

![image](https://user-images.githubusercontent.com/3519706/114407606-3a073680-9bb1-11eb-8be9-b7bf4ee190e2.png)

But first, I need to provide the admin password. In the ArgoCD project, I can get it from the secret section as follows.

![image](https://user-images.githubusercontent.com/3519706/114407665-51deba80-9bb1-11eb-8007-5d2295b3073b.png)

After providing the password, we can now log into the system with the admin user.

![image](https://user-images.githubusercontent.com/3519706/114407775-6cb12f00-9bb1-11eb-8a7b-7e2bbabe1fc4.png)

Now I can deploy my application. I'm using the sample repo below for this article. You can fork and customize it for yourself.

![image](https://user-images.githubusercontent.com/3519706/114407896-8eaab180-9bb1-11eb-87ad-d9bcea5a8a0b.png)
