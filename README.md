# renovate-auth-repro

`.npmrc` configures a private registry as the source for all packages.

The Renovate config has a `hostRules` block for that private registry with an invalid `token` and `abortOnError: true`. (I've also seen this issue on self-hosted with invalid GitHub tokens.)

```json
{
  "matchHost": "https://pkgs.dev.azure.com/uifabric/renovate-repros/_packaging/demo-feed/npm/registry/",
  "hostType": "npm",
  "token": "not a token",
  "abortOnError": true
}
```

If you run Renovate on the repo and search the logs for `401`, you can see there are many errors, but the job registered as successful despite the `abortOnError` setting.
