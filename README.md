# binder-repo

> This is an example repository to host and deploy Jupyter notebooks. 
> The notebook files are hosted in a public git repository (github, gitlab, bitbucket, etc.).
> The deployment of the notebooks is done by Binder through a special link or button.
> This also includes a workflow that triggers the build on mybinder.org. 
> This should reduce the wait time for users.

[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/maxb2/binder-repo/HEAD)

The button above will launch a Jupyter server at the root of this repository.

## Projects

### TDKS

[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/maxb2/binder-repo/HEAD?filepath=projects%2Ftdks%2Ftdks.ipynb)

This program solves the 1D Kohn-Sham equation for two electrons in a harmonic-oscillator potential. It first calculates the self-consistent ground state, and then does a time propagation, assuming a short "kick".
