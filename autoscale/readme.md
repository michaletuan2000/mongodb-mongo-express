
# apply all 
    ka -f autoscale/1.deployment.yml
    ka -f autoscale/2.hpa.yml


# delete all
    kd -f autoscale/1.deployment.yml
    kd -f autoscale/2.hpa.yml

# test loading
    k run -i --tty load-generator --rm --image=busybox:1.28 --restart=Never -- /bin/sh -c "while sleep 0.01; do wget -q -O- http://php-apache; done"

# watch hpa
    kg hpa php-apache-hpa --watch
