# Brightbox Docker Containers

This repository automatically builds docker containers containing tools
to access the Brightbox cloud.

* Brightbox Cloud CLI
* Terraform

The docker containers are built once a week, ensuring you always have
the latest tools available. Just replace your usual command line with
the equivalent `docker run` command.

### Brightbox Cloud CLI Usage

[Brightbox Cloud CLI](https://www.brightbox.com/docs/guides/cli/)
requires a working directory which can store the config. You can map
any directory you like, or you can co-opt the default one created by a
local cli command. You can use this directory with the following:
```shell
docker run -it -v ~/.brightbox:/root/.brightbox brightbox/cli <command>
```

For example:
```shell
docker run -it -v ~/.brightbox:/root/.brightbox brightbox/cli accounts
```

```shell
docker run -it -v ~/.brightbox:/root/.brightbox brightbox/cli server create img-6xysw
```

### Terraform Usage

The [Terraform](https://www.brightbox.com/docs/guides/terraform/getting-started/) container includes the terraform tool and the Brightbox
provider plugin, so you're ready to go with no installation. Run
the docker container from the directory containing your terraform
configuration - as you would do with a locally installed tool.

You can use this version with the following:
```shell
docker run -i -t -v $(pwd):/app/ -w /app/ brightbox/terraform <command>
```

For example:
Initialize the plugins (You will only need to do this once)

```shell
docker run -i -t -v $(pwd):/app/ -w /app/ brightbox/terraform init
```

Show the build plan
```shell
docker run -i -t -v $(pwd):/app/ -w /app/ brightbox/terraform plan
```
