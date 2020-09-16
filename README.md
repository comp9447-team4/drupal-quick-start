# drupal-quick-start
Follows the Drupal reference deployment: 

* https://aws.amazon.com/quickstart/architecture/drupal/
* https://aws-quickstart.s3.amazonaws.com/quickstart-drupal/doc/drupal-on-the-aws-cloud.pdf

I've written some wrappers to make it easy to deploy & reproduce.

Check them out in `./bin`

These are written in `bash` which glues together AWS commands. This works best under Linux / MacOS.

If you are on Windows, Cygwin / WSL may work but it may not be as smooth.

* https://docs.microsoft.com/en-us/windows/wsl/install-win10
* https://www.cygwin.com/


# Setup prerequisites
This varies by OS but these instructions are for a Debian / Ubuntu based system.
You can also use `brew` for MacOS or Chocolatey for `Windows`.

## Jq
json parsing for API calls

```
sudo apt install direnv jq
```

## Direnv
Setup direnv for environment variables. This is used for substituing environment variables to params.
It's optional, you can just set your environment variables as in `.envrc-demo`.
```
cp .envrc-demo .envrc
direnv allow

echo 'eval "$(direnv hook zsh)"' >> ~/.zshrc
```

## AWS Cli

Setup AWS CLI tools.

Assumes you have setup your IAM user with MFA enabled. If not follow: https://wellarchitectedlabs.com/security/200_labs/200_automated_deployment_of_iam_groups_and_roles/1_cfn_create_iam_groups_policies/

```
sudo apt install python3 python3-pip
pip3 install aws-cli

cp aws-credentials.sample ~/.aws/credentials

# Edit your AWS credentials
vi ~/.aws/credentials
```

## Drupal

https://aws.amazon.com/quickstart/architecture/drupal/

Create a key pair with:

```
./bin/key-pair.sh create
./bin/key-pair.sh describe
```

Make sure you save it.


Deploy the stack with:

```
./bin/stack.sh create
```

## Clean up

```
./bin/key-pair.sh delete
./bin/stach.sh delete
```
