
This is based on [@vsoch's](https://github.com/sponsors/vsoch) amazingly useful [singularity-deploy](https://github.com/singularityhub/singularity-deploy) template.

Instead of building the `SIF` directly, my version uses a Dockerfile with the [Docker build-push action](https://github.com/marketplace/actions/build-and-push-docker-images) to upload a Docker image to the [GitHub container registry](https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-container-registry). It then converts the Docker image to `SIF` and stores that in a release as in the original [singularity-deploy](https://github.com/singularityhub/singularity-deploy) template.

Is this useful? I don't know, but I like having the Docker image stored in the registry AND a reproducible container in the assets.

Right now you can only have one Dockerfile per repo, until I work out how to use the `build-push` action to build multiple containers. 

The steps are pretty similar to @vsoch's [orignal repo](https://github.com/singularityhub/singularity-deploy):

1. Template or fork.
2. Edit the repo:
    - Check out a new branch
    - Modify the **`Docker`** recipe (`Dockerfile`)
    - Update the Version file
    - Push the new branch to GitHub
3. Open a PR for the new branch. This triggers the **test** build, which just builds the Docker image but doesn't push it.
4. Once the check passes, merge the PR. This creates a release, re-builds the Docker image, uploads it to GHCR, converts it to `SIF`, and adds the `SIF` to the release.

### Notes

To get the repo to work with GHCR:

- [Enable GHCR for your account](https://docs.github.com/en/packages/working-with-a-github-packages-registry/enabling-improved-container-support-with-the-container-registry).
- Use the following URL to create a Personal Access Token with the scopes `read:packages`, `write:packages` and `delete:packages`. [https://github.com/settings/tokens/new?scopes=write:packages](https://github.com/settings/tokens/new?scopes=write:packages).  
This is documented [here](https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-container-registry#authenticating-to-the-container-registry).
- Add the PAT to the Repository Secrets and call it `CR_PAT` (Settings -> Secrets -> New Repository Secret)

These steps allow the actions runner to authenticate with GHCR and push/pull the images.
