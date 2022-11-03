<p align="center">
 <img src="https://github.com/bard-rr/.github/blob/main/profile/Asset%2010-8.png?raw=true" width="500">
</p>
 
# Bard

<!-- toc -->

- [Description](#Description)
- [Usage](#usage)
- [Commands](#commands)
- [Scripting](#scripting)
<!-- tocstop -->

# Description

Bard is a session replay tool that can be auto-deployed to AWS or set up using a docker-compose. Bard includes a session recorder and a session replayer. This tool will allow you to easily create user conversion funnels and view exactly why a user did not complete the conversion while also identifying sessions that experience errors on the front end of your application.

# Usage

## Prerequisites

- an [AWS account](https://portal.aws.amazon.com/gp/aws/developer/registration/index.html?nc2=h_ct&src=default&tag=soumet-20)
- `npm` is [installed](https://www.npmjs.com/get-npm)
- the AWS CLI is [installed](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html?tag=soumet-20) and configured
- an [AWS named profile](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-profiles.html)
- the AWS CDK command-line tool is [installed](https://docs.aws.amazon.com/cdk/latest/guide/cli.html?tag=soumet-20)

## Recorder

First install the npm package into your project.

```
npm install bardrr
```

In your project you need to import the `Agent` front the `bardrr` npm package. Then run the `start` method on the Agent passing an object as the argument with
the properties `appName` that will be the name of this specific application, and `endpoint` which is the location of the replayer. Example:

```
import Agent from "bardrr"

new Agent().start({appName: "Party App", endpoint: "http://www.myfancyapp.com"});
```

More Information can be found [Here](https://github.com/bard-rr/agent)

## Replayer

??????????
