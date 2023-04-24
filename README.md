# my public kubernetes repo



##### .kube/config
```
 mkdir -p $HOME/.kube
 sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
 sudo chown $(id -u):$(id -g) $HOME/.kube/config
```


##### Nginx Ingress Sample
```
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: example-ingress
  annotations:
    nginx.ingress.kubernetes.io/configuration-snippet: |
      if ($host = 'www.demo.foo.com' ) {
        rewrite ^ https://demo.foo.com$request_uri permanent;
      }
    nginx.ingress.kubernetes.io/force-ssl-redirect: "true"
    nginx.ingress.kubernetes.io/server-alias: demo.foo.com
spec:
  rules:
    - host: "demo.foo.com"
      http:
        paths:
          - path: /
            backend:
              serviceName: demo-service
              servicePort: 5678
  tls:
    - hosts:
      - "demo.foo.com"
      secretName: wildcard-foo-com
```
