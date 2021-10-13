# AWS-Blue-Green-Management
DevOps Blue/Green Management Tool for AWS Route53

#### Pre-requisites
* Python 3.7
* At least one network load balancer with an alias record
* Local environment variables containing an unexpired AWS Access Key, Secret Access Key, and Session Token with sufficient access to AWS Route53
  * `export AWS_SECRET_ACCESS_KEY=(secret access key)`
  * `export AWS_SESSION_TOKEN=(session token)`

#### Usage

##### Help
`aws-alias-mgmt -h` [`--help`]

##### Options

* `-a` ACTION, `--action` = ACTION
  * ACTION = [C]reate, [D]elete, or [U]pdate
    * Non-existent alias records require creation before updating

* `-t` TARGET, `--target` = TARGET
  * Name of a target load balancer name excluding trailing DNS formating
    * i.e., `blue-nlb` for blue-nlb.<your account>.<your region>.aws.<hosted zone tld> load balancer.

* `-l` ALIAS, `--alias` = ALIAS
  * New or existing alias name excluidng trailing DNS formating
    * i.e., `example-alias` for example-nlb-a.<your account>.<your region>.aws.<hosted zone tld> alias record.

* `-f` [default]
  * Do not enable 'EvaluateTargetHealth' upon Create or Update.

* `-e`
  * Enable 'EvaluateTargetHealth' upon Create or Update.

##### Examples

  * Update target for 'example-alias' alias to 'blue-nlb' load balancer
    * `aws-alias-mgmt -a U -t blue-nlb -l example-alias -r us-east-1`
  * Create new alias named 'example-alias-b' pointing to 'blue-nlb' load balancer
    * `aws-alias-mgmt -a create -t blue-nlb -l example-alias-b -r us-east-1`
  * Update target for 'example-alias' alias to 'green-nlb' load balancer with 'EvaluateTargetHealth'
    * `aws-alias-mgmt -a u -t green-nlb -l example-alias -r us-east-1 -e`

