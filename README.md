## This is for the non-deprecated version of Minio, ignore
https://github.com/minio/operator/tree/master/helm/operator


helm repo add minio https://operator.min.io/

helm install \
  --namespace minio-operator \
  --create-namespace \
  minio-operator minio/operator

kubectl get secret $(kubectl get serviceaccount console-sa --namespace minio-operator -o jsonpath="{.secrets[0].name}") --namespace minio-operator -o jsonpath="{.data.token}" | base64 --decode

kubectl --namespace minio-operator port-forward svc/console 9090:9090

helm install --namespace minio-tentant \
--create-namespace tenant minio/tenant


-------

## Snippets for the depecreated Azure Gateway Minio

STORAGEACCOUNTNAME=miniotest123
STORAGEACCOUNTKEY=i3psRqmEWdn53UH4jPEjvdDp4lvUHbfCL5K3BiwxJOYVPm+CmrAXLH6Ku2Fg3UnktFTHAwiyBTYWcp97ZBWwxg==


helm upgrade --install --wait minio minio/minio --set azuregateway.enabled=true --set accessKey=$STORAGEACCOUNTNAME --set secretKey=$STORAGEACCOUNTKEY --set service.type=LoadBalancer --values values.yaml
From: https://github.com/Azure/azure-quickstart-templates/blob/master/application-workloads/minio/minio-azure-gateway/scripts/minio.sh


helm upgrade --install --wait minio minio/minio -f values.yaml


## References

https://github.com/Azure/azure-quickstart-templates/blob/master/application-workloads/minio/minio-azure-gateway/scripts/minio.sh
https://joachim8675309.medium.com/using-azure-blob-storage-d31954f5cb0f
https://cloudblogs.microsoft.com/opensource/2017/11/09/s3cmd-amazon-s3-compatible-apps-azure-storage/
