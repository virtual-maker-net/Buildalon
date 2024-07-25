# Buildalon

Welcome to Buildalon!

Buildalon allows you to:
- Automatically generate build of your Unity project on a VM in the cloud.
- Your entire VM is cached to ensure so iterative builds are fast.
- Automatically run tests.
- Automatically deploy your built app.

Need help? Get support on Discord.

## Prerequisites

- A Unity project you want to build.
- A Unity license to build the project (Personal, Pro, etc.).
- Your Unity project should be pushed to a Github repository.
- Sign up for Buildalon here.

## Install the Buildalon Github App

TODO: need to make the app public to see what the installation page looks like.

## Install com.utilities.buildpipeline

The com.utilities.buildpipeline package adds new command line arguments to the Unity
Editor which will allow you to build your project and run tests in an automation setting.

Visit the [OpenUPM Page](https://openupm.com/packages/com.utilities.buildpipeline/#close)
and select from one of the installation options.

## Create a build workflow

Buildalon Works with Github Actions. You define actions for the runner machine to perform by writing a workflow file. We provide a few samples in the `workflow` directory. Here's how to setup a simple Unity build:

- Create the folder `.github\workflows` in your project repo.
- Copy the [unity-build.yml](workflows\unity-build.yml) workflow into this folder.
- Read through the file and make any changes you need. Most importantly:
  - Set `push/branches` to the branches you want to build on every commit.
  - Set `pull_request/branches` to the branches you want to build when a pull request is created.
  - Set `version-file-path` to the path of your project's `ProjectVersion.txt`.
  - Set `license-type` to `Personal` or `Pro`.
  - Note: The `5mB-windows` label tells Github to run the workflow on a Buildalon runner.

## Add secrets required to activate your license

In order to activate your license, the runner needs to login on your behalf and enter your license serial number.

You can add secrets for an Oranization or single Repo in Github by going to  > `Settings` > `Secrets and variables` > `Actions`.

Add the following secrets:
- `UNITY_USERNAME` The email address you use for your Unity Id
- `UNITY_PASSWORD` The password you use for Unity Id access
- `UNITY_SERIAL` Only required for pro/plus activations.
- `UNITY_2FA_KEY` Only required for personal activations.

<details>
<summary><b>2FA Auth Key Setup Steps (Personal License Only)</b></summary>
To activate new two factor authentication for your Unity account:

1. Login to Unity account and navigate to `Security`
2. Click `+` (activate) next to `Two Factor Authentication`
3. Select `Start setup`
4. Input password if prompted
5. Select `Authenticator App` to receive codes, then `Next`
6. Click `Can't Scan the barcode?`
7. Copy the 16 character key
8. Create new secret `UNITY_2FA_KEY` and save the generated key from the previous step
9. Scan the QR code in your Authenticator app and verify the code.
</details>

## Run a Build!

Commit and push your changes, then visit the `Action` tab in Github to see your build run. Buildalon will allocate a dedicated virtual machine to run your workflow.

The first time it runs, your workflow will install Unity and build your project from scratch. Subsequent runs will use the same virtual machine and build files, which should speed up the build significantly.

For help and questions, be sure to visit our Discord.
