# cvm

Tinfoil Containers config repo for the [hush](https://github.com/Pilgrim-Xzed) confidential
bot computer. This repo must stay public: Tinfoil's release workflows compute and sign the
enclave measurement from it, and clients verify attestation against those releases.

- `tinfoil-config.yml` — the measured enclave config. It pins the computer image by SHA-256
  digest; hush connects to deployed instances with attested, certificate-pinned TLS.
- `.github/workflows/` — Tinfoil's release workflows (from `tinfoilsh/tinfoil-containers-template`).
  Cut a release with the **Tinfoil Release** workflow (version input, e.g. `v0.0.1`); wait for
  both workflow runs to finish before deploying that tag.

The image source lives in the hush repo under `infra/computer`; publish a new image with
`pnpm computer:publish <registry-ref>` there and pin the printed digest here. The
`HUSH_CONTROL_TOKEN` secret is declared by name only — its value lives in Tinfoil's secret
store, never in this repo.
