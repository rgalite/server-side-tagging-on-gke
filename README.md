# server-side-tagging-on-gke


## Installation
Enable the Certificate Manager API:
```
gcloud services enable certificatemanager.googleapis.com
```

Create a certificate map:
```
gcloud beta certificate-manager maps create ssgtm-map
```


```
gcloud certificate-manager dns-authorizations create ssgtm-dns-authorization \
  --domain="ssgtm.mgalite.demo.altostrat.com,ssgtm-preview.mgalite.demo.altostrat.com"
gcloud certificate-manager dns-authorizations describe ssgtm-dns-authorization
```


To create a Google-managed certificate that references the DNS authorization you created in the previous steps, do the following:

```
gcloud certificate-manager certificates create ssgtm-certificate \
  --domains=ssgtm.mgalite.demo.altostrat.com,ssgtm-preview.mgalite.demo.altostrat.com --dns-authorizations=ssgtm-dns-authorization,ssgtm-preview-dns-authorization
```

Create a certificate map that references the certificate map entry associated with your certificate:
```
gcloud certificate-manager maps create ssgtm-certificate-map
```


```
gcloud certificate-manager maps entries create ssgtm-certificate-map-entry-preview \
  --map="ssgtm-certificate-map" \
  --certificates="ssgtm-certificate" \
  --hostname="ssgtm-preview.mgalite.demo.altostrat.com"

gcloud certificate-manager maps entries create ssgtm-certificate-map-entry-tagging \
  --map="ssgtm-certificate-map" \
  --certificates="ssgtm-certificate" \
  --hostname="ssgtm.mgalite.demo.altostrat.com"
```
