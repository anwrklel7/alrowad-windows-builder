# AL-ROWAD Logistics — Windows Builder

This **public repository contains no application source code, certificate, customer data, release binary, or private configuration**. It exists solely to run a manually triggered Windows build on a public GitHub Actions runner.

## Security boundary

The private application source remains in [`anwrklel7/alrowad-logistics`](https://github.com/anwrklel7/alrowad-logistics). The workflow retrieves it only during a manually started job and uses the following repository secrets:

| Secret | Purpose | Minimum permission |
|---|---|---|
| `PRIVATE_SOURCE_READ_TOKEN` | Read the private application repository during the build | Fine-grained token limited to `Contents: Read` on `alrowad-logistics` only |
| `WINDOWS_SIGNING_CERTIFICATE_BASE64` | Base64-encoded PFX code-signing certificate | Repository secret |
| `WINDOWS_SIGNING_CERTIFICATE_PASSWORD` | Password for the PFX certificate | Repository secret |

The workflow runs only through **Actions → Build AL-ROWAD Windows Installer → Run workflow**. It does not run on pushes or pull requests. It disables persistent checkout credentials and uploads only the final installer artifact for seven days.

## Operating the build

1. Create a fine-grained personal access token restricted to **Contents: Read** for the private source repository only.
2. Add the three secrets above to this builder repository.
3. Open the Actions tab, select the build workflow, and run it with `main` or a specific private commit SHA.
4. Download `AlRowad-Setup-Windows` from the completed workflow artifact.

Never store source files, `.pfx` files, passwords, access tokens, or compiled installers in this public repository.
