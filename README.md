# keycloak-gitops
## First, we install the argocd operator:
```
oc apply -k bootstrap/argocd
```

## Second, we install the Red Hat Single Sign Dev Environment using Red Hat Single Sign On Operator
```
oc apply -k bootstrap/deploy/application/01_rhsso-dev
```

## get the route to RH SSO
```
oc get route keycloak -n rhsso-dev --template='https://{{.spec.host}}'
```

## get the password of the user admin
```
oc get secret credential-rhsso-dev -n rhsso-dev -o jsonpath="{.data['ADMIN_PASSWORD']}" | base64 -d
```

# Install Database for prod
## add values to secret for DB
```
oc apply -k bootstrap/deploy/application/02_rhsso-prod
```


based on https://developers.redhat.com/articles/2023/04/10/how-deploy-single-sign-code-using-gitops

