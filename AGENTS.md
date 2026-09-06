# terraform-provider-catalystcenter

Agent context for the Terraform Provider for Cisco Catalyst Center.

## Project overview

- Language: Go ≥ 1.25
- Build/package: Go modules (`go.mod`), Terraform provider plugin protocol
- Layout: Terraform provider resources and data sources at the repo root; generated docs under `docs/`; usage examples under `examples/`; code generation helpers under `gen/`.
- Registry: published as `CiscoDevNet/catalystcenter` on the Terraform Registry.

## Setup commands

```bash
# Build and install the provider binary into $GOPATH/bin
go install
```

To use a locally built provider, place the binary in your Terraform plugins directory and run `terraform init`.

## Run / test / lint commands

```bash
# Run unit tests
go test ./...

# Run acceptance tests (creates real Catalyst Center resources)
make testacc
# Equivalent to:
# TF_ACC=1 go test ./... -v -timeout 120m

# Generate or update provider documentation
go generate

# Tidy modules
go mod tidy
```

Acceptance tests require environment variables such as `CC_USERNAME`, `CC_PASSWORD`, and `CC_URL` pointing to a real Catalyst Center instance.

## Key conventions

- Conventional Go project structure with Terraform SDKv2/framework patterns.
- `go generate` produces documentation in `docs/`; do not hand-edit generated files there.
- Add dependencies with `go get`, then run `go mod tidy` and commit `go.mod` and `go.sum`.
- Acceptance tests are gated behind `TF_ACC=1` and create real resources.

## Important gotchas

- Go 1.25+ and Terraform ≥ 1.0 are required.
- Provider was validated against Catalyst Center 2.3.7.10/2.3.7.11 and 3.1.5.
- The default `make` target is `testacc`, which runs acceptance tests against live infrastructure—ensure credentials and environment variables are set before running it blindly.
- Documentation at `https://registry.terraform.io/providers/CiscoDevNet/catalystcenter/latest/docs` is the authoritative user-facing reference.

## Useful shortcuts

```bash
# Quick build
go install

# Regenerate docs
go generate

# Run unit tests only (no live resources)
go test ./...
```
