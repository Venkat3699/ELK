##### ArgoCD Installation:
=========================
```
    kubectl create namespace argocd
    kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
    kubectl get all -n argocd
    kubectl get svc -n argocd
    kubectl edit svc argocd-server -n argocd		[Here change service type from ClusterIP to LoadBalancer]
    kubectl get svc -n argocd		[Using DNS we can access ArgoCD, UserName: admin, Password: Check with below commands]
    kubectl get secrets -n argocd
    kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
```
    - Copy the Password carefully & Paste it in ArgoCD Login
	- Once Login, Click on Userinfo and Update the Password

ArgoCD Steps for GitOps:
=======================
Click on ArgoCD Settings -> click on Repositories -> Click on Connect Repo -> Choose via HTTPS -> type: git -> 
project -> default (other wise we can create the project) ->  Repository URL: provide deployment github URL -> 
Provide Credentials (Username & Password) -> Click on Connect (top).

Click on Applications -> click on New App -> Application Name: bankapp -> ProjectName: default -> sync policy: Automatic -> Enable Self Heal -> 
Enable Auto Create Namespace -> Source: Select RepositoryURL -> Revision: master (based on our deployment file branches) -> path: . -> 
Destination: ClusterURL: Select URL -> Namespace: bankapp -> Go to Directory: Enable Directory recurse -> Click on Create.
