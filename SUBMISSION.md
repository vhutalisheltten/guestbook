# Guestbook Final Project Submission

This fork completes the supplied IBM Guestbook starter repository.

## Task 1: Updated Dockerfile

File: `v1/guestbook/Dockerfile`

The placeholders are completed with `COPY` instructions and `EXPOSE 3000`.

## Task 2: IBM Cloud Container Registry v1 image

Replace `YOUR_NAMESPACE`, then run:

```sh
cd v1/guestbook
docker build -t us.icr.io/YOUR_NAMESPACE/guestbook:v1 .
docker push us.icr.io/YOUR_NAMESPACE/guestbook:v1
ibmcloud cr images
```

Submit the real terminal output.

## Task 3: Default title and heading

File: `v1/guestbook/public/index.html`

```html
<title>Lavanya's Guestbook - v1</title>
<h1>Guestbook - v1</h1>
```

## Horizontal Pod Autoscaling

```sh
kubectl apply -f v1/guestbook/deployment.yml
kubectl apply -f v1/guestbook/service.yml
kubectl autoscale deployment guestbook --cpu-percent=5 --min=1 --max=10
kubectl get hpa guestbook
```

## Task 6: Push updated v2 image

```sh
cd v2/guestbook
docker build -t us.icr.io/YOUR_NAMESPACE/guestbook:v2 .
docker push us.icr.io/YOUR_NAMESPACE/guestbook:v2
```

Submit the real push output including the digest.

## Task 8: Updated title and heading

File: `v2/guestbook/public/index.html`

```html
<title>Guestbook - v2</title>
<h1>Guestbook - v2</h1>
```

## Rolling update and rollback

```sh
kubectl set image deployment/guestbook guestbook=us.icr.io/YOUR_NAMESPACE/guestbook:v2 --record
kubectl apply -f v1/guestbook/deployment.yml
kubectl delete hpa guestbook
kubectl scale deployment guestbook --replicas=1
kubectl rollout history deployment/guestbook
kubectl rollout history deployments guestbook --revision=2
kubectl rollout undo deployment/guestbook --to-revision=1
kubectl get rs
```
