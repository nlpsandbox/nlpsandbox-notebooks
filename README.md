[![nlpsandbox.io](https://nlpsandbox.github.io/nlpsandbox-themes/banner/Banner@3x.png)](https://nlpsandbox.io)

# NLP Sandbox Notebooks

[![GitHub Release](https://img.shields.io/github/release/nlpsandbox/nlpsandbox-analysis.svg?color=94398d&labelColor=555555&logoColor=ffffff&style=for-the-badge&logo=github)](https://github.com/nlpsandbox/nlpsandbox-analysis/releases)
[![GitHub CI](https://img.shields.io/github/workflow/status/nlpsandbox/nlpsandbox-analysis/CI.svg?color=94398d&labelColor=555555&logoColor=ffffff&style=for-the-badge&logo=github)](https://github.com/nlpsandbox/nlpsandbox-analysis)
[![GitHub License](https://img.shields.io/github/license/nlpsandbox/nlpsandbox-analysis.svg?color=94398d&labelColor=555555&logoColor=ffffff&style=for-the-badge&logo=github)](https://github.com/nlpsandbox/nlpsandbox-analysis/blob/main/LICENSE)

## Introduction

TBA

## Specification

- NLP Sandbox schemas version: 1.2.0
- NLP Sandbox notebooks version: TBA

## Requirements

- [Docker Engine] >=19.03.0
- [Synapse.org] user account

## Notebooks

Rmd Notebook | Description | HTML Notebook
-------- | ----------- | -------------
[generate-dataset.Rmd](notebooks/generate-dataset.Rmd)         | Generation of the i2b2 PHI dataset for the NLP Sandbox.                                | [![HTML notebook](https://img.shields.io/badge/latest-blue.svg?color=1283c3&labelColor=555555&logoColor=ffffff&style=for-the-badge&logo=github)](https://nlpsandbox.github.io/i2b2-phi-dataset/latest/notebooks/generate-dataset.html)

> Important: Please make sure when you write your own notebooks that no
> sensitive information ends up being publicly available. Please check with the
> information security officer of your organization to confirm that the approach
> described here can be applied to your use case.

## Usage

1. Create and edit the configuration file.

       cp .env.example .env

2. Start RStudio. Add the option `-d` or `--detach` to run in the background.

       docker compose up

RStudio is now available at http://localhost. On the login page, enter the
default username (`rstudio`) and the password specified in `.env`.

To stop RStudio, enter `Ctrl+C` followed by `docker compose down`.  If running
in detached mode, you will only need to enter `docker compose down`.

## Configuring the CI/CD workflow

The [CI/CD workflow] of this repository performs the following actions:

- Generate HTML notebooks from R notebook and publishes them to GitHub Pages.
- Build the Docker image [docker.synapse.org/syn22277123/i2b2-phi-dataset] and
  push it to Synapse Docker Registry.

If you decided to fork this repository, you will need to update the environment
variables defined at the top of the [CI/CD workflow]. You also need to create
the following [GitHub Secrets]:

- `RSTUDIO_PASSWORD`: Random password.
- `SYNAPSE_USERNAME`: Your [Synapse.org] username.
- `SYNAPSE_TOKEN`: A [personal access token (PAT)] that has the permissions
  `View`, `Download` and `Modify`.

## Versioning

### GitHub tags

This repository uses [semantic versioning] to track the releases of this
project. This repository uses "non-moving" GitHub tags, that is, a tag will
always point to the same git commit once it has been created.

### GitHub Pages

The artifact published by this repository are HTML notebooks published to GitHub
Pages and the Docker image [docker.synapse.org/syn22277123/i2b2-phi-dataset].

The table below describes the GH Pages tags available.

| Tag name                    | Moving | Description
|-----------------------------|--------|------------
| `latest`                    | Yes    | Latest stable release.
| `edge`                      | Yes    | Latest commit made to the default branch.
| `edge-<sha>`                | No     | Same as above with the reference to the git commit.
| `<major>.<minor>.<patch>`   | No     | Stable release.

You should avoid using a moving tag like `latest` when deploying containers in
production, because this makes it hard to track which version of the image is
running and hard to roll back.

## License

[Apache License 2.0]

<!-- Links -->

[NLPSandbox.io]: https://nlpsandbox.io
[semantic versioning]: https://semver.org/
[Apache License 2.0]: https://github.com/nlpsandbox/nlpsandbox-analysis/blob/main/LICENSE
[renv.lock]: renv.lock
[conda/i2b2-phi-dataset/environment.yml]: conda/i2b2-phi-dataset/environment.yml
[CI/CD workflow]: .github/workflows/ci.yml
[Docker Engine]: https://docs.docker.com/engine/install/
[docker.synapse.org/syn22277123/i2b2-phi-dataset]: https://www.synapse.org/#!Synapse:syn25813728
[2014 i2b2 NLP De-identification Challenge]: https://dx.doi.org/10.1016%2Fj.jbi.2015.06.007
[2014 i2b2 NLP De-identification Challenge Dataset]: https://portal.dbmi.hms.harvard.edu/projects/n2c2-nlp/
[NLP Sandbox schemas]: https://github.com/nlpsandbox/nlpsandbox-schemas
[Synapse.org]: https://synapse.org
[NLP Sandbox Data Node]: https://github.com/nlpsandbox/data-node
[NLP Sandbox CLI]: https://github.com/nlpsandbox/nlpsandbox-client
[GitHub Secrets]: https://docs.github.com/en/actions/reference/encrypted-secrets
[personal access token (PAT)]: https://help.synapse.org/docs/Managing-Your-Account.2055405596.html
