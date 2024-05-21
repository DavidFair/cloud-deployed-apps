Notes from prototype
====================

- Install SOPS: https://github.com/getsops/sops
- Install age: https://github.com/FiloSottile/age or `apt-get install age` for 22.04+

Setup / Creating a SOPS secret
------------------------------

- Generate a personal private key for age:
```
mkdir -p ~/.config/sops/age
age-keygen >> ~/.config/sops/age/keys.txt
```

- The .sops.yaml file is used to specify which public keys get automatically associated
  with the encrypted file. Add yours to the relevant sections following existing file sections

- Add or edit your secret as follows:
```
cd secrets/dev  # Currently we have to be in the same dir
sops example-secret.yaml
```

- Add the generated secret to the K8s ArgoCD deployment:
```
kubectl -n argocd create secret generic helm-secrets-private-keys --from-file=key.txt=age-key.txt
```