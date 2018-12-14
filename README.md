# terraform_EC2_kitchen

### Purpose of the repository 
- The repository creates EC2 Ubuntu 16.4 instance in AWS and test that instance with `kitchen` framework.

#### List of files in the repository

File name                            | File description 
------------------------------------ | --------------------------------------------------------------
`test/integration/default/inspec.yml` | inspec directory for testing.
`test/integration/controls/operating_system_spec.rb` | basic test to make sure we are running Ubuntu system.
`.gitignore` | which files and directories to ignore in the repository.
`.kitchen.yml` | configuration file for `kitchen` test framework.
`Gemfile` | used for ruby dependencies.
`main.tf` | Terraform configuration file for building EC2 instance.
`variables.tf` | Terraform configuration file with environmental variables.
`output.tf` | Terraform configuration file with output parameters.

### How to use this repository. 
- Install `terraform` by following this [instructions](https://www.terraform.io/intro/getting-started/install.html).
- Clone the repository to your local computer: `git clone git@github.com:nikcbg/terraform_EC2_kitchen`.
- Go to the cloned repo on your computer: `cd terraform_EC2_kitchen`.

### Creating and configuring the AWS box.
### Note: NEVER make your AWS access keys public so you can prevent your account from been compromised.
- To be able to connect to your AWS account without compromising your credentials you need to use environment variables.
- You need to get your secret access and access keys form your AWS account, you can follow this [instructions](https://docs.aws.amazon.com/general/latest/gr/managing-aws-access-keys.html)
- 
- Execute `packer validate template.json` to validate the template.

- Once the box is ready you need to set up your testing environment.

### Setting up `ruby` environment on Ubuntu 16.04 instructions:

Command execution |	Command outcome
------------------|--------------------------
`sudo apt update` | to update the packages on your machine.
`sudo apt-get install autoconf bison build-essential libssl-dev libyaml-dev libreadline6-dev zlib1g-dev libncurses5-dev libffi-dev libgdbm3 libgdbm-dev` | to install ruby dependencies.
`git clone https://github.com/rbenv/rbenv.git ~/.rbenv` | to clone rbenv repo.
`echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc to change your ~/.bashrc file` | to use ruby command line utility.
`'eval "$(rbenv init -)"' >> ~/.bashrc` | so rbenv loads automatically.
`source ~/.bashrc` | to reload bash profile.
`rbenv` | command to verify that `rbenv` is set up properly.

- Next execute the commands in the table below:
Command execution |	Command outcome
------------------|--------------------------
`rbenv install 2.3.1`	| to install ruby 2.3.1 version.
`rbenv local 2.3.1`	| to set the default version of ruby to your local directory.
`rbenv -v`	| to make sure ruby is installed and you have the correct version.
`gem install bundler`	| to install gem which is package manager for ruby.


### Commands needed to test with `kitchen`.

Command execution | Command outcome
------------------|--------------------------------------------------------------
`bundle exec kitchen list` | to list `kitchen` instances.
`bundle exec kitchen converge` | to create `kitchen` environment.
`bundle exec kitchen verify` | command to execute `kitchen` test.
`bundle exec kitchen destroy` | to destroy `kitchen` environment.
`bundle exec kitchen test` | to automatically build, test and destroy `kitchen` environment.

- If the command/s complete successfully the output will display the following:

```
 Profile: default
Version: (not specified)
Target:  local://

  ✔  operating_system: Command: `lsb_release -a`
     ✔  Command: `lsb_release -a` stdout should match /Ubuntu/


Profile Summary: 1 successful control, 0 control failures, 0 controls skipped
Test Summary: 1 successful, 0 failures, 0 skipped
       Finished verifying <default-ubuntu> (0m0.27s).

```


### TO DO: 
- Check if everything works as expected. 
