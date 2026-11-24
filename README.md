# medlab-k3s

GitOps config for my k3s homelab, managed by Argo CD using the app-of-apps pattern.

## Layout

```
bootstrap/root.yaml   # root Argo CD app → watches apps/
apps/<name>.yaml      # one Argo CD Application per service
apps/<name>/          # Kubernetes manifests for that service
```

## Apps

| App         | Namespace    | Description              |
|-------------|--------------|--------------------------|
| uptime-kuma | `monitoring` | Uptime monitoring        |
| searxng     | —            | Metasearch engine        |

## Bootstrap

Requires k3s (Traefik + `local-path` storage) and Argo CD installed in the `argocd` namespace.

```sh
kubectl apply -f bootstrap/root.yaml
```

Argo CD then syncs everything under `apps/` automatically.

## Adding an app

1. Put manifests in `apps/<name>/`
2. Add an `Application` at `apps/<name>.yaml` pointing to that folder
3. Push — Argo CD does the rest

## License

[MIT](LICENSE)
