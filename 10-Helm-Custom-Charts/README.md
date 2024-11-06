```
 349  mkdir 10-Helm-Custom-Charts
  350  cd 10-Helm-Custom-Charts/
  351  ls
  352  helm create my-tiny-web
  353  ls
  354  cd my-tiny-web/
  355  ls
  356  apt-get install tree -y
  357  ls
  358  tree .
  359  cat templates/service.yaml
  360  ls
  361  vim values.yaml
  362  ls
  363  cd ..
  364  ls
  365  helm install my-app my-tiny-web --dry-run
  366  helm install my-app my-tiny-web
  367  helm list
  368  kubectl  get deploy
  369  kubectl  get po
  370  kubectl  get svc
  371  ls
  372  cd my-tiny-web/
  373  ls
  374  vim values.yaml
  375  ls
  376  vim Chart.yaml
  377  ls
  378  cd ..
  379  helm list
  380  helm upgrade my-app my-tiny-web
  381  helm list
  382  kubectl  get po
  383  helm list
  384  helm history my-app
  385  helm rollback my-app
  386  helm history my-app
  387  kubectl get po
```
