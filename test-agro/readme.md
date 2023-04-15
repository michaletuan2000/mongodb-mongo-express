
# apply all 
    ka -f 1.mongodb-secret.yaml
    ka -f 2.mongo-deployment.yaml
    ka -f 3.mongo-configmap.yaml
    ka -f 4.mongo-express-deployment.yaml
    ka -f 5.mongo-express-ingress.yaml

# delete all
    kd -f 1.mongodb-secret.yaml
    kd -f 2.mongo-deployment.yaml
    kd -f 3.mongo-configmap.yaml
    kd -f 4.mongo-express-deployment.yaml
    kd -f 5.mongo-express-ingress.yaml

# start argocd
    k port-forward svc/argocd-server -n argocd 8080:443

# run argocd-application
    ka -f 0.argo-application.yaml
    
# get password:
    k -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d && echo

# Test git push and automatic pull
(change '4.mongo-express.yaml' first)

    git add 4.mongo-express.yaml && git commit -m "changed" && git push

# run ngrok
    ngrok http --host-header=localhost https://localhost:8080
 
 You will get one url like this:   https://f396-158-181-71-25.ngrok-free.app
 

 Write the url in webhook of github with the pattern: https://github.com/cusernamepilot/mongodb-mongo-express/settings/hooks/409175949
 
    https://f396-158-181-71-25.ngrok-free.app/api/webhook

