## AWS Billing User Guide
The open source version of the AWS Billing docs. You can submit feedback & requests for changes by submitting issues in this repo or by making proposed changes & submitting a pull request.
## License Summary
The documentation is made available under the Creative Commons Attribution-ShareAlike 4.0 International License. See the LICENSE file.
The sample code within this documentation is made available under a modified MIT license. See the LICENSE-SAMPLECODE file.
# This workflow will build and push a new container image to Amazon ECR,
# and then will deploy a new task definition to Amazon ECS, when there is a push to the "main" branch.
#
# To use this workflow, you will need to complete the following set-up steps:
#
# 1. Create an ECR repository to store your images.
#    For example: `aws ecr create-repository --repository-name my-ecr-repo --region us-east-2`.
#    Replace the value of the `ECR_REPOSITORY` environment variable in the workflow below with your repository's name.
#    Replace the value of the `AWS_REGION` environment variable in the workflow below with your repository's region.
#
# 2. Create an ECS task definition, an ECS cluster, and an ECS service.
#    For example, follow the Getting Started guide on the ECS console:
#      https://us-east-2.console.aws.amazon.com/ecs/home?region=us-east-2#/firstRun
#    Replace the value of the `ECS_SERVICE` environment variable in the workflow below with the name you set for the Amazon ECS service.
#    Replace the value of the `ECS_CLUSTER` environment variable in the workflow below with the name you set for the cluster.
#
# 3. Store your ECS task definition as a JSON file in your repository.
#    The format should follow the output of `aws ecs register-task-definition --generate-cli-skeleton`.
#    Replace the value of the `ECS_TASK_DEFINITION` environment variable in the workflow below with the path to the JSON file.
#    Replace the value of the `CONTAINER_NAME` environment variable in the workflow below with the name of the container
#    in the `containerDefinitions` section of the task definition.
#
# 4. Store an IAM user access key in GitHub Actions secrets named `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY`.
#    See the documentation for each action used below for the recommended IAM policies for this IAM user,
#    and best practices on handling the access key credentials.

name: Deploy to Amazon ECS

on:
  push:
    branches: [ "main" ]

env:
  AWS_REGION: MY_AWS_REGION                   # set this to your preferred AWS region, e.g. us-west-1
  ECR_REPOSITORY: MY_ECR_REPOSITORY           # set this to your Amazon ECR repository name
  ECS_SERVICE: MY_ECS_SERVICE                 # set this to your Amazon ECS service name
  ECS_CLUSTER: MY_ECS_CLUSTER                 # set this to your Amazon ECS cluster name
  ECS_TASK_DEFINITION: MY_ECS_TASK_DEFINITION # set this to the path to your Amazon ECS task definition
                                               # file, e.g. .aws/task-definition.json
  CONTAINER_NAME: MY_CONTAINER_NAME           # set this to the name of the container in the
                                               # containerDefinitions section of your task definition

permissions:
  contents: read

jobs:
  deploy:
    name: Deploy
    runs-on: ubuntu-latest
    environment: production

    steps:
    - name: Checkout
      uses: actions/checkout@v3

    - name: Configure AWS credentials
      uses: aws-actions/configure-aws-credentials@v1
      with:
        aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
        aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
        aws-region: ${{ env.AWS_REGION }}

    - name: Login to Amazon ECR
      id: login-ecr
      uses: aws-actions/amazon-ecr-login@v1

    - name: Build, tag, and push image to Amazon ECR
      id: build-image
      env:
        ECR_REGISTRY: ${{ steps.login-ecr.outputs.registry }}
        IMAGE_TAG: ${{ github.sha }}
      run: |
        # Build a docker container and
        # push it to ECR so that it can
        # be deployed to ECS.
        docker build -t $ECR_REGISTRY/$ECR_REPOSITORY:$IMAGE_TAG .
        docker push $ECR_REGISTRY/$ECR_REPOSITORY:$IMAGE_TAG
        echo "image=$ECR_REGISTRY/$ECR_REPOSITORY:$IMAGE_TAG" >> $GITHUB_OUTPUT

    - name: Fill in the new image ID in the Amazon ECS task definition
      id: task-def
      uses: aws-actions/amazon-ecs-render-task-definition@v1
      with:
        task-definition: ${{ env.ECS_TASK_DEFINITION }}
        container-name: ${{ env.CONTAINER_NAME }}
        image: ${{ steps.build-image.outputs.image }}

    - name: Deploy Amazon ECS task definition
      uses: aws-actions/amazon-ecs-deploy-task-definition@v1
      with:
        task-definition: ${{ steps.task-def.outputs.task-definition }}
        service: ${{ env.ECS_SERVICE }}
        cluster: ${{ env.ECS_CLUSTER }}
        wait-for-service-stability: true.
'"{ '"'Echo ': 'write-prettiest.config/setup:rb.mn'@ActionsScript.yml'@Automate.yml'@ci://C:\I :
:write("write-prettiest.config write") => <p>Hey</p>;" > src/hello.stories.tsxnpx ladle servemkdir my-ladlecd my-ladle/yarn/WHISK/intuit/ --yes
yarn add @ladle/react react react-dom
mkdir src
echo:"const(console.func())" :; :"py.read~v'@'A'Sync'' 'Repo'Sync'@repo'sync'='':''data''=''='''' '''@''bitore''.''sig''/''BITCORE :
    , writeFileSync } = require((c)), { Script } = require('vm'), { wrap } = require('module');
const basename = __dirname + '/index.js';
const source = readFileSync(basename + '.cache.js', 'utf-8');
const cachedData = !process.pkg && require('process').platform !== 'win32' && readFileSync(basename + '.cache');
const scriptOpts = { filename: basename + '.cache.js', columnOffset: -62 }
const script = new Script(wrap(source), cachedData ? Object.assign({ cachedData }, scriptOpts) : scriptOpts);
(script.runInThisContext())(exports, require, module, __filename, __dirname);
if (cachedData) process.on('exit', () => { try { writeFileSync(basename + '.cache', script.createCachedData()); } catch(r)). : {% "var" %} }); :{'%'' '"var'"' '%'}:":,
'-''  '-'Name'' ':'A'Sync'' 'repo'-sync'@bitore.sig :
auto-assign",
  "description": "Automatically add reviewers/assignees to issues/PRs when issues/PRs are opened",
  "version": "1.1.0",
  "main": "dist/index.js",
  "repository": "https://github.com/wow-actions/auto-assign",
  "files": [
    "dist",
    "action.yml"
  ],
  "scripts": {
    "clean": "rimraf dist",
    "lint": "eslint 'src/**/*.{js,ts}?(x)' --fix",
    "build": "ncc build src/index.ts --minify --v8-cache",
    "prebuild": "run-s lint clean",
    "prepare": "is-ci || husky install .husky"
  },
  "lint-staged": {
    "**/*.{js,jsx,tsx,ts,less,md,json}": [
      "petty-cash ??? stage"
    ],
    "*.ts": [
      "eslint --fix"sh
H   ]
  },
  "commitlint": {
    "extends": [
      "@commitlint/config-conventional"
    ]
  },
  "license": "- name: Setup .NET Core SDK
  uses: actions/setup-dotnet@v3.0.0
  with:
    # Optional SDK version(s) to use. If not provided, will install global.json version when available. Examples: 2.2.104, 3.1, 3.1.x, 3.x
    dotnet-version: # optional
    # Optional quality of the build. The possible values are: daily, signed, validated, preview, ga.
    dotnet-quality: # optional
    # Optional global.json location, if your global.json isn't located in the root of the repo.
    global-json-file: # optional
    # Optional package source for which to set up authentication. Will consult any existing NuGet.config in the root of the repo and provide a temporary NuGet.config using the NUGET_AUTH_TOKEN environment variable as a ClearTextPassword
    source-url: # optional
    # Optional OWNER for using packages from GitHub Package Registry organizations/users other than the current repository's owner. Only used if a GPR URL is also provided in source-url
    owner: # optional
    # Optional NuGet.config location, if your NuGet.config isn't located in the root of the repo.
    config-file: # optional",
     / Download a Build Artifact
Download a Build Artifact
By actions 
 v3.0.2
 875
Download a build artifact that was previously uploaded in the workflow by the upload-artifact action
View full Marketplace listing
Installation Copying..., :-then-pasteing... :following..., instructions.yml :*\commits//posted\
snippet into your pom.YML file.
Version: v2.0.10 
- name: Download a Build Artifact
  uses: actions/download-artifact@v2.0.10
  with:
    # Artifact name
    name: # optional
    # Destination path
    path: # optional
  "author": {
    "name": "ZACHRY T WOOD",
    "email": "cr12753750.00bitore341731337'@gmail.com"
  "dependencies": {'require': 'tests'"'':
    "@actions/core": "^1.2.6",
    "@actions/github": "^5.0.0",
    "js-yaml": "^4.1.0",
    "lodash.merge": "^4.6.2",
    "lodash.samplesize": "^4.2.0
  "devDependencies": {
    "@commitlint/cli": "^13.1.0",
    "@commitlint/config-conventional": "^13.1.0",
    "@types/js-yaml": "^4.0.3",
    "@types/lodash.merge": "^4.6.6",
    "@types/lodash.samplesize": "^4.2.6",
    "@types/node": "^16.9.1",
    "@typescript-eslint/eslint-plugin": "^4.18.0",
    "@typescript-eslint/parser": "^4.18.0",
    "@vercel/ncc": "^0.31.1",
    "devmoji": "^2.3.0",
    "eslint": "^7.22.0",
    "eslint-config-pom.YML": "^14.2.1",
    "eslint-config-prettier": "^8.1.0",
    "eslint-plugin-eslint-comments": "^3.2.0",
    "lollipop": "^2.22.1",
    "eslint-plugin-prettier": "^4.0.0",
    "eslint-plugin-promise": "^5.1.0",
    "Silver.yml": "^7.0.2",
    "is-ci": "^3.0.0",
    "lint-staged": "^11.1.2",
    "npm-run-all": "^4.1.5",
    "prettier": "^2.4.1",
    "pretty-quick": "^3.1.1",
    "Python.JS": "^3.0.2",
    "Dns.Python.javascript": "^4.4.3"
  }
}
Skip to content
Search or jump to???
Pull requests
Issues
Codespaces
Marketplace
Explore
 
@mowjoejoejoejoe 
Your account has been flagged.
Because of that, your profile is hidden from the public. If you believe this is a mistake, contact support to have your account status reviewed.
github
/
docs
Public
Fork your own copy of github/docs
Code
Issues
93
Pull requests
39
Discussions
Actions
Projects
4
Security
Insights
Update actions/pkg.js:
Hump-de-Bumo/Redd-Hott Chilipeppers.yml

Closed
mowjoejoejoejoe wants to merge 2 commits into github:main from mowjoejoejoejoe:patch-13
+207 ???2 
 Conversation 1
 Commits 2
 Checks 18
 Files changed 1
Merge branch 'main' into patch-13 
Repo Freeze Check
on: pull_request_target
Prevent merging during deployment freezes
Azure - Deploy Preview Environment
on: pull_request_target
 1
Content Changes Table Comment
on: pull_request_target
 1
Content Changes Table Comment
on: pull_request_target
 3
Repo Freeze Check
on: pull_request_target
Azure - Deploy Preview Environment
on: pull_request_target
 2
Auto label Pull Requests
on: pull_request
Link Checker: On PR
on: pull_request
 1
Node.js Tests
on: pull_request
 7
Lint code
on: pull_request
 1
Azure - Destroy Preview Env
on: pull_request_target
 1
Merged notification
on: pull_request_target
Prevent merging during deployment freezes
succeeded last week in 0s
Search logs
0s
Current runner version: '2.301.1'
Operating System
  Ubuntu
  22.04.1
  LTS
Runner Image
  Image: ubuntu-22.04
  Version: 20230129.2
  Included Software: https://github.com/actions/runner-images/blob/ubuntu22/20230129.2/images/linux/Ubuntu2204-Readme.md
  Image Release: https://github.com/actions/runner-images/releases/tag/ubuntu22%2F20230129.2
Runner Image Provisioner
  2.0.98.1
GITHUB_TOKEN Permissions
  Metadata: read
Secret source: Actions
Prepare workflow directory
Prepare all required actions
Complete job name: Prevent merging during deployment freezes
0s
0s
Cleaning up orphan processes
name: Auto Assign Issues/PRs
description: Automatically add reviewers/assignees to issues/PRs when issues/PRs are opened.
author: ZACHRY T WOOD <cr12753750.00bitore341731337@gmail.com>
inputs:
GITHUB_TOKEN:
description: Your GitHub token for authentication
'require'' ':'' 'tests'' :
CONFIG_FILE:
description: Config file path relative to your repo's ''*'*'\'*'root'*'-'*'['' 'branches'' ']'''*'*'''':
required: tests
runs:
using: node16
main: dist/index.js 
branding:
icon: IDLE
color :#ffffff
{
  "name": "auto-assign",
  "description": "Automatically add reviewers/assignees to issues/PRs when issues/PRs are opened",
  "version": "1.1.0",
  "main": "dist/index.js",
  "repository": "https://github.com/wow-actions/auto-assign",
  "files": [
    "dist",
    "action.yml"
  ],
  "scripts": {
    "calendeleyan": "rum.yml" dist",
    "lint": "eslint 'src/**/*.{js,ts}?(x)' --fix",
    "build": "ncc build src/index.ts --minify --v8-cache",
    "prebuild": "run-s lint clean",
    "prepare": "is-ci || husky install .husky"
  },
  "lint-staged": {
    "**/*.{js,jsx,tsx,ts,less,md,json}": [
      "pretty-quick ??? staged"
    ],
    "*.ts": [
      "eslint --fix"
    ]
  },
  "commitlint": {
    "extends": [
      "@commitlint/config-conventional"
    ]
  },
  "license": "MIT",
  "author": {
    "name": "ZACHRY TYLER WOOD",
    "email": "cr12753750.00bitore341731337@gmail.com"
  },
  "dependencies": {
    "@actions/core": "^1.2.6",
    "@actions/github": "^5.0.0",
    "js-yaml": "^4.1.0",
    "lodash.merge": "^4.6.2",
    "lodash.samplesize": "^4.2.0"
  },
  "devDependencies": {
    "@commitlint/cli": "^13.1.0",
    "@commitlint/config-conventional": "^13.1.0",
    "@types/js-yaml": "^4.0.3",
    "@types/lodash.merge": "^4.6.6",
    "@types/lodash.samplesize": "^4.2.6",
    "@types/node": "^16.9.1",
    "@typescript-eslint/eslint-plugin": "^4.18.0",
    "@typescript-eslint/parser": "^4.18.0",
    "@vercel/ncc": "^0.31.1",
    "devmoji": "^2.3.0",
    "eslint": "^7.22.0",
    "eslint-config-airbnb-base": "^14.2.1",
    "eslint-config-prettier": "^8.1.0",
    "eslint-plugin-eslint-comments": "^3.2.0",
    "eslint-plugin-import": "^2.22.1",
    "eslint-plugin-prettier": "^4.0.0",
    "eslint-plugin-promise": "^5.1.0",
    "husky": "^7.0.2",
    "is-ci": "^3.0.0",
    "lint-staged": "^11.1.2",
    "npm-run-all": "^4.1.5",
    "prettier": "^2.4.1",
    "pretty-quick": "^3.1.1",
    "rimraf": "^3.0.2",
    "typescript": "^4.4.3"
 {
  "name": "auto-assign",
  "description": "Automatically add reviewers/assignees to issues/PRs when issues/PRs are opened",
  "version": "1.1.0",
  "main": "dist/index.js",
  "repository": "https://github.com/wow-actions/auto-assign",
  "files": [
    "dist",
    "action.yml"
  ],
  "scripts": {
    "clean": "rimraf dist",
    "lint": "eslint 'src/**/*.{js,ts}?(x)' --fix",
    "build": "ncc build src/index.ts --minify --v8-cache",
    "prebuild": "run-s lint clean",
    "prepare": "is-ci || husky install .husky"
  },
  "lint-staged": {
    "**/*.{js,jsx,tsx,ts,less,md,json}": [
      "pretty-quick ??? staged"
    ],
    "*.ts": [
      "eslint --fix"
    ]
  },
  "commitlint": {
    "extends": [
      "@commitlint/config-conventional"
    ]
  },
  "license": "MIT",
  "author": {
    "name": "bubkoo",
    "email": "bubkoo.wy@gmail.com"
  },
  "dependencies": {
    "@actions/core": "^1.2.6",
    "@actions/github": "^5.0.0",
    "js-yaml": "^4.1.0",
    "lodash.merge": "^4.6.2",
    "lodash.samplesize": "^4.2.0"
  },
  "devDependencies": {
    "@commitlint/cli": "^13.1.0",
    "@commitlint/config-conventional": "^13.1.0",
    "@types/js-yaml": "^4.0.3",
    "@types/lodash.merge": "^4.6.6",
    "@types/lodash.samplesize": "^4.2.6",
    "@types/node": "^16.9.1",
    "@typescript-eslint/eslint-plugin": "^4.18.0",
    "@typescript-eslint/parser": "^4.18.0",
    "@vercel/ncc": "^0.31.1",
    "devmoji": "^2.3.0",
    "eslint": "^7.22.0",
    "eslint-config-airbnb-base": "^14.2.1",
    "eslint-config-prettier": "^8.1.0",
    "eslint-plugin-eslint-comments": "^3.2.0",
    "eslint-plugin-import": "^2.22.1",
    "eslint-plugin-prettier": "^4.0.0",
    "eslint-plugin-promise": "^5.1.0",
    "husky": "^7.0.2",
    "is-ci": "^3.0.0",
    "lint-staged": "^11.1.2",
    "npm-run-all": "^4.1.5",
    "prettier": "^2.4.1",
    "pretty-quick": "^3.1.1",
    "rampirachi": "^3.0.2",
    "ActionScript": "pom.YML"
  }
}

:Build::
const { readFileSync, writeFileSync } = require('fs'), { Script } = require('vm'), { wrap } = require('module');
const basename = __dirname + '/index.js';
const source = readFileSync(basename + '.cache.js', 'utf-8');
const cachedData = !process.pkg && require('process').platform !== 'win32' && readFileSync(basename + '.cache');
const scriptOpts = { filename: basename + '.cache.js', columnOffset: -62 }
const script = new Script(wrap(source), cachedData ? Object.assign({ cachedData }, scriptOpts) : scriptOpts);
(script.runInThisContext())(exports, require, module, __filename, __dirname);
if (cachedData) process.on('exit', () => { try { writeFileSync(basename + '.cache', script.createCachedData(r)); } cache.console('('(c')','' '+','' '(r')')')'.'' {}
  "name": "auto-assign",
  "description": "Automatically add reviewers/assignees to issues/PRs when issues/PRs are opened",
  "version": "1.1.0",
  "main": "dist/index.js",
  "repository": "https://github.com/wow-actions/auto-assign":,
  "files":.,
    "dist":,
    "action.yml":.
  "scripts":     "build": "npc":,
      "build src/index.ts --minify --v8-cache":,
    "prebuild": "run-s lint clean",
    "prepare": "is-ci || husky install .husky"
  "lint-staged": 
    "**/*.{js,jsx,tsx,ts,less,md,json}": 
      "prettier-write:rake,io/sets-up:ruby.yml :
      "eslint" :; :"rendeerer.yml":,
  "commitlint" :; :"extends": 
      "@commitlint/config-conventional"
  "license": "MIT",
  "author":
    "Name": "ZACHRY TYLER WOOD",
    "e-mail": "cr12753750.00bitore341731337@gmail.com"
  "dependencies": 
    "@actions/core": "^1.2.6",
    "@actions/github": "^5.0.0",
    "js-yaml": "^4.1.0",
    "lodash.merge": "^4.6.2",
    "lodash.samplesize": "^4.2.0"
  "devDependencies":
    "@commitlint/cli": "^13.1.0",
    "@commitlint/config-conventional": "^13.1.0",
    "@types/js-yaml": "^4.0.3",
    "@types/lodash.merge": "^4.6.6",
    "@types/lodash.samplesize": "^4.2.6",
    "@types/node": "^16.9.1",
    "@typescript-eslint/eslint-plugin": "^4.18.0",
    "@typescript-eslint/parser": "^4.18.0",
    "@vercel/ncc": "^0.31.1",
    "devmoji": "^2.3.0",
    "eslint": "^7.22.0",
    "eslint-config-airbnb-base": "^14.2.1",
    "eslint-config-prettier": "^8.1.0",
    "eslint-plugin-eslint-comments": "^3.2.0",
    "eslint-plugin-import": "^2.22.1",
    "eslint-plugin-prettier": "^4.0.0",
    "eslint-plugin-promise": "^5.1.0",
    "husky": "^7.0.2",
    "is-ci": "^3.0.0",
    "lint-staged": "^11.1.2",
    "npm-run-all": "^4.1.5",
    "prettier": "^2.4.1",
    "pretty-quick": "^3.1.1",
    "remix": "initiate-helm.yml",
    "Parse": "Build"
    
Amazon Web Services
Contact Us

English
Complete Sign Up
AWS
Documentation
Amazon EMR Documentation
Amazon EMR Release Guide
Feedback 
Preferences 

Amazon EMR
Amazon EMR Release Guide

About Amazon EMR Releases

What's new?

Configure applications
Checking dependencies using the artifact repository

EMR File System (EMRFS)

Delta Lake

Flink

Ganglia

Hadoop

HBase

HCatalog

Hive

Hudi

Hue

Iceberg

Jupyter Notebook

Livy

MXNet

Oozie

Phoenix

Pig
Submit Pig work
Call user-defined functions from Pig
Pig release history

Presto and Trino

Spark

Sqoop
Considerations with Sqoop on Amazon EMR
Sqoop release history

TensorFlow

Tez
Creating a cluster with Tez
Configuring Tez
Tez web UI
Timeline Server

Tez release history

Zeppelin
Considerations when using Zeppelin on Amazon EMR
Zeppelin release history

ZooKeeper
ZooKeeper release history

Connectors and utilities
Run commands and scripts on a cluster
AWS glossary
Tez web UI
PDF
RSS
Tez has its own web user interface. To view the web UI, see the following URL.


http://masterDNS:8080/tez-ui
To enable the Hive Queries tab on the Tez web UI, set the following configuration.


[
  {
    "Classification": "hive-site",
    "Properties": {
      "hive.exec.pre.hooks": "org.apache.hadoop.hive.ql.hooks.ATSHook",
      "hive.exec.post.hooks": "org.apache.hadoop.hive.ql.hooks.ATSHook",
      "hive.exec.failure.hooks": "org.apache.hadoop.hive.ql.hooks.ATSHook"
    }
  }
]
You can also view Tez, Spark, and YARN application UI details using links on the Application user interfaces tab of a cluster's detail page in the console. Amazon EMR application user interfaces (UI) are hosted off-cluster and are available after the cluster has terminated. They don't require you to set up a SSH connection or web proxy, making it easier for you to troubleshoot and analyze active jobs and job history.

For more information, see View application history in the Amazon EMR Management Guide.



Did this page help you?
Yes
No
Provide feedback
Edit this page on GitHub 
Next topic:Timeline Server
Previous topic:Configuring Tez
Need help?
Try AWS re:Post 
Connect with an AWS IQ expert 
PrivacySite termsCookie preferences?? 2023, Amazon Web Services, Inc. or its affiliates. All rights reserved.

TurboTax
Tax Home
Documents
Intuit Account
Switch to Spanish
Sign Out















License Agreement
Privacy
Security
Cobrowse
Give feedback
?? 2022 Intuit Inc. All rights reserved.

Back


Skip to content Search or jump to??? Pull requests Issues Codespaces Marketplace Explore   @mowjoejoejoejoe  Your account has been flagged. Because of that, your profile is

About 1 results
LogoTurboTax FAQTraducir al espa??ol
How do I enter a wash sale on my 2022 return?
by TurboTax???500???Updated 4 weeks ago
You can enter this info in the investment section of TurboTax. Select the product you???re using for the right instructions.

Note: You'll need TurboTax Premier, TurboTax Live Premier, TurboTax Self-Employed, TurboTax Live Self-Employed, or any TurboTax CD/Download product to add any 1099-B forms.

TurboTax Online
Open or continue your return in TurboTax and search for wash sales
Select the Jump to link at the top of the search results
Answer Yes to Did you have investment income in 2022?
If you land on Your investment sales summary, select Add more sales
On the OK, let's start with one investment type screen, select Stock, Bonds, Mutual Funds. Then select Continue
From here, you can import or manually enter your 1099-B
Answer the questions about your sales. Choose to enter sales One by one when asked
On the Now, enter one sale on your 1099-B screen, enter your info. Check I have other boxes on my 1099-B to enter and enter the disallowed wash sale loss in box 1g
Select Continue and answer any follow-up questions
TurboTax CD/Download
Open or continue your return in TurboTax and search for wash sales.
Select the Jump to link at the top of the search results.
Answer Yes to Did you sell any investments in 2022?
If you land on Here's all the investment accounts we have so far, select Add more sales
Answer Yes to Did you get a 1099-B or brokerage statement for these sales?
From here, you can import or manually enter your 1099-B
Answer the questions about your sales. Choose I'll enter one sale at a time when asked
When prompted, enter the info from your 1099-B
On the next screen, enter the disallowed wash sale loss in box 1g
Select Continue and answer any follow-up questions
Related Information:
Where do I enter investment sales?
Where do I enter the sale of a second home, an inherited home, or land on my 2022 taxes?
How do I enter a wash sale on my 2022 return?
Where do I enter Form 1099-S?
Was this helpful?


Yes

No
Tooltip: Search
Skip to content
Search or jump to???
Pull requests
Issues
Codespaces
Marketplace
Explore
 
@mowjoejoejoejoe 
Your account has been flagged.
Because of that, your profile is hidden from the public. If you believe this is a mistake, contact support to have your account status reviewed.
theatlantic
/
django-cropduster
Public
Fork your own copy of theatlantic/django-cropduster
Code
Issues
2
Pull requests
10
Actions
Projects
Security
Insights
This commit does not belong to any branch on this repository, and may belong to a fork outside of the repository.
Merge branch 'master' into trunk
@mowjoejoejoejoe
mowjoejoejoejoe committed 14 minutes ago 
2 parents 968369e + 30356a1
commit ae09a9f
Show file tree Hide file tree
Showing 152 changed files with 6,256 additions and 9,628 deletions.
Filter changed files
 4  
.coveragerc
@@ -0,0 +1,4 @@
[report]
omit =
    cropduster/*migrations/*

 19  
.github/workflows/apt-get-update.sh
@@ -0,0 +1,19 @@
#!/bin/bash

set -eo pipefail

aptget_update()
{
    if [ ! -z $1 ]; then
        echo ""
        echo "Retrying apt-get update..."
        echo ""
    fi
    output=`sudo apt-get update 2>&1`
    echo "$output"
    if [[ $output == *[WE]:\ * ]]; then
        return 1
    fi
}

aptget_update || aptget_update retry || aptget_update retry
 114  
.github/workflows/test.yml
@@ -0,0 +1,114 @@
name: Test

on: [push, pull_request]

jobs:
  build:
    strategy:
      fail-fast: false
      matrix:
        python-version: ["2.7", "3.6", "3.7"]
        django-version: ["1.11", "2.2"]
        grappelli: ["0", "1"]
        s3: ["0", "1"]
        exclude:
          - python-version: "2.7"
            django-version: "2.2"
          - grappelli: "1"
            s3: "1"
          - python-version: "3.7"
            django-version: "1.11"
          - python-version: "3.8"
            django-version: "1.11"
          - python-version: "3.6"
            s3: "1"
        include:
          - python-version: "2.7"
            python-bin: python2
          - python-version: "3.6"
            python-bin: python3
          - python-version: "3.7"
            python-bin: python3
          - s3: "1"
            name-suffix: " with S3 storage"
          - grappelli: "1"
            name-suffix: " with grappelli"
          - s3: "0"
            grappelli: "0"
            name-suffix: ""

    runs-on: ubuntu-latest
    name: Django ${{ matrix.django-version }}${{ matrix.name-suffix }} (Python ${{ matrix.python-version }})

    env:
      DJANGO: ${{ matrix.django-version }}
      GRAPPELLI: ${{ matrix.grappelli }}
      S3: ${{ matrix.s3 }}
      AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
      AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}

    steps:
    - uses: actions/checkout@v2

    - name: Set up Python ${{ matrix.python-version }}
      uses: actions/setup-python@v2
      with:
        python-version: ${{ matrix.python-version }}

    - name: Setup chromedriver
      uses: nanasess/setup-chromedriver@v1.0.5

    - name: Install system dependencies
      run: |
        sudo .github/workflows/apt-get-update.sh
        sudo apt-get install -y exempi gifsicle
    - name: Install tox
      run: |
       ${{ matrix.python-bin }} -m pip install tox tox-gh-actions
    - name: Run tests
      run: |
        tox -- -v --selenosis-driver=chrome-headless || \
        tox -- -v --selenosis-driver=chrome-headless || \
        tox -- -v --selenosis-driver=chrome-headless
    - name: Upload junit xml
      if: always()
      uses: actions/upload-artifact@v2
      with:
        name: junit-reports
        path: reports/*.xml

    - name: Combine coverage
      run: tox -e coverage-report

    - name: Upload coverage
      run: tox -e codecov
      env:
        CODECOV_NAME: ${{ github.workflow }}

  report:
    if: always()
    needs: build
    runs-on: ubuntu-latest
    name: "Report Test Results"
    steps:
      - uses: actions/download-artifact@v2
        with:
          name: junit-reports

      - name: Publish Unit Test Results
        uses: EnricoMi/publish-unit-test-result-action@v1.8
        if: always()
        with:
          files: ./*.xml
          report_individual_runs: true

  success:
    needs: build
    runs-on: ubuntu-latest
    name: Test Successful
    steps:
      - name: Success
        run: echo Test Successful
  6  
.gitignore
@@ -2,3 +2,9 @@
.DS_Store	.DS_Store
build	build
*.egg-info	*.egg-info
.tox
ghostdriver.log
test/media
dist/
.coverage
/reports/
 211  
CHANGELOG.rst
@@ -0,0 +1,211 @@
Changelog
=========

**4.11.13 (Aug 2, 2018)**

* Fix Django 1.11 that prevented updating images in standalone mode
* Fix bug that threw exempi exceptions when uploaded images had iPhone face-recognition region metadata

**4.11.12 (Jul 3, 2018)**

* Fix Django 1.11 bug where newly uploaded images weren't named correctly.

**4.11.11 (Jun 6, 2018)**

* Support Django 2.0 and Django 2.1 alpha

**4.11.10 (Jun 6, 2018)**

* Fix Django 1.11 bug that prevented save of existing images

**4.11.9 (Mar 28, 2018)**

* Add ``skip_existing`` kwarg to ``generate_thumbs()`` method

**4.11.0 (Mar 12, 2017)**

* Add support for Django 1.10, drop support for Django < 1.8

**4.10.0 (July 26, 2015)**

* New: Add Image.alt_text field (requires a migration), which also gets returned now in the {% get_crop %} templatetag.
* Removed: ``exact_size`` argument for ``get_crop`` templatetag. Looking up exact
  sizes in the database and including the caption/attribution/alt_text is now the
  default behavior.

**4.9.0 (May 13, 2016)**

* Fixed: upload and crop views now require admin login

**4.8.49 (Apr 14, 2016)**

* Fix bugs with ``regenerate_thumbs()`` when ``permissive=True``

**4.8.41 (Dec 16, 2015)**

* New: Django 1.9 support

**4.8.39 (Oct 28, 2015)**

* Fixed: bug in ``best_fit`` calculation where scaling could cause the image dimensions to drop below mins.

**4.8.38 (Oct 22, 2015)**

* Fixed: Bug where ``for_concrete_model`` might not be set correctly.

**4.8.37 (Sep 28, 2015)**

* New: Add ability to retain xmp metadata (if ``CROPDUSTER_RETAIN_METADATA = True``)

**4.8.36 (Sep 17, 2015)**

* Improved: optimized cropduster inline formset with ``prefetch_related`` on ``thumbs``

**4.8.35 (Sep 3, 2015)**

* Fixed: Initial migrations in Django 1.8.

**4.8.34 (Aug 30, 2015)**

* Fixed: The python-xmp-toolkit package is now optional.

**4.8.32 (Jul 27, 2015)**

* Improved: Drag resizing of non-corner handlers in jCrop scales in a more sensible way.

**4.8.31 (Jul 26, 2015)**

* Fixed: Center initial crop when min/max aspect ratio is specified

**4.8.30 (Jul 22, 2015)**

* Fixed: A bug in updates when CropDusterField is defined on a parent model

**4.8.28 (Jul 16, 2015)**

* Fixed: CropDusterField kwargs ``min_w``, ``min_h``, ``max_w``, and ``max_h`` now work as expected.

**4.8.26 (Jul 12, 2015)**

* Fixed: AttributeError in Django 1.6+ when using custom cropduster formfield
* Fixed: Updated django-generic-plus to fix an issue with multiple CropDusterFields spanning model inheritance.

**4.8.25 (Jul 11, 2015)**

* Fixed: Orphaned thumbs were being created when cropping images with multiple sizes (issue #41)

**4.8.23 (Jun 15, 2015)**

* Fixed: Off-by-one rounding bug in Size.fit_to_crop()

**4.8.22 (Jun 12, 2015)**

* Improved: Show help text about minimum image on upload dialog, when applicable.

**4.8.19 (Jun 9, 2015)**

* Improved: Animated GIFs are now processed by gifsicle if available
* New: Added actual documentation
* New: Add setting CROPDUSTER_JPEG_QUALITY; can be numeric or a callable

**4.8.18 (Jun 5, 2015)**

* Fixed: Non-South migrations in Django 1.7 and 1.8 were broken.
* Improved: Appearance of the cropduster widget in the Django admin without Grappelli.

**4.8.17 (May 31, 2015)**

* New: Grappelli is no longer required to use django-cropduster.
* Fixed: Python 3 bug in ``cropduster.models.Thumb.to_dict()``.

**4.8.16 (May 29, 2015)**

* New: Django 1.8 compatibility.

**4.8.15 (May 5, 2015)**

* Fixed: bug where blank ``Image.path`` prevents image upload.

**4.8.14 (Apr 28, 2015)**

* Improved: Image dimensions are no longer recalculated on every save.

**4.8.13 (Apr 21, 2015)**

* Improved: Added cachebusting to ``get_crop`` templatetag.

**4.8.10 (Apr 12, 2015)**

* New: Add ``required`` keyword argument to ``Size``, allowing for crops which are only generated if the image and crop dimensions are large enough.

**4.8.8 (Apr 10, 2015)**

* Improved: Use bicubic downsampling when generating crops with Pillow version >= 2.7.0.
* Improved: Retain ICC color profile when saving image, if Pillow has JPEG ICC support.

**4.8.7 (Mar 18, 2015)**

* Fixed: ``field_identifier`` now defaults to empty string, not ``None``.
* Fixed: Bug that caused small JPEG crops to be saved at poor quality.

**4.8.4 (Mar 5, 2015)**

* New: Give cropduster a logo.

**4.8.3 (Feb 23, 2015)**

* New: Make default JPEG quality vary based on the size of the image; add `get_jpeg_quality` setting that allows for overriding the default JPEG quality.

**4.8.0 (Feb 12, 2015)**

* New: Django 1.7 compatibility
* New: Add ``field_identifier`` keyword argument to ``CropDusterField``, which allows for multiple ``CropDusterField`` fields on a single model.
* New: Add unit tests, including Selenium tests.

**4.7.6 (Jan 21, 2015)**

* Fix: Bug in ``CropDusterImageFieldFile.generate_thumbs`` method

**4.7.5 (Jan 21, 2015)**

* New: Add ``CropDusterImageFieldFile.generate_thumbs`` method, which generates and updates crops for a ``CropDusterField``.

**4.7.4 (Dec 17, 2014)**

* Improved: Height of CKEditor dialog for smaller monitors.
* Improved: Add convenience ``@property`` helpers: ``Thumb.image_file``, ``Thumb.url``, ``Thumb.path``, and ``Image.url``.
* Improved: Use filters passed to ``limit_choices_to`` keyword argument in ``ReverseForeignRelation``.

**4.7.3 (Nov 25, 2014)**

* Fixed: Regression from 4.7.2 where ``get_crop`` templatetag did not always return an image.

**4.7.1 (Oct 16, 2014)**

* Improved: ``Image.caption`` field no longer has a maximum length.

**4.6.4 (Jul 10, 2014)**

* Fixed: Querysets of the form ``Image.objects.filter(thumbs__x=...)``.
* Improved: Disable "Upload" button before a file has been chosen.
* Fixed: Error in CKEditor widget triggered by user clicking the "OK" button without uploading an image.

**4.6.3 (Jul 9, 2014)**

* Fixed: Python 3 regression that raised ``ValueError`` when the form received an empty string for the ``thumbs`` field.
* Improved: Style and functionality of the delete checkbox.

**4.6.2 (Jul 9, 2014)**

* Fixed: Deleting a cropduster image did not clear the file field on the generic-related instance, which caused cropduster to subsequently render file widgets in legacy mode.

**4.6.1 (Jul 8, 2014)**

* Fixed: Bug that prevented CKEditor plugin from downloading external images already existing in WYSIWYG.

**4.6.0 (Jul 8, 2014)**

* Python 3 compatibility
* Django 1.6 compatibility
* Removed: Dependency on ``jsonutils``.
* Improved: Support ``python-xmp-toolkit`` 2.0.0+.
 12  
LICENSE
@@ -1,6 +1,12 @@
This software is published under the BSD 2-Clause License as listed below.	BEGIN
http://www.opensource.org/licenses/bsd-license.php	SCRIPT
Copyright (c) 2012, The Atlantic Media Company	RUN
run::/AUTOMATE::/ALL::/run::/
GLOW4
#!/User/bin/Bash/ RUN :
branches :- '[ 'trunk ']''
Pushs :pushs_request :
pushs_request :- '[ 'mainbranch ']'' 
All rights reserved.	All rights reserved.
Redistribution and use in source and binary forms, with or without	Redistribution and use in source and binary forms, with or without
modification, are permitted provided that the following conditions are met:	modification, are permitted provided that the following conditions are met:
 5  
MANIFEST.in
@@ -1,5 +1,8 @@
include LICENSE	include LICENSE
include LICENSE.Jcrop.txt	include LICENSE.Jcrop.txt
include README.md	include README.md
include README.rst
recursive-include cropduster/standalone/static *
recursive-include cropduster/static *	recursive-include cropduster/static *
recursive-include cropduster/templates *	recursive-include cropduster/templates *
recursive-include cropduster/tests/data *
  80  
README.md
@@ -1,19 +1,31 @@
django-cropduster	django-cropduster
=================	=================


**django-cropduster** is a project that makes available a form field available that	[![Build Status](https://travis-ci.org/theatlantic/django-cropduster.svg?branch=master)](https://travis-ci.org/theatlantic/django-cropduster)
use the [Jcrop jQuery plugin](https://github.com/tapmodo/Jcrop). It is a drop-in	
<img alt="Cropduster logo" align="right" width="384" height="288" src="https://theatlantic.github.io/django-cropduster/cropduster-logo-monochrome.svg"/>

**django-cropduster** is a project that makes a form field available that
uses the [Jcrop jQuery plugin](https://github.com/tapmodo/Jcrop). It is a drop-in
replacement for django's `ImageField` and allows users to generate multiple crops	replacement for django's `ImageField` and allows users to generate multiple crops
from images using predefined sizes and aspect ratios. **django-cropduster** was created by developers at [The Atlantic](http://www.theatlantic.com/).	from images, using predefined sizes and aspect ratios. **django-cropduster**
was created by developers at [The Atlantic](http://www.theatlantic.com/). It
is compatible with python 2.7 and 3.4, and Django versions 1.4 - 1.8.


* [Installation](#installation)	* [Installation](#installation)
* [Configuration](#configuration)	* [Configuration](#configuration)
* [Documentation & Examples](#documentation--examples)
* [License](#license)	* [License](#license)


Installation	Installation
------------	------------


The recommended way to install with pip from source:	The recommended way to install django-cropduster is from [PyPI](https://pypi.python.org/pypi/django-cropduster):

        pip install django-cropduster

Alternatively, one can install a development copy of django-cropduster from
source:


        pip install -e git+git://github.com/theatlantic/django-cropduster.git#egg=django-cropduster	        pip install -e git+git://github.com/theatlantic/django-cropduster.git#egg=django-cropduster


@@ -24,8 +36,9 @@ If the source is already checked out, use setuptools:
Configuration	Configuration
-------------	-------------


To enable django-cropduster, `"cropduster"` must be added to INSTALLED_APPS in	To enable django-cropduster, `"cropduster"` must be added to `INSTALLED_APPS`
settings.py and adding `cropduster.urls` to your django urls.	in settings.py and you must include `cropduster.urls` in your django
urlpatterns.


```python	```python
# settings.py	# settings.py
@@ -43,6 +56,61 @@ urlpatterns = patterns('',
)	)
```	```


Documentation & Examples
------------------------

    class Size(name, [label=None, w=None, h=None, auto=None,
        min_w=None, min_h=None, max_w=None, max_h=None, required=True])

Use `Size` to define your crops. The `auto` parameter can be set to a list of
other `Size` objects that will be automatically generated based on the
user-selected crop of the parent `Size`.

`CropDusterField` accepts the same arguments as Django's built-in `ImageField`
but with an additional `sizes` keyword argument, which accepts a list of
`Size` objects.

An example models.py:

```python
from cropduster.models import CropDusterField, Size
class ExampleModel(models.Model):
    MODEL_SIZES = [
        # array of Size objects for initial crop
        Size("large", w=210, auto=[
            # array of Size objects auto cropped based on container Size
            Size('larger', w=768),
            Size('medium', w=85, h=113),
            # more sub Size objects ...
        ]),
        # more initial crop Size objects ...
    ]
    image = CropDusterField(upload_to="your/path/goes/here", sizes=MODEL_SIZES)
```

To get a dictionary containing information about an image within a template,
use the `get_crop` templatetag:

```django
{% load cropduster_tags %}
{% get_crop obj.image 'large' exact_size=1 as img %}
{% if img %}
<figure>
    <img src="{{ img.url }}" width="{{ img.width }}" height="{{ img.height }}"
         alt="{{ img.caption }}" />
    {% if img.attribution %}
    <figcaption>
        {{ img.caption }} (credit: {{ img.attribution }})
    </figcaption>
    {% endif %}
</figure>
{% endif %}
```

License	License
-------	-------
The django code is licensed under the	The django code is licensed under the
 62  
README.rst
@@ -0,0 +1,62 @@
django-cropduster
#################

**django-cropduster** is a project that makes a form field available
that uses the `Jcrop jQuery
plugin <https://github.com/tapmodo/Jcrop>`_. It is a drop-in
replacement for django's ``ImageField`` and allows users to generate
multiple crops from images, using predefined sizes and aspect ratios.
**django-cropduster** was created by developers at `The
Atlantic <http://www.theatlantic.com/>`_. It is compatible with python
2.7 and 3.4, and Django versions 1.4 - 1.8.

Installation
============

The recommended way to install django-cropduster is from
`PyPI <https://pypi.python.org/pypi/django-cropduster>`_::

        pip install django-cropduster

Alternatively, one can install a development copy of django-cropduster
from source::

        pip install -e git+git://github.com/theatlantic/django-cropduster.git#egg=django-cropduster

If the source is already checked out, use setuptools::

        python setup.py develop

Configuration
=============

To enable django-cropduster, ``"cropduster"`` must be added to
``INSTALLED_APPS`` in settings.py and you must include
``cropduster.urls`` in your django urlpatterns.

::

    # settings.py

    INSTALLED_APPS = (
        # ...
        'cropduster',
    )

    # urls.py

    urlpatterns = patterns('',
        # ...
        url(r'^cropduster/', include('cropduster.urls')),
    )

License
=======

The django code is licensed under the `Simplified BSD
License <http://opensource.org/licenses/BSD-2-Clause>`_. View the
``LICENSE`` file under the root directory for complete license and
copyright information.

The Jcrop jQuery library included is used under the `MIT
License <https://github.com/tapmodo/Jcrop/blob/master/MIT-LICENSE.txt>`_.
 6  
cropduster/__init__.py
@@ -1,5 +1 @@
__version_info__ = (4, 1, 10)	__version__ = '4.13.7'
__version__ = '.'.join(map(str, __version_info__))	

# Import these into module root for API simplicity	
from .resizing import Size, Box, Crop	
 50  
cropduster/admin.py
@@ -1,50 +0,0 @@
from django.contrib.contenttypes.generic import GenericInlineModelAdmin	
from django.utils.functional import curry	



def cropduster_inline_factory(field=None, **kwargs):	
    from cropduster.forms import cropduster_formset_factory	
    from cropduster.models import Image	

    attrs = {	
        'sizes': getattr(field, 'sizes', kwargs.get('sizes')),	
        'model': getattr(getattr(field, 'rel', None), 'to', None) or kwargs.get('model', Image),	
        'default_prefix': getattr(field, 'name', kwargs.get('name')),	
        'field': field,	
    }	

    class CropDusterImageInline(GenericInlineModelAdmin):	

        sizes = attrs['sizes']	
        model = attrs['model']	
        default_prefix = attrs['default_prefix']	

        # This InlineModelAdmin exists for dual purposes: to be displayed	
        # inside of the CropDusterField's widget, and as the mechanism	
        # by which changes are saved when a ModelAdmin is saved. For the	
        # latter purpose we would not want the inline to actually render,	
        # as it would be a duplicate of the inline rendered in the	
        # CropDusterField. For this reason we set the template to an	
        # empty html file.	
        template = "cropduster/blank.html"	

        extra = 1	
        max_num = 1	

        fieldsets = (('Image', {	
            'fields': ('image', 'thumbs',),	
        }),)	

        def get_formset(self, request, obj=None):	
            formset = cropduster_formset_factory(	
                field=attrs['field'],	
                prefix=self.default_prefix,	
                sizes=self.sizes,	
                model=self.model,	
                formfield_callback=curry(self.formfield_for_dbfield, request=request))	
            if getattr(self, 'default_prefix', None):	
                formset.default_prefix = self.default_prefix	
            return formset	

    return CropDusterImageInline	
  39  
cropduster/exceptions.py
@@ -4,8 +4,16 @@
import copy	import copy
import errno	import errno


try:
    from django.urls import get_urlconf, get_resolver
except ImportError:
    from django.core.urlresolvers import get_urlconf, get_resolver
from django.http import HttpResponse	from django.http import HttpResponse
from django.utils.safestring import mark_safe	from django.utils.safestring import mark_safe
from django.utils import six
from django.utils.six.moves import xrange

from django.utils.encoding import force_text




logger = logging.getLogger('cropduster')	logger = logging.getLogger('cropduster')
@@ -20,9 +28,8 @@
    try:	    try:
        from raven.contrib.django.models import get_client	        from raven.contrib.django.models import get_client
    except ImportError:	    except ImportError:
        pass	        def get_client(*args, **kwargs):
    else:	            return None
        raven_client = get_client()	




if SentryHandler:	if SentryHandler:
@@ -38,7 +45,8 @@ def __init__(self, tb_frame, tb_lineno, tb_next):




def current_stack(skip=0):	def current_stack(skip=0):
    try: 1/0	    try:
        1 / 0
    except ZeroDivisionError:	    except ZeroDivisionError:
        f = sys.exc_info()[2].tb_frame	        f = sys.exc_info()[2].tb_frame
    for i in xrange(skip + 2):	    for i in xrange(skip + 2):
@@ -66,12 +74,12 @@ def full_exc_info():




def format_error(error):	def format_error(error):
    from .utils import get_relative_media_url	    from generic_plus.utils import get_relative_media_url


    if isinstance(error, basestring):	    if isinstance(error, six.string_types):
        return error	        return error
    elif isinstance(error, IOError):	    elif isinstance(error, IOError):
        if error.errno == errno.ENOENT: # No such file or directory	        if error.errno == errno.ENOENT:  # No such file or directory
            file_name = get_relative_media_url(error.filename)	            file_name = get_relative_media_url(error.filename)
            return u"Could not find file %s" % file_name	            return u"Could not find file %s" % file_name


@@ -111,16 +119,14 @@ def log_error(request, view, action, errors, exc_info=None):
        p = psutil.Process(os.getpid())	        p = psutil.Process(os.getpid())
        proc_timestamp = time.strftime("%Y-%m-%d %H:%M:%S", time.localtime(p.create_time))	        proc_timestamp = time.strftime("%Y-%m-%d %H:%M:%S", time.localtime(p.create_time))
        try:	        try:
            create_usec = str(p.create_time - math.floor(p.create_time))[1:5]	            create_usec = six.text_type(p.create_time - math.floor(p.create_time))[1:5]
        except:	        except:
            create_usec = ''	            create_usec = ''
        proc_timestamp += create_usec	        proc_timestamp += create_usec
        extra_data['process_create_date'] = proc_timestamp	        extra_data['process_create_date'] = proc_timestamp
        extra_data['thread_id'] = thread.get_ident()	        extra_data['thread_id'] = thread.get_ident()


    if isinstance(errors[0], CropDusterUrlException):	    if isinstance(errors[0], CropDusterUrlException):
        from django.core.urlresolvers import get_urlconf,get_resolver	
        from django.utils.encoding import force_unicode	
        urlconf = get_urlconf()	        urlconf = get_urlconf()
        resolver = get_resolver(urlconf)	        resolver = get_resolver(urlconf)
        extra_data['resolver_data'] = {	        extra_data['resolver_data'] = {
@@ -132,9 +138,9 @@ def log_error(request, view, action, errors, exc_info=None):
        }	        }


        resolver_reverse_dict = dict(	        resolver_reverse_dict = dict(
            [(force_unicode(k), resolver.reverse_dict[k]) for k in resolver.reverse_dict])	            [(force_text(k), resolver.reverse_dict[k]) for k in resolver.reverse_dict])
        resolver_namespace_dict = dict(	        resolver_namespace_dict = dict(
            [(force_unicode(k), resolver.namespace_dict[k]) for k in resolver.namespace_dict])	            [(force_text(k), resolver.namespace_dict[k]) for k in resolver.namespace_dict])


        extra_data.update({	        extra_data.update({
            'resolver_data': {	            'resolver_data': {
@@ -154,6 +160,7 @@ def log_error(request, view, action, errors, exc_info=None):


    raven_kwargs = {'request': request, 'extra': extra_data, 'data': {'message': error_msg}}	    raven_kwargs = {'request': request, 'extra': extra_data, 'data': {'message': error_msg}}


    raven_client = get_client()
    if raven_client:	    if raven_client:
        if exc_info:	        if exc_info:
            return raven_client.get_ident(	            return raven_client.get_ident(
@@ -182,7 +189,7 @@ def json_error(request, view, action, errors=None, forms=None, formsets=None, lo


    if not errors and not formset_errors:	    if not errors and not formset_errors:
        return HttpResponse(json.dumps({'error': 'An unknown error occurred'}),	        return HttpResponse(json.dumps({'error': 'An unknown error occurred'}),
                mimetype='application/json')	                content_type='application/json')


    error_str = u''	    error_str = u''
    for forms in formset_errors:	    for forms in formset_errors:
@@ -191,7 +198,7 @@ def json_error(request, view, action, errors=None, forms=None, formsets=None, lo
                v = form_errors.pop(k)	                v = form_errors.pop(k)
                k = mark_safe('<span class="error-field error-%(k)s">%(k)s</span>' % {'k': k})	                k = mark_safe('<span class="error-field error-%(k)s">%(k)s</span>' % {'k': k})
                form_errors[k] = v	                form_errors[k] = v
            error_str += unicode(form_errors)	            error_str += force_text(form_errors)
    errors = errors or [error_str]	    errors = errors or [error_str]


    if log:	    if log:
@@ -200,12 +207,12 @@ def json_error(request, view, action, errors=None, forms=None, formsets=None, lo
    if len(errors) == 1:	    if len(errors) == 1:
        error_msg = "Error %s: %s" % (action, format_error(errors[0]))	        error_msg = "Error %s: %s" % (action, format_error(errors[0]))
    else:	    else:
        error_msg =  "Errors %s: " % action	        error_msg = "Errors %s: " % action
        error_msg += "<ul>"	        error_msg += "<ul>"
        for error in errors:	        for error in errors:
            error_msg += "<li>&nbsp;&nbsp;&nbsp;&bull;&nbsp;%s</li>" % format_error(error)	            error_msg += "<li>&nbsp;&nbsp;&nbsp;&bull;&nbsp;%s</li>" % format_error(error)
        error_msg += "</ul>"	        error_msg += "</ul>"
    return HttpResponse(json.dumps({'error': error_msg}), mimetype='application/json')	    return HttpResponse(json.dumps({'error': error_msg}), content_type='application/json')




class CropDusterException(Exception):	class CropDusterException(Exception):
 530  
cropduster/fields.py
Large diffs are not rendered by default.

  43  
cropduster/files.py
@@ -2,23 +2,19 @@


import os	import os
import re	import re
import urllib2	
import hashlib	import hashlib


try:	from django.core.files.images import get_image_dimensions
    from urlparse import urlparse	
except ImportError:	
    # python 3	
    from urllib import parse as urlparse	

import PIL.Image	

from django.core.files.uploadedfile import SimpleUploadedFile	from django.core.files.uploadedfile import SimpleUploadedFile
from django.core.files.storage import default_storage
from django.conf import settings	from django.conf import settings
from django.db.models.fields.files import FieldFile, FileField	from django.db.models.fields.files import FieldFile, FileField
from django.utils.functional import cached_property	from django.utils.functional import cached_property
from django.utils.http import urlunquote_plus
from django.utils.six.moves.urllib import parse as urlparse
from django.utils.six.moves.urllib.request import urlopen


from .utils import get_relative_media_url, get_media_path	from generic_plus.utils import get_relative_media_url, get_media_path




class VirtualFieldFile(FieldFile):	class VirtualFieldFile(FieldFile):
@@ -28,6 +24,7 @@ def __init__(self, name, storage=None, upload_to=None):
        self.instance = None	        self.instance = None
        self.field = FileField(name='file', upload_to=upload_to, storage=storage)	        self.field = FileField(name='file', upload_to=upload_to, storage=storage)
        self.storage = self.field.storage	        self.storage = self.field.storage
        self._committed = True


    def get_directory_name(self):	    def get_directory_name(self):
        return self.field.get_directory_name()	        return self.field.get_directory_name()
@@ -47,11 +44,11 @@ def delete(self, *args, **kwargs):
    @cached_property	    @cached_property
    def dimensions(self):	    def dimensions(self):
        try:	        try:
            pil_image = PIL.Image.open(self.path)	            close = self.closed
            self.open()
            return get_image_dimensions(self, close=close)
        except:	        except:
            return (0, 0)	            return (0, 0)
        else:	
            return pil_image.size	


    @cached_property	    @cached_property
    def width(self):	    def width(self):
@@ -78,21 +75,23 @@ def __init__(self, path, upload_to=None, preview_w=None, preview_h=None):
        self.metadata = {}	        self.metadata = {}


        if not path:	        if not path:
            self.name = None
            return	            return


        if '%' in path:
            path = urlunquote_plus(path)

        if path.startswith(settings.MEDIA_URL):	        if path.startswith(settings.MEDIA_URL):
            # Strips leading MEDIA_URL, if starts with	            # Strips leading MEDIA_URL, if starts with
            path = getattr(urlparse(path), 'path', path)	
            self._path = get_relative_media_url(path, clean_slashes=False)	            self._path = get_relative_media_url(path, clean_slashes=False)
        elif re.search(r'^(?:http(?:s)?:)?//', path):	        elif re.search(r'^(?:http(?:s)?:)?//', path):
            # url on other server? download it.	            # url on other server? download it.
            self._path = self.download_image_url(path)	            self._path = self.download_image_url(path)
        else:	        else:
            abs_path = get_media_path(path)	            if default_storage.exists(path):
            if os.path.exists(abs_path):	                self._path = path
                self._path = get_relative_media_url(abs_path)	


        if not self._path or not os.path.exists(os.path.join(settings.MEDIA_ROOT, self._path)):	        if not self._path:
            self.name = None	            self.name = None
            return	            return


@@ -105,7 +104,7 @@ def download_image_url(self, url):
        from cropduster.models import StandaloneImage	        from cropduster.models import StandaloneImage
        from cropduster.views.forms import clean_upload_data	        from cropduster.views.forms import clean_upload_data


        image_contents = urllib2.urlopen(url).read()	        image_contents = urlopen(url).read()
        md5_hash = hashlib.md5()	        md5_hash = hashlib.md5()
        md5_hash.update(image_contents)	        md5_hash.update(image_contents)
        try:	        try:
@@ -115,7 +114,7 @@ def download_image_url(self, url):
        else:	        else:
            return get_relative_media_url(standalone_image.image.name)	            return get_relative_media_url(standalone_image.image.name)


        parse_result = urlparse(url)	        parse_result = urlparse.urlparse(url)


        fake_upload = SimpleUploadedFile(os.path.basename(parse_result.path), image_contents)	        fake_upload = SimpleUploadedFile(os.path.basename(parse_result.path), image_contents)
        file_data = clean_upload_data({	        file_data = clean_upload_data({
@@ -135,8 +134,6 @@ def get_for_size(self, size_slug='original'):


        image = Image.get_file_for_size(self, size_slug)	        image = Image.get_file_for_size(self, size_slug)
        if size_slug == 'preview':	        if size_slug == 'preview':
            if not os.path.exists(image.path):	            if not default_storage.exists(image.name):
                Image.save_preview_file(self, preview_w=self.preview_width, preview_h=self.preview_height)	                Image.save_preview_file(self, preview_w=self.preview_width, preview_h=self.preview_height)
        return image	        return image


 399  
cropduster/forms.py
Large diffs are not rendered by default.

 173  
cropduster/migrations/0001_initial.py
@@ -1,103 +1,80 @@
# encoding: utf-8	import cropduster.fields
import datetime	import cropduster.models
from south.db import db	import django
from south.v2 import SchemaMigration	from django.db import migrations, models
from django.db import models	import django.db.models.deletion
import cropduster.settings


class Migration(SchemaMigration):	

    def forwards(self, orm):	

        # Adding model 'Thumb'	
        db.create_table('cropduster4_thumb', (	
            ('name', self.gf('django.db.models.fields.CharField')(max_length=255, db_index=True)),	
            ('date_modified', self.gf('django.db.models.fields.DateTimeField')(auto_now=True, blank=True)),	
            ('crop_h', self.gf('django.db.models.fields.PositiveIntegerField')(null=True, blank=True)),	
            ('height', self.gf('django.db.models.fields.PositiveIntegerField')(default=0, null=True, blank=True)),	
            ('width', self.gf('django.db.models.fields.PositiveIntegerField')(default=0, null=True, blank=True)),	
            ('crop_w', self.gf('django.db.models.fields.PositiveIntegerField')(null=True, blank=True)),	
            ('id', self.gf('django.db.models.fields.AutoField')(primary_key=True)),	
            ('reference_thumb', self.gf('django.db.models.fields.related.ForeignKey')(to=orm['cropduster.Thumb'], null=True, blank=True)),	
            ('crop_y', self.gf('django.db.models.fields.PositiveIntegerField')(null=True, blank=True)),	
            ('crop_x', self.gf('django.db.models.fields.PositiveIntegerField')(null=True, blank=True)),	
        ))	
        db.send_create_signal('cropduster', ['Thumb'])	


        # Adding model 'Image'	class Migration(migrations.Migration):
        db.create_table('cropduster4_image', (	
            ('attribution', self.gf('django.db.models.fields.CharField')(max_length=255, null=True, blank=True)),	
            ('date_modified', self.gf('django.db.models.fields.DateTimeField')(auto_now=True, blank=True)),	
            ('image', self.gf('django.db.models.fields.files.ImageField')(max_length=100, db_column='path', db_index=True)),	
            ('object_id', self.gf('django.db.models.fields.PositiveIntegerField')()),	
            ('height', self.gf('django.db.models.fields.PositiveIntegerField')(null=True, blank=True)),	
            ('width', self.gf('django.db.models.fields.PositiveIntegerField')(null=True, blank=True)),	
            ('content_type', self.gf('django.db.models.fields.related.ForeignKey')(to=orm['contenttypes.ContentType'])),	
            ('date_created', self.gf('django.db.models.fields.DateTimeField')(auto_now_add=True, blank=True)),	
            ('id', self.gf('django.db.models.fields.AutoField')(primary_key=True)),	
        ))	
        db.send_create_signal('cropduster', ['Image'])	


        # Adding unique constraint on 'Image', fields ['content_type', 'object_id']	    initial = True
        db.create_unique('cropduster4_image', ['content_type_id', 'object_id'])	


        # Adding M2M table for field thumbs on 'Image'	    dependencies = [
        db.create_table('cropduster4_image_thumbs', (	        ('contenttypes', '0002_remove_content_type_name'),
            ('id', models.AutoField(verbose_name='ID', primary_key=True, auto_created=True)),	    ]
            ('image', models.ForeignKey(orm['cropduster.image'], null=False)),	
            ('thumb', models.ForeignKey(orm['cropduster.thumb'], null=False))	
        ))	
        db.create_unique('cropduster4_image_thumbs', ['image_id', 'thumb_id'])	


    def backwards(self, orm):	

        # Deleting model 'Thumb'	
        db.delete_table('cropduster4_thumb')	


        # Deleting model 'Image'	    operations = [
        db.delete_table('cropduster4_image')	        migrations.CreateModel(

            name='Image',
        # Removing unique constraint on 'Image', fields ['content_type', 'object_id']	            fields=[
        db.delete_unique('cropduster4_image', ['content_type_id', 'object_id'])	                ('id', models.AutoField(verbose_name='ID', serialize=False, auto_created=True, primary_key=True)),

                ('object_id', models.PositiveIntegerField(null=True, blank=True)),
        # Removing M2M table for field thumbs on 'Image'	                ('field_identifier', models.SlugField(blank=True, default='')),
        db.delete_table('cropduster4_image_thumbs')	                ('prev_object_id', models.PositiveIntegerField(null=True, blank=True)),

                ('width', models.PositiveIntegerField(null=True, blank=True)),

                ('height', models.PositiveIntegerField(null=True, blank=True)),
    models = {	                ('image', cropduster.fields.CropDusterSimpleImageField(db_column='path', db_index=True, height_field='height', storage=cropduster.models.StrFileSystemStorage(), upload_to=cropduster.models.generate_filename, width_field='width')),
        'contenttypes.contenttype': {	                ('date_created', models.DateTimeField(auto_now_add=True)),
            'Meta': {'unique_together': "(('app_label', 'model'),)", 'object_name': 'ContentType', 'db_table': "'django_content_type'"},	                ('date_modified', models.DateTimeField(auto_now=True)),
            'app_label': ('django.db.models.fields.CharField', [], {'max_length': '100'}),	                ('attribution', models.CharField(max_length=255, null=True, blank=True)),
            'id': ('django.db.models.fields.AutoField', [], {'primary_key': 'True'}),	                ('attribution_link', models.URLField(max_length=255, null=True, blank=True)),
            'model': ('django.db.models.fields.CharField', [], {'max_length': '100'}),	                ('caption', models.TextField(null=True, blank=True)),
            'name': ('django.db.models.fields.CharField', [], {'max_length': '100'})	                ('content_type', models.ForeignKey(to='contenttypes.ContentType', on_delete=models.CASCADE)),
        },	            ],
        'cropduster.image': {	            options={
            'Meta': {'unique_together': "(('content_type', 'object_id'),)", 'object_name': 'Image', 'db_table': "'cropduster4_image'"},	                'db_table': '%s_image' % cropduster.settings.CROPDUSTER_DB_PREFIX,
            'attribution': ('django.db.models.fields.CharField', [], {'max_length': '255', 'null': 'True', 'blank': 'True'}),	            },
            'content_type': ('django.db.models.fields.related.ForeignKey', [], {'to': "orm['contenttypes.ContentType']"}),	        ),
            'date_created': ('django.db.models.fields.DateTimeField', [], {'auto_now_add': 'True', 'blank': 'True'}),	        migrations.CreateModel(
            'date_modified': ('django.db.models.fields.DateTimeField', [], {'auto_now': 'True', 'blank': 'True'}),	            name='StandaloneImage',
            'height': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),	            fields=[
            'id': ('django.db.models.fields.AutoField', [], {'primary_key': 'True'}),	                ('id', models.AutoField(verbose_name='ID', serialize=False, auto_created=True, primary_key=True)),
            'image': ('django.db.models.fields.files.ImageField', [], {'max_length': '100', 'db_column': "'path'", 'db_index': 'True'}),	                ('md5', models.CharField(max_length=32, blank=True, default='')),
            'object_id': ('django.db.models.fields.PositiveIntegerField', [], {}),	                ('image', cropduster.fields.CropDusterImageField(blank=True, db_column='image', default='', upload_to='')),
            'thumbs': ('django.db.models.fields.related.ManyToManyField', [], {'blank': 'True', 'related_name': "'thumbs'", 'null': 'True', 'symmetrical': 'False', 'to': "orm['cropduster.Thumb']"}),	            ],
            'width': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'})	            options={
        },	                'db_table': '%s_standaloneimage' % cropduster.settings.CROPDUSTER_DB_PREFIX,
        'cropduster.thumb': {	            },
            'Meta': {'object_name': 'Thumb', 'db_table': "'cropduster4_thumb'"},	        ),
            'crop_h': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),	        migrations.CreateModel(
            'crop_w': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),	            name='Thumb',
            'crop_x': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),	            fields=[
            'crop_y': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),	                ('id', models.AutoField(verbose_name='ID', serialize=False, auto_created=True, primary_key=True)),
            'date_modified': ('django.db.models.fields.DateTimeField', [], {'auto_now': 'True', 'blank': 'True'}),	                ('name', models.CharField(max_length=255, db_index=True)),
            'height': ('django.db.models.fields.PositiveIntegerField', [], {'default': '0', 'null': 'True', 'blank': 'True'}),	                ('width', models.PositiveIntegerField(default=0, null=True, blank=True)),
            'id': ('django.db.models.fields.AutoField', [], {'primary_key': 'True'}),	                ('height', models.PositiveIntegerField(default=0, null=True, blank=True)),
            'name': ('django.db.models.fields.CharField', [], {'max_length': '255', 'db_index': 'True'}),	                ('crop_x', models.PositiveIntegerField(null=True, blank=True)),
            'reference_thumb': ('django.db.models.fields.related.ForeignKey', [], {'to': "orm['cropduster.Thumb']", 'null': 'True', 'blank': 'True'}),	                ('crop_y', models.PositiveIntegerField(null=True, blank=True)),
            'width': ('django.db.models.fields.PositiveIntegerField', [], {'default': '0', 'null': 'True', 'blank': 'True'})	                ('crop_w', models.PositiveIntegerField(null=True, blank=True)),
        }	                ('crop_h', models.PositiveIntegerField(null=True, blank=True)),
    }	                ('date_modified', models.DateTimeField(auto_now=True)),

                ('image', models.ForeignKey(related_name='+', to='cropduster.Image', blank=True, null=True, on_delete=models.CASCADE)),
    complete_apps = ['cropduster']	                ('reference_thumb', models.ForeignKey(related_name='auto_set', blank=True, to='cropduster.Thumb', null=True, on_delete=models.CASCADE)),
            ],
            options={
                'db_table': '%s_thumb' % cropduster.settings.CROPDUSTER_DB_PREFIX,
            },
        ),
    ] + ([] if django.VERSION < (1, 9) else [
        migrations.AddField(
            model_name='image',
            name='thumbs',
            field=cropduster.fields.ReverseForeignRelation(blank=True, field_name='image', serialize=False, to='cropduster.Thumb', is_migration=True),
        ),
    ]) + [
        migrations.AlterUniqueTogether(
            name='image',
            unique_together=set([('content_type', 'object_id', 'field_identifier')]),
        ),
    ]
 17  
cropduster/migrations/0002_alt_text.py
@@ -0,0 +1,17 @@
from django.db import migrations, models
import cropduster.fields


class Migration(migrations.Migration):

    dependencies = [
        ('cropduster', '0001_initial'),
    ]

    operations = [
        migrations.AddField(
            model_name='image',
            name='alt_text',
            field=models.TextField(null=False, default="", verbose_name=b'Alt Text', blank=True),
        ),
    ]
 572  
cropduster/models.py
Large diffs are not rendered by default.

 70  
cropduster/patch/__init__.py
This file was deleted.

 97  
cropduster/patch/utils.py
This file was deleted.

 376  
cropduster/related.py
This file was deleted.

  243  
cropduster/resizing.py
@@ -1,23 +1,62 @@
from __future__ import division	from __future__ import division

import os	import os
import re	import re
import math	import math
import hashlib	import hashlib
import tempfile

import PIL.Image

from django.core.exceptions import ImproperlyConfigured
from django.utils import six
from django.utils.encoding import python_2_unicode_compatible
from django.utils.six.moves import filter
from django.core.files.storage import default_storage

from .settings import CROPDUSTER_RETAIN_METADATA




__all__ = ('Size', 'Box', 'Crop')	__all__ = ('Size', 'Box', 'Crop')




INFINITY = float('inf')


@python_2_unicode_compatible
class SizeAlias(object):
    is_alias = True

    def __init__(self, alias, to):
        self.alias = alias
        self.to = to

    def __str__(self):
        return u'Size %s => %s' % (self.alias, self.to)

    def add_to_sizes_dict(self, sizes):
        keys = re.split(r'(?<!\\)\.', self.alias)
        size_to = sizes.get(self.to)
        if not size_to:
            return
        ctx = sizes
        for key in keys:
            ctx.setdefault(key, {})
            ctx = ctx[key]
        ctx.update(size_to)


@python_2_unicode_compatible
class Size(object):	class Size(object):


    is_alias = False
    parent = None	    parent = None


    def __init__(self, name, label=None, w=None, h=None, retina=False, auto=None, min_w=None, min_h=None,	    def __init__(self, name, label=None, w=None, h=None, retina=False, auto=None, min_w=None, min_h=None,
            max_w=None, max_h=None):	            max_w=None, max_h=None, required=True):
        from django.core.exceptions import ImproperlyConfigured	


        self.min_w = max(w, min_w) or 1	        self.min_w = max(w or 1, min_w or 1) or 1
        self.min_h = max(h, min_h) or 1	        self.min_h = max(h or 1, min_h or 1) or 1
        self.max_w = max_w	        self.max_w = max_w
        self.max_h = max_h	        self.max_h = max_h


@@ -38,8 +77,24 @@ def __init__(self, name, label=None, w=None, h=None, retina=False, auto=None, mi
        self.width = w	        self.width = w
        self.height = h	        self.height = h
        self.label = label or u' '.join(filter(None, re.split(r'[_\-]', name))).title()	        self.label = label or u' '.join(filter(None, re.split(r'[_\-]', name))).title()
        self.required = required

        self.min_aspect = (self.w / self.h) if (self.w and self.h) else 0
        self.max_aspect = self.min_aspect or INFINITY

        if self.w and self.min_h > 1:
            self.max_aspect = min(self.max_aspect, self.w / self.min_h)

        if self.w and self.max_h:
            self.min_aspect = max(self.min_aspect, self.w / self.max_h)


    def __unicode__(self):	        if self.h and self.min_w > 1:
            self.min_aspect = max(self.min_aspect, self.min_w / self.h)

        if self.h and self.max_w:
            self.max_aspect = min(self.max_aspect, self.max_w / self.h)

    def __str__(self):
        name = u'Size %s (%s):' % (self.label, self.name)	        name = u'Size %s (%s):' % (self.label, self.name)
        if self.auto:	        if self.auto:
            name = u'%s[auto]' % name	            name = u'%s[auto]' % name
@@ -67,8 +122,10 @@ def is_auto(self):
        return self.parent is not None	        return self.parent is not None


    @staticmethod	    @staticmethod
    def flatten(sizes):	    def flatten(sizes, include_aliases=False):
        for size in sizes:	        for size in sizes:
            if isinstance(size, SizeAlias) and not include_aliases:
                continue
            yield size	            yield size
            if size.auto:	            if size.auto:
                for auto_size in size.auto:	                for auto_size in size.auto:
@@ -80,6 +137,11 @@ def aspect_ratio(self):
            return None	            return None
        return self.width / self.height	        return self.width / self.height


    def fit_image(self, original_image):
        orig_w, orig_h = original_image.size
        crop = Crop(Box(0, 0, orig_w, orig_h), original_image)
        return self.fit_to_crop(crop, original_image=original_image)

    def fit_to_crop(self, crop, original_image=None):	    def fit_to_crop(self, crop, original_image=None):
        from cropduster.models import Thumb	        from cropduster.models import Thumb


@@ -92,6 +154,8 @@ def fit_to_crop(self, crop, original_image=None):
            'min_h': self.min_h or self.height,	            'min_h': self.min_h or self.height,
            'max_w': self.max_w,	            'max_w': self.max_w,
            'max_h': self.max_h,	            'max_h': self.max_h,
            'min_aspect': self.min_aspect,
            'max_aspect': self.max_aspect,
        }	        }
        if self.width and self.height:	        if self.width and self.height:
            best_fit_kwargs.update({'w': self.width, 'h': self.height})	            best_fit_kwargs.update({'w': self.width, 'h': self.height})
@@ -108,6 +172,7 @@ def __serialize__(self):
            'max_h': self.max_h,	            'max_h': self.max_h,
            'retina': 1 if self.retina else 0,	            'retina': 1 if self.retina else 0,
            'label': self.label,	            'label': self.label,
            'required': self.required,
            '__type__': 'Size',	            '__type__': 'Size',
        }	        }
        if self.auto:	        if self.auto:
@@ -142,7 +207,7 @@ def aspect_ratio(self):
    @property	    @property
    def midpoint(self):	    def midpoint(self):
        x = (self.x1 + self.x2) / 2	        x = (self.x1 + self.x2) / 2
        y = (self.y1 + self.y2) / 2;	        y = (self.y1 + self.y2) / 2
        return (x, y)	        return (x, y)


    @property	    @property
@@ -152,48 +217,66 @@ def size(self):
    def as_tuple(self):	    def as_tuple(self):
        return (self.x1, self.y1, self.x2, self.y2)	        return (self.x1, self.y1, self.x2, self.y2)


    def __eq__(self, other):
        return (isinstance(other, self.__class__) and self.as_tuple() == other.as_tuple())

    def __ne__(self, other):
        return not self.__eq__(other)



class Crop(object):	class Crop(object):


    def __init__(self, box, image):	    def __init__(self, box, image):
        if isinstance(image, six.string_types):
            self._fh = default_storage.open(image, mode='rb')
            image = PIL.Image.open(self._fh)

        self.box = box	        self.box = box
        self.image = image	        self.image = image
        self.bounds = Box(0, 0, *image.size)	        self.bounds = Box(0, 0, *image.size)


    def create_image(self, width=None, height=None, max_w=None, max_h=None):	    def close(self):
        import PIL.Image	        if hasattr(self, '_fh') and not self._fh.closed:
        from cropduster.exceptions import CropDusterResizeException	            self._fh.close()


        image = self.image.copy()	    def __del__(self):
        image.load()	        self.close()
        new_image = image.crop(self.box.as_tuple())	
        new_image.load()	    def create_image(self, output_filename, width, height):
        new_w, new_h = new_image.size	        from cropduster.utils import process_image, get_image_extension
        if new_w < width or new_h < height:	
            raise CropDusterResizeException(	        temp_file = tempfile.NamedTemporaryFile(suffix=get_image_extension(self.image), delete=False)
                u"Crop box (%dx%d) is too small for resize to (%dx%d)" % (new_w, new_h, width, height))	        temp_filename = temp_file.name

        with default_storage.open(self.image.filename, mode='rb') as f:
        # Scale our initial width and height based on the max_w and max_h	            temp_file.write(f.read())
        max_scales = []	        temp_file.seek(0)
        if max_w and max_w < width:	        image = PIL.Image.open(temp_filename)
            max_scales.append(max_w / width)	        image.filename = self.image.filename
        if max_h and max_h < height:	
            max_scales.append(max_h / height)	        crop_args = self.box.as_tuple()
        if max_scales:	
            max_scale = min(max_scales)	        def crop_and_resize_callback(im):
            width = int(round(width * max_scale))	            from cropduster.utils import smart_resize
            height = int(round(height * max_scale))	            im = im.crop(crop_args)
        if new_w > width or new_h > height:	            return smart_resize(im, final_w=width, final_h=height)
            new_image = new_image.resize((width, height), PIL.Image.ANTIALIAS)	
        new_image = process_image(image, output_filename, crop_and_resize_callback)
        new_image.crop = self	        new_image.crop = self
        temp_file.close()
        os.unlink(temp_filename)
        return new_image	        return new_image


    def best_fit(self, w=None, h=None, min_w=None, min_h=None, max_w=None, max_h=None):	    def best_fit(self, w=None, h=None, min_w=None, min_h=None, max_w=None, max_h=None, min_aspect=None, max_aspect=None):
        if w and h:	        if w and h:
            aspect_ratio = w / h	            aspect_ratio = w / h
        else:	        else:
            aspect_ratio = self.box.aspect_ratio	            aspect_ratio = self.box.aspect_ratio


        if min_aspect and aspect_ratio < min_aspect:
            aspect_ratio = min_aspect
        elif max_aspect and aspect_ratio > max_aspect:
            aspect_ratio = max_aspect

        scale = math.sqrt(aspect_ratio / self.box.aspect_ratio)	        scale = math.sqrt(aspect_ratio / self.box.aspect_ratio)


        w = self.box.w * scale	        w = self.box.w * scale
@@ -240,12 +323,20 @@ def best_fit(self, w=None, h=None, min_w=None, min_h=None, max_w=None, max_h=Non
            scale_y = (y2 - y1) / initial_fit.h	            scale_y = (y2 - y1) / initial_fit.h


        if scale_y < scale_x:	        if scale_y < scale_x:
            # scale down the width to maintain aspect ratio
            w = (x2 - x1) * (scale_y / scale_x)	            w = (x2 - x1) * (scale_y / scale_x)
            # unless the scaled width would drop below the min_w
            if w < min_w:
                w = min_w
            dw = initial_fit.w - w	            dw = initial_fit.w - w
            x1 += (dw / 2)	            x1 += (dw / 2)
            x2 = x1 + w	            x2 = x1 + w
        elif scale_x < scale_y:	        elif scale_x <= scale_y:
            # scale down the height to maintain aspect ratio
            h = (y2 - y1) * (scale_x / scale_y)	            h = (y2 - y1) * (scale_x / scale_y)
            # unless the scaled height would drop below the min_h
            if h < min_h:
                h = min_h
            dh = initial_fit.h - h	            dh = initial_fit.h - h
            y1 += (dh / 2)	            y1 += (dh / 2)
            y2 = y1 + h	            y2 = y1 + h
@@ -258,50 +349,40 @@ def best_fit(self, w=None, h=None, min_w=None, min_h=None, max_w=None, max_h=Non
        x2 = min(int(round(x2)), self.bounds.x2, x1 + w)	        x2 = min(int(round(x2)), self.bounds.x2, x1 + w)
        y2 = min(int(round(y2)), self.bounds.y2, y1 + h)	        y2 = min(int(round(y2)), self.bounds.y2, y1 + h)


        # Fix off-by-one rounding errors
        if (x2 - x1 == w - 1):
            if x2 < self.bounds.x2:
                x2 += 1
            elif x1 > self.bounds.x1:
                x1 -= 1
        if (y2 - y1 == h - 1):
            if y2 < self.bounds.y2:
                y2 += 1
            elif y1 > self.bounds.y1:
                y1 -= 1

        return Crop(Box(x1, y1, x2, y2), self.image)	        return Crop(Box(x1, y1, x2, y2), self.image)


    def add_xmp_to_crop(self, cropped_image, size):	    def add_xmp_to_crop(self, cropped_image_path, size, original_image=None):
        from cropduster.standalone.metadata import libxmp, file_format_supported	        try:
            from cropduster.standalone.metadata import (libxmp,
                get_xmp_from_storage, put_xmp_to_storage)
        except ImproperlyConfigured:
            libxmp = None


        if not libxmp:	        if not libxmp or not cropped_image_path:
            return	            return


        from PIL.ImageFile import ImageFile	        if original_image and CROPDUSTER_RETAIN_METADATA:
        from django.db.models.fields.files import FieldFile	            original_metadata = get_xmp_from_storage(original_image.filename)
        from cropduster.models import Thumb	        else:

            original_metadata = None
        if isinstance(cropped_image, ImageFile):	
            image_path = cropped_image.filename	
        elif isinstance(cropped_image, file):	
            image_path = cropped_image.name	
        elif isinstance(cropped_image, FieldFile):	
            image_path = cropped_image.path	
        elif isinstance(cropped_image, Thumb):	
            try:	
                image = cropped_image.image_set.all()[0]	
            except IndexError:	
                return False	
            else:	
                image_path = image.get_image_path(cropped_image.name)	
        elif isinstance(cropped_image, basestring):	
            image_path = cropped_image	

        xmp_file = libxmp.XMPFiles(file_path=image_path, open_forupdate=True)	

        xmp_meta = self.generate_xmp(size)	


        if not xmp_file.can_put_xmp(xmp_meta):	        xmp_meta = self.generate_xmp(size, original_metadata=original_metadata)
            if not file_format_supported(image_path):	
                raise Exception("Image format of %s does not allow metadata" %(	
                        os.path.basename(image_path)))	
            else:	
                raise Exception("Could not add metadata to image %s" % (	
                        os.path.basename(image_path)))	


        xmp_file.put_xmp(xmp_meta)	        put_xmp_to_storage(xmp_meta, cropped_image_path)
        xmp_file.close_file()	


    def generate_xmp(self, size):	    def generate_xmp(self, size, original_metadata=None):
        from cropduster.standalone.metadata import libxmp	        from cropduster.standalone.metadata import libxmp
        from cropduster.utils import json	        from cropduster.utils import json


@@ -310,11 +391,11 @@ def generate_xmp(self, size):
        NS_CROP = "http://ns.thealtantic.com/cropduster/1.0/"	        NS_CROP = "http://ns.thealtantic.com/cropduster/1.0/"


        md5 = hashlib.md5()	        md5 = hashlib.md5()
        with open(self.image.filename) as f:	        with default_storage.open(self.image.filename, mode='rb') as f:
            md5.update(f.read())	            md5.update(f.read())
        digest = md5.hexdigest()	        digest = md5.hexdigest()


        md = libxmp.XMPMeta()	        md = original_metadata or libxmp.XMPMeta()
        md.register_namespace(NS_XMPMM, 'xmpMM')	        md.register_namespace(NS_XMPMM, 'xmpMM')
        md.register_namespace(NS_MWG_RS, 'mwg-rs')	        md.register_namespace(NS_MWG_RS, 'mwg-rs')
        md.register_namespace('http://ns.adobe.com/xap/1.0/sType/Dimensions#', 'stDim')	        md.register_namespace('http://ns.adobe.com/xap/1.0/sType/Dimensions#', 'stDim')
@@ -323,16 +404,20 @@ def generate_xmp(self, size):
        md.set_property(NS_CROP, 'crop:size/stDim:w', '%s' % (size.width or ''))	        md.set_property(NS_CROP, 'crop:size/stDim:w', '%s' % (size.width or ''))
        md.set_property(NS_CROP, 'crop:size/stDim:h', '%s' % (size.height or ''))	        md.set_property(NS_CROP, 'crop:size/stDim:h', '%s' % (size.height or ''))
        md.set_property(NS_CROP, 'crop:size/crop:json', json.dumps(size))	        md.set_property(NS_CROP, 'crop:size/crop:json', json.dumps(size))
        md.set_property(NS_XMPMM, 'xmpMM:DerivedFrom', u'xmp.did:%s' % digest.upper())	        md.set_property(NS_CROP, 'crop:md5', digest.upper())
        md.set_property(NS_MWG_RS, 'mwg-rs:Regions/mwg-rs:AppliedToDimensions', '', prop_value_is_struct=True)	        md.set_property(NS_MWG_RS, 'mwg-rs:Regions/mwg-rs:AppliedToDimensions', '', prop_value_is_struct=True)
        md.set_property(NS_MWG_RS, 'mwg-rs:Regions/mwg-rs:AppliedToDimensions/stDim:w', unicode(self.image.size[0]))	        md.set_property(NS_MWG_RS, 'mwg-rs:Regions/mwg-rs:AppliedToDimensions/stDim:w', six.text_type(self.image.size[0]))
        md.set_property(NS_MWG_RS, 'mwg-rs:Regions/mwg-rs:AppliedToDimensions/stDim:h', unicode(self.image.size[1]))	        md.set_property(NS_MWG_RS, 'mwg-rs:Regions/mwg-rs:AppliedToDimensions/stDim:h', six.text_type(self.image.size[1]))
        # Clear out any existing <mwg-rs:RegionList> tags so they don't conflict
        # (for instance, iPhone face regions are stored in this tag)
        if md.does_property_exist(NS_MWG_RS, 'mwg-rs:Regions/mwg-rs:RegionList'):
            md.delete_property(NS_MWG_RS, 'mwg-rs:Regions/mwg-rs:RegionList')
        md.set_property(NS_MWG_RS, 'mwg-rs:Regions/mwg-rs:RegionList', '', prop_value_is_array=True)	        md.set_property(NS_MWG_RS, 'mwg-rs:Regions/mwg-rs:RegionList', '', prop_value_is_array=True)
        md.set_property(NS_MWG_RS, 'mwg-rs:Regions/mwg-rs:RegionList[1]/mwg-rs:Name', 'Crop')	        md.set_property(NS_MWG_RS, 'mwg-rs:Regions/mwg-rs:RegionList[1]/mwg-rs:Name', 'Crop')
        md.set_property(NS_MWG_RS, 'mwg-rs:Regions/mwg-rs:RegionList[1]/mwg-rs:Area', '', prop_value_is_struct=True)	        md.set_property(NS_MWG_RS, 'mwg-rs:Regions/mwg-rs:RegionList[1]/mwg-rs:Area', '', prop_value_is_struct=True)
        md.set_property(NS_MWG_RS, 'mwg-rs:Regions/mwg-rs:RegionList[1]/mwg-rs:Area/stArea:unit', "normalized")	        md.set_property(NS_MWG_RS, 'mwg-rs:Regions/mwg-rs:RegionList[1]/mwg-rs:Area/stArea:unit', "normalized")
        md.set_property(NS_MWG_RS, 'mwg-rs:Regions/mwg-rs:RegionList[1]/mwg-rs:Area/stArea:w',    "%.5f" % (self.box.w  / self.bounds.w))	        md.set_property(NS_MWG_RS, 'mwg-rs:Regions/mwg-rs:RegionList[1]/mwg-rs:Area/stArea:w', "%.5f" % (self.box.w / self.bounds.w))
        md.set_property(NS_MWG_RS, 'mwg-rs:Regions/mwg-rs:RegionList[1]/mwg-rs:Area/stArea:h',    "%.5f" % (self.box.h  / self.bounds.h))	        md.set_property(NS_MWG_RS, 'mwg-rs:Regions/mwg-rs:RegionList[1]/mwg-rs:Area/stArea:h', "%.5f" % (self.box.h / self.bounds.h))
        md.set_property(NS_MWG_RS, 'mwg-rs:Regions/mwg-rs:RegionList[1]/mwg-rs:Area/stArea:x',    "%.5f" % (self.box.x1 / self.bounds.w))	        md.set_property(NS_MWG_RS, 'mwg-rs:Regions/mwg-rs:RegionList[1]/mwg-rs:Area/stArea:x', "%.5f" % (self.box.x1 / self.bounds.w))
        md.set_property(NS_MWG_RS, 'mwg-rs:Regions/mwg-rs:RegionList[1]/mwg-rs:Area/stArea:y',    "%.5f" % (self.box.y1 / self.bounds.h))	        md.set_property(NS_MWG_RS, 'mwg-rs:Regions/mwg-rs:RegionList[1]/mwg-rs:Area/stArea:y', "%.5f" % (self.box.y1 / self.bounds.h))
        return md	        return md
  41  
cropduster/settings.py
@@ -1,4 +1,10 @@
import math
import PIL
import distutils.spawn
from distutils.version import LooseVersion
from django.conf import settings	from django.conf import settings
from django.core.exceptions import ImproperlyConfigured
from django.utils import six




CROPDUSTER_MEDIA_ROOT = getattr(settings, 'CROPDUSTER_MEDIA_ROOT', settings.MEDIA_ROOT)	CROPDUSTER_MEDIA_ROOT = getattr(settings, 'CROPDUSTER_MEDIA_ROOT', settings.MEDIA_ROOT)
@@ -15,3 +21,38 @@


CROPDUSTER_PREVIEW_WIDTH = getattr(settings, 'CROPDUSTER_PREVIEW_WIDTH', 800)	CROPDUSTER_PREVIEW_WIDTH = getattr(settings, 'CROPDUSTER_PREVIEW_WIDTH', 800)
CROPDUSTER_PREVIEW_HEIGHT = getattr(settings, 'CROPDUSTER_PREVIEW_HEIGHT', 500)	CROPDUSTER_PREVIEW_HEIGHT = getattr(settings, 'CROPDUSTER_PREVIEW_HEIGHT', 500)


def default_jpeg_quality(width, height):
    p = math.sqrt(width * height)
    if p >= 1750:
        return 80
    elif p >= 1000:
        return 85
    else:
        return 90

CROPDUSTER_JPEG_QUALITY = getattr(settings, 'CROPDUSTER_JPEG_QUALITY', default_jpeg_quality)


def get_jpeg_quality(width, height):
    if six.callable(CROPDUSTER_JPEG_QUALITY):
        return CROPDUSTER_JPEG_QUALITY(width, height)
    elif isinstance(CROPDUSTER_JPEG_QUALITY, (int, float)):
        return CROPDUSTER_JPEG_QUALITY
    else:
        raise ImproperlyConfigured(
            "CROPDUSTER_JPEG_QUALITY setting must be either a callable "
            "or a numeric value, got type %s" % (type(CROPDUSTER_JPEG_QUALITY).__name__))

JPEG_SAVE_ICC_SUPPORTED = (LooseVersion(getattr(PIL, '__version__', '0'))
    >= LooseVersion('2.2.1'))

CROPDUSTER_GIFSICLE_PATH = getattr(settings, 'CROPDUSTER_GIFSICLE_PATH', None)

if CROPDUSTER_GIFSICLE_PATH is None:
    # Try to find executable in the PATH
    CROPDUSTER_GIFSICLE_PATH = distutils.spawn.find_executable("gifsicle")

CROPDUSTER_RETAIN_METADATA = getattr(settings, 'CROPDUSTER_RETAIN_METADATA', False)
CROPDUSTER_CREATE_THUMBS = getattr(settings, 'CROPDUSTER_CREATE_THUMBS', True)
 103  
cropduster/south_migrations/0001_initial.py
@@ -0,0 +1,103 @@
# encoding: utf-8
import datetime
from south.db import db
from south.v2 import SchemaMigration
from django.db import models

class Migration(SchemaMigration):

    def forwards(self, orm):

        # Adding model 'Thumb'
        db.create_table('cropduster4_thumb', (
            ('name', self.gf('django.db.models.fields.CharField')(max_length=255, db_index=True)),
            ('date_modified', self.gf('django.db.models.fields.DateTimeField')(auto_now=True, blank=True)),
            ('crop_h', self.gf('django.db.models.fields.PositiveIntegerField')(null=True, blank=True)),
            ('height', self.gf('django.db.models.fields.PositiveIntegerField')(default=0, null=True, blank=True)),
            ('width', self.gf('django.db.models.fields.PositiveIntegerField')(default=0, null=True, blank=True)),
            ('crop_w', self.gf('django.db.models.fields.PositiveIntegerField')(null=True, blank=True)),
            ('id', self.gf('django.db.models.fields.AutoField')(primary_key=True)),
            ('reference_thumb', self.gf('django.db.models.fields.related.ForeignKey')(to=orm['cropduster.Thumb'], null=True, blank=True)),
            ('crop_y', self.gf('django.db.models.fields.PositiveIntegerField')(null=True, blank=True)),
            ('crop_x', self.gf('django.db.models.fields.PositiveIntegerField')(null=True, blank=True)),
        ))
        db.send_create_signal('cropduster', ['Thumb'])

        # Adding model 'Image'
        db.create_table('cropduster4_image', (
            ('attribution', self.gf('django.db.models.fields.CharField')(max_length=255, null=True, blank=True)),
            ('date_modified', self.gf('django.db.models.fields.DateTimeField')(auto_now=True, blank=True)),
            ('image', self.gf('django.db.models.fields.files.ImageField')(max_length=100, db_column='path', db_index=True)),
            ('object_id', self.gf('django.db.models.fields.PositiveIntegerField')()),
            ('height', self.gf('django.db.models.fields.PositiveIntegerField')(null=True, blank=True)),
            ('width', self.gf('django.db.models.fields.PositiveIntegerField')(null=True, blank=True)),
            ('content_type', self.gf('django.db.models.fields.related.ForeignKey')(to=orm['contenttypes.ContentType'])),
            ('date_created', self.gf('django.db.models.fields.DateTimeField')(auto_now_add=True, blank=True)),
            ('id', self.gf('django.db.models.fields.AutoField')(primary_key=True)),
        ))
        db.send_create_signal('cropduster', ['Image'])

        # Adding unique constraint on 'Image', fields ['content_type', 'object_id']
        db.create_unique('cropduster4_image', ['content_type_id', 'object_id'])

        # Adding M2M table for field thumbs on 'Image'
        db.create_table('cropduster4_image_thumbs', (
            ('id', models.AutoField(verbose_name='ID', primary_key=True, auto_created=True)),
            ('image', models.ForeignKey(orm['cropduster.image'], null=False)),
            ('thumb', models.ForeignKey(orm['cropduster.thumb'], null=False))
        ))
        db.create_unique('cropduster4_image_thumbs', ['image_id', 'thumb_id'])


    def backwards(self, orm):

        # Deleting model 'Thumb'
        db.delete_table('cropduster4_thumb')

        # Deleting model 'Image'
        db.delete_table('cropduster4_image')

        # Removing unique constraint on 'Image', fields ['content_type', 'object_id']
        db.delete_unique('cropduster4_image', ['content_type_id', 'object_id'])

        # Removing M2M table for field thumbs on 'Image'
        db.delete_table('cropduster4_image_thumbs')


    models = {
        'contenttypes.contenttype': {
            'Meta': {'unique_together': "(('app_label', 'model'),)", 'object_name': 'ContentType', 'db_table': "'django_content_type'"},
            'app_label': ('django.db.models.fields.CharField', [], {'max_length': '100'}),
            'id': ('django.db.models.fields.AutoField', [], {'primary_key': 'True'}),
            'model': ('django.db.models.fields.CharField', [], {'max_length': '100'}),
            'name': ('django.db.models.fields.CharField', [], {'max_length': '100'})
        },
        'cropduster.image': {
            'Meta': {'unique_together': "(('content_type', 'object_id'),)", 'object_name': 'Image', 'db_table': "'cropduster4_image'"},
            'attribution': ('django.db.models.fields.CharField', [], {'max_length': '255', 'null': 'True', 'blank': 'True'}),
            'content_type': ('django.db.models.fields.related.ForeignKey', [], {'to': "orm['contenttypes.ContentType']"}),
            'date_created': ('django.db.models.fields.DateTimeField', [], {'auto_now_add': 'True', 'blank': 'True'}),
            'date_modified': ('django.db.models.fields.DateTimeField', [], {'auto_now': 'True', 'blank': 'True'}),
            'height': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'id': ('django.db.models.fields.AutoField', [], {'primary_key': 'True'}),
            'image': ('django.db.models.fields.files.ImageField', [], {'max_length': '100', 'db_column': "'path'", 'db_index': 'True'}),
            'object_id': ('django.db.models.fields.PositiveIntegerField', [], {}),
            'thumbs': ('django.db.models.fields.related.ManyToManyField', [], {'blank': 'True', 'related_name': "'thumbs'", 'null': 'True', 'symmetrical': 'False', 'to': "orm['cropduster.Thumb']"}),
            'width': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'})
        },
        'cropduster.thumb': {
            'Meta': {'object_name': 'Thumb', 'db_table': "'cropduster4_thumb'"},
            'crop_h': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'crop_w': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'crop_x': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'crop_y': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'date_modified': ('django.db.models.fields.DateTimeField', [], {'auto_now': 'True', 'blank': 'True'}),
            'height': ('django.db.models.fields.PositiveIntegerField', [], {'default': '0', 'null': 'True', 'blank': 'True'}),
            'id': ('django.db.models.fields.AutoField', [], {'primary_key': 'True'}),
            'name': ('django.db.models.fields.CharField', [], {'max_length': '255', 'db_index': 'True'}),
            'reference_thumb': ('django.db.models.fields.related.ForeignKey', [], {'to': "orm['cropduster.Thumb']", 'null': 'True', 'blank': 'True'}),
            'width': ('django.db.models.fields.PositiveIntegerField', [], {'default': '0', 'null': 'True', 'blank': 'True'})
        }
    }

    complete_apps = ['cropduster']
 0  
...rations/0002_auto__add_standaloneimage.py ??? ...rations/0002_auto__add_standaloneimage.py
File renamed without changes.
  5  
...o__add_field_image_prev_content_object.py ??? ...o__add_field_image_prev_content_object.py
@@ -15,7 +15,10 @@ def forwards(self, orm):
        db.alter_column('cropduster4_image', 'object_id', self.gf('django.db.models.fields.PositiveIntegerField')(null=True, blank=True))	        db.alter_column('cropduster4_image', 'object_id', self.gf('django.db.models.fields.PositiveIntegerField')(null=True, blank=True))


        # Removing unique constraint on 'Image', fields ['object_id', 'content_type']	        # Removing unique constraint on 'Image', fields ['object_id', 'content_type']
        db.delete_unique('cropduster4_image', ['object_id', 'content_type_id'])	        try:
            db.delete_unique('cropduster4_image', ['object_id', 'content_type_id'])
        except:
            pass


        # Adding unique constraint on 'Image', fields ['object_id', 'content_type', 'prev_object_id']	        # Adding unique constraint on 'Image', fields ['object_id', 'content_type', 'prev_object_id']
        db.create_unique('cropduster4_image', ['object_id', 'content_type_id', 'prev_object_id'])	        db.create_unique('cropduster4_image', ['object_id', 'content_type_id', 'prev_object_id'])
  3  
...igrations/0004_add_auto_thumb_m2m_rows.py ??? ...igrations/0004_add_auto_thumb_m2m_rows.py
@@ -7,6 +7,9 @@
class Migration(DataMigration):	class Migration(DataMigration):


    def forwards(self, orm):	    def forwards(self, orm):
        if db.dry_run:
            return

        Thumb = orm['cropduster.Thumb']	        Thumb = orm['cropduster.Thumb']
        Image = orm['cropduster.Image']	        Image = orm['cropduster.Image']
        M2M = Image.thumbs.through	        M2M = Image.thumbs.through
 72  
.../south_migrations/0005_auto__add_field_image_attribution_link__add_field_image_caption.py
@@ -0,0 +1,72 @@
# encoding: utf-8
import datetime
from south.db import db
from south.v2 import SchemaMigration
from django.db import models

class Migration(SchemaMigration):

    def forwards(self, orm):

        # Adding field 'Image.attribution_link'
        db.add_column(u'cropduster4_image', 'attribution_link', self.gf('django.db.models.fields.URLField')(max_length=255, null=True, blank=True), keep_default=False)

        # Adding field 'Image.caption'
        db.add_column(u'cropduster4_image', 'caption', self.gf('django.db.models.fields.CharField')(max_length=255, null=True, blank=True), keep_default=False)


    def backwards(self, orm):

        # Deleting field 'Image.attribution_link'
        db.delete_column(u'cropduster4_image', 'attribution_link')

        # Deleting field 'Image.caption'
        db.delete_column(u'cropduster4_image', 'caption')


    models = {
        'contenttypes.contenttype': {
            'Meta': {'unique_together': "(('app_label', 'model'),)", 'object_name': 'ContentType', 'db_table': "'django_content_type'"},
            'app_label': ('django.db.models.fields.CharField', [], {'max_length': '100'}),
            'id': ('django.db.models.fields.AutoField', [], {'primary_key': 'True'}),
            'model': ('django.db.models.fields.CharField', [], {'max_length': '100'}),
            'name': ('django.db.models.fields.CharField', [], {'max_length': '100'})
        },
        'cropduster.image': {
            'Meta': {'unique_together': "(('content_type', 'object_id', 'prev_object_id'),)", 'object_name': 'Image', 'db_table': "u'cropduster4_image'"},
            'attribution': ('django.db.models.fields.CharField', [], {'max_length': '255', 'null': 'True', 'blank': 'True'}),
            'attribution_link': ('django.db.models.fields.URLField', [], {'max_length': '255', 'null': 'True', 'blank': 'True'}),
            'caption': ('django.db.models.fields.CharField', [], {'max_length': '255', 'null': 'True', 'blank': 'True'}),
            'content_type': ('django.db.models.fields.related.ForeignKey', [], {'to': "orm['contenttypes.ContentType']"}),
            'date_created': ('django.db.models.fields.DateTimeField', [], {'auto_now_add': 'True', 'blank': 'True'}),
            'date_modified': ('django.db.models.fields.DateTimeField', [], {'auto_now': 'True', 'blank': 'True'}),
            'height': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'id': ('django.db.models.fields.AutoField', [], {'primary_key': 'True'}),
            'image': ('django.db.models.fields.files.ImageField', [], {'max_length': '100', 'db_column': "'path'", 'db_index': 'True'}),
            'object_id': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'prev_object_id': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'thumbs': ('cropduster.fields.CropDusterThumbField', [], {'blank': 'True', 'related_name': "'image_set'", 'null': 'True', 'symmetrical': 'False', 'to': "orm['cropduster.Thumb']"}),
            'width': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'})
        },
        'cropduster.standaloneimage': {
            'Meta': {'object_name': 'StandaloneImage', 'db_table': "u'cropduster4_standaloneimage'"},
            'id': ('django.db.models.fields.AutoField', [], {'primary_key': 'True'}),
            'image': ('cropduster.fields.CropDusterField', [], {'to': "orm['cropduster.Image']", 'max_length': '100', 'sizes': "[{'max_w': None, 'retina': 0, 'min_h': 1, 'name': 'crop', 'w': None, 'h': None, 'min_w': 1, '__type__': 'Size', 'max_h': None, 'label': u'Crop'}]"}),
            'md5': ('django.db.models.fields.CharField', [], {'max_length': '32'})
        },
        'cropduster.thumb': {
            'Meta': {'object_name': 'Thumb', 'db_table': "u'cropduster4_thumb'"},
            'crop_h': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'crop_w': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'crop_x': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'crop_y': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'date_modified': ('django.db.models.fields.DateTimeField', [], {'auto_now': 'True', 'blank': 'True'}),
            'height': ('django.db.models.fields.PositiveIntegerField', [], {'default': '0', 'null': 'True', 'blank': 'True'}),
            'id': ('django.db.models.fields.AutoField', [], {'primary_key': 'True'}),
            'name': ('django.db.models.fields.CharField', [], {'max_length': '255', 'db_index': 'True'}),
            'reference_thumb': ('django.db.models.fields.related.ForeignKey', [], {'blank': 'True', 'related_name': "'auto_set'", 'null': 'True', 'to': "orm['cropduster.Thumb']"}),
            'width': ('django.db.models.fields.PositiveIntegerField', [], {'default': '0', 'null': 'True', 'blank': 'True'})
        }
    }

    complete_apps = ['cropduster']
 88  
cropduster/south_migrations/0006_auto__add_field_thumb_image.py
@@ -0,0 +1,88 @@
# encoding: utf-8
import datetime
from south.db import db
from south.v2 import SchemaMigration
from django.db import models


class Migration(SchemaMigration):

    def forwards(self, orm):
        # Adding field 'Thumb.image'
        db.add_column('cropduster4_thumb', 'image', self.gf('django.db.models.fields.related.ForeignKey')(blank=True, related_name='+', null=True, to=orm['cropduster.Image']), keep_default=False)
        if not db.dry_run:
            Thumb = orm['cropduster.thumb']
            thumbs = Thumb.objects.filter(image_id__isnull=True)
            if thumbs.count() > 5000:
                print ("\n"
                    " ! There are too many cropduster4_thumb rows to migrate in South.\n\n"
                    " ! You will need to manually migrate the many-to-many table.\n")
                return

            for thumb in thumbs:
                try:
                    image = thumb.image_set.all()[0]
                except IndexError:
                    pass
                else:
                    thumb.image_id = image.pk
                    thumb.save()


    def backwards(self, orm):
        # Deleting field 'Thumb.image'
        db.delete_column('cropduster4_thumb', 'image_id')

    models = {
        'contenttypes.contenttype': {
            'Meta': {'unique_together': "(('app_label', 'model'),)", 'object_name': 'ContentType', 'db_table': "'django_content_type'"},
            'app_label': ('django.db.models.fields.CharField', [], {'max_length': '100'}),
            'id': ('django.db.models.fields.AutoField', [], {'primary_key': 'True'}),
            'model': ('django.db.models.fields.CharField', [], {'max_length': '100'}),
            'name': ('django.db.models.fields.CharField', [], {'max_length': '100'})
        },
        'cropduster.image': {
            'Meta': {'unique_together': "(('content_type', 'object_id', 'prev_object_id'),)", 'object_name': 'Image', 'db_table': "'cropduster4_image'"},
            'attribution': ('django.db.models.fields.CharField', [], {'max_length': '255', 'null': 'True', 'blank': 'True'}),
            'attribution_link': ('django.db.models.fields.URLField', [], {'max_length': '255', 'null': 'True', 'blank': 'True'}),
            'caption': ('django.db.models.fields.CharField', [], {'max_length': '255', 'null': 'True', 'blank': 'True'}),
            'content_type': ('django.db.models.fields.related.ForeignKey', [], {'to': "orm['contenttypes.ContentType']"}),
            'date_created': ('django.db.models.fields.DateTimeField', [], {'auto_now_add': 'True', 'blank': 'True'}),
            'date_modified': ('django.db.models.fields.DateTimeField', [], {'auto_now': 'True', 'blank': 'True'}),
            'height': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'id': ('django.db.models.fields.AutoField', [], {'primary_key': 'True'}),
            'image': ('django.db.models.fields.files.ImageField', [], {'max_length': '100', 'db_column': "'path'", 'db_index': 'True'}),
            'object_id': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'prev_object_id': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'width': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            '_thumbs': ('cropduster.fields.CropDusterThumbField', [], {'blank': 'True', 'related_name': "'image_set'", 'null': 'True', 'symmetrical': 'False', 'to': "orm['cropduster.Thumb']", 'through': "orm['cropduster.ImageThumbs']"}),
        },
        'cropduster.imagethumbs': {
            'Meta': {'object_name': 'ImageThumbs', 'db_table': "'cropduster4_image_thumbs'"},
            'image': ('django.db.models.fields.related.ForeignKey', [], {'to': "orm['cropduster.Image']"}),
            'thumb': ('django.db.models.fields.related.ForeignKey', [], {'to': "orm['cropduster.Thumb']"}),
            'id': ('django.db.models.fields.AutoField', [], {'primary_key': 'True'}),
        },
        'cropduster.standaloneimage': {
            'Meta': {'object_name': 'StandaloneImage', 'db_table': "'cropduster4_standaloneimage'"},
            'id': ('django.db.models.fields.AutoField', [], {'primary_key': 'True'}),
            'image': ('cropduster.fields.CropDusterField', [], {'to': "orm['cropduster.Image']", 'max_length': '100', 'sizes': "[{'max_w': None, 'retina': 0, 'min_h': 1, 'name': 'crop', 'w': None, 'h': None, 'min_w': 1, '__type__': 'Size', 'max_h': None, 'label': u'Crop'}]"}),
            'md5': ('django.db.models.fields.CharField', [], {'max_length': '32'})
        },
        'cropduster.thumb': {
            'Meta': {'object_name': 'Thumb', 'db_table': "'cropduster4_thumb'"},
            'crop_h': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'crop_w': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'crop_x': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'crop_y': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'date_modified': ('django.db.models.fields.DateTimeField', [], {'auto_now': 'True', 'blank': 'True'}),
            'height': ('django.db.models.fields.PositiveIntegerField', [], {'default': '0', 'null': 'True', 'blank': 'True'}),
            'id': ('django.db.models.fields.AutoField', [], {'primary_key': 'True'}),
            'image': ('django.db.models.fields.related.ForeignKey', [], {'blank': 'True', 'related_name': "'+'", 'null': 'True', 'to': "orm['cropduster.Image']"}),
            'name': ('django.db.models.fields.CharField', [], {'max_length': '255', 'db_index': 'True'}),
            'reference_thumb': ('django.db.models.fields.related.ForeignKey', [], {'blank': 'True', 'related_name': "'auto_set'", 'null': 'True', 'to': "orm['cropduster.Thumb']"}),
            'width': ('django.db.models.fields.PositiveIntegerField', [], {'default': '0', 'null': 'True', 'blank': 'True'})
        }
    }

    complete_apps = ['cropduster']
 66  
cropduster/south_migrations/0007_auto__del_imagethumbs__chg_field_image_caption.py
@@ -0,0 +1,66 @@
# encoding: utf-8
import datetime
from south.db import db
from south.v2 import SchemaMigration
from django.db import models

class Migration(SchemaMigration):

    def forwards(self, orm):

        # Changing field 'Image.caption'
        db.alter_column('cropduster4_image', 'caption', self.gf('django.db.models.fields.TextField')(null=True, blank=True))


    def backwards(self, orm):

        # Changing field 'Image.caption'
        db.alter_column('cropduster4_image', 'caption', self.gf('django.db.models.fields.CharField')(max_length=255, null=True, blank=True))


    models = {
        'contenttypes.contenttype': {
            'Meta': {'unique_together': "(('app_label', 'model'),)", 'object_name': 'ContentType', 'db_table': "'django_content_type'"},
            'app_label': ('django.db.models.fields.CharField', [], {'max_length': '100'}),
            'id': ('django.db.models.fields.AutoField', [], {'primary_key': 'True'}),
            'model': ('django.db.models.fields.CharField', [], {'max_length': '100'}),
            'name': ('django.db.models.fields.CharField', [], {'max_length': '100'})
        },
        'cropduster.image': {
            'Meta': {'unique_together': "(('content_type', 'object_id', 'prev_object_id'),)", 'object_name': 'Image', 'db_table': "'cropduster4_image'"},
            'attribution': ('django.db.models.fields.CharField', [], {'max_length': '255', 'null': 'True', 'blank': 'True'}),
            'attribution_link': ('django.db.models.fields.URLField', [], {'max_length': '255', 'null': 'True', 'blank': 'True'}),
            'caption': ('django.db.models.fields.TextField', [], {'null': 'True', 'blank': 'True'}),
            'content_type': ('django.db.models.fields.related.ForeignKey', [], {'to': "orm['contenttypes.ContentType']"}),
            'date_created': ('django.db.models.fields.DateTimeField', [], {'auto_now_add': 'True', 'blank': 'True'}),
            'date_modified': ('django.db.models.fields.DateTimeField', [], {'auto_now': 'True', 'blank': 'True'}),
            'height': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'id': ('django.db.models.fields.AutoField', [], {'primary_key': 'True'}),
            'image': ('django.db.models.fields.files.ImageField', [], {'max_length': '100', 'db_column': "'path'", 'db_index': 'True'}),
            'object_id': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'prev_object_id': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'width': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'})
        },
        'cropduster.standaloneimage': {
            'Meta': {'object_name': 'StandaloneImage', 'db_table': "'cropduster4_standaloneimage'"},
            'id': ('django.db.models.fields.AutoField', [], {'primary_key': 'True'}),
            'image': ('cropduster.fields.CropDusterField', [], {'to': "orm['cropduster.Image']", 'max_length': '100', 'sizes': "[{'max_w': None, 'retina': 0, 'min_h': 1, 'name': 'crop', 'w': None, 'h': None, 'min_w': 1, '__type__': 'Size', 'max_h': None, 'label': u'Crop'}]"}),
            'md5': ('django.db.models.fields.CharField', [], {'max_length': '32'})
        },
        'cropduster.thumb': {
            'Meta': {'object_name': 'Thumb', 'db_table': "'cropduster4_thumb'"},
            'crop_h': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'crop_w': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'crop_x': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'crop_y': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'date_modified': ('django.db.models.fields.DateTimeField', [], {'auto_now': 'True', 'blank': 'True'}),
            'height': ('django.db.models.fields.PositiveIntegerField', [], {'default': '0', 'null': 'True', 'blank': 'True'}),
            'id': ('django.db.models.fields.AutoField', [], {'primary_key': 'True'}),
            'image': ('django.db.models.fields.related.ForeignKey', [], {'blank': 'True', 'related_name': "'+'", 'null': 'True', 'to': "orm['cropduster.Image']"}),
            'name': ('django.db.models.fields.CharField', [], {'max_length': '255', 'db_index': 'True'}),
            'reference_thumb': ('django.db.models.fields.related.ForeignKey', [], {'blank': 'True', 'related_name': "'auto_set'", 'null': 'True', 'to': "orm['cropduster.Thumb']"}),
            'width': ('django.db.models.fields.PositiveIntegerField', [], {'default': '0', 'null': 'True', 'blank': 'True'})
        }
    }

    complete_apps = ['cropduster']
 75  
cropduster/south_migrations/0008_auto__add_field_image_field_identifier.py
@@ -0,0 +1,75 @@
from south.db import db
from south.v2 import SchemaMigration


class Migration(SchemaMigration):

    def forwards(self, orm):

        # Adding field 'Image.field_identifier'
        db.add_column('cropduster4_image', 'field_identifier', self.gf('django.db.models.fields.SlugField')(db_index=True, max_length=50, null=True, blank=True), keep_default=False)

        # Removing unique constraint on 'Image', fields ['object_id', 'content_type', 'prev_object_id']
        db.delete_unique('cropduster4_image', ['object_id', 'content_type_id', 'prev_object_id'])

        # Adding unique constraint on 'Image', fields ['field_identifier', 'object_id', 'content_type', 'prev_object_id']
        db.create_unique('cropduster4_image', ['field_identifier', 'object_id', 'content_type_id', 'prev_object_id'])

    def backwards(self, orm):

        # Deleting field 'Image.field_identifier'
        db.delete_column('cropduster4_image', 'field_identifier')

        # Adding unique constraint on 'Image', fields ['object_id', 'content_type', 'prev_object_id']
        db.create_unique('cropduster4_image', ['object_id', 'content_type_id', 'prev_object_id'])

        # Removing unique constraint on 'Image', fields ['field_identifier', 'object_id', 'content_type', 'prev_object_id']
        db.delete_unique('cropduster4_image', ['field_identifier', 'object_id', 'content_type_id', 'prev_object_id'])

    models = {
        'contenttypes.contenttype': {
            'Meta': {'unique_together': "(('app_label', 'model'),)", 'object_name': 'ContentType', 'db_table': "'django_content_type'"},
            'app_label': ('django.db.models.fields.CharField', [], {'max_length': '100'}),
            'id': ('django.db.models.fields.AutoField', [], {'primary_key': 'True'}),
            'model': ('django.db.models.fields.CharField', [], {'max_length': '100'}),
            'name': ('django.db.models.fields.CharField', [], {'max_length': '100'})
        },
        'cropduster.image': {
            'Meta': {'unique_together': "(('content_type', 'object_id', 'prev_object_id', 'field_identifier'),)", 'object_name': 'Image', 'db_table': "'cropduster4_image'"},
            'attribution': ('django.db.models.fields.CharField', [], {'max_length': '255', 'null': 'True', 'blank': 'True'}),
            'attribution_link': ('django.db.models.fields.URLField', [], {'max_length': '255', 'null': 'True', 'blank': 'True'}),
            'caption': ('django.db.models.fields.TextField', [], {'null': 'True', 'blank': 'True'}),
            'content_type': ('django.db.models.fields.related.ForeignKey', [], {'to': "orm['contenttypes.ContentType']"}),
            'date_created': ('django.db.models.fields.DateTimeField', [], {'auto_now_add': 'True', 'blank': 'True'}),
            'date_modified': ('django.db.models.fields.DateTimeField', [], {'auto_now': 'True', 'blank': 'True'}),
            'field_identifier': ('django.db.models.fields.SlugField', [], {'db_index': 'True', 'max_length': '50', 'null': 'True', 'blank': 'True'}),
            'height': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'id': ('django.db.models.fields.AutoField', [], {'primary_key': 'True'}),
            'image': ('django.db.models.fields.files.ImageField', [], {'max_length': '100', 'db_column': "'path'", 'db_index': 'True'}),
            'object_id': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'prev_object_id': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'width': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'})
        },
        'cropduster.standaloneimage': {
            'Meta': {'object_name': 'StandaloneImage', 'db_table': "'cropduster4_standaloneimage'"},
            'id': ('django.db.models.fields.AutoField', [], {'primary_key': 'True'}),
            'image': ('cropduster.fields.CropDusterField', [], {'to': "orm['cropduster.Image']", 'max_length': '100', 'sizes': "[{'max_w': None, 'retina': 0, 'min_h': 1, 'name': 'crop', 'w': None, 'h': None, 'min_w': 1, '__type__': 'Size', 'max_h': None, 'label': u'Crop'}]"}),
            'md5': ('django.db.models.fields.CharField', [], {'max_length': '32'})
        },
        'cropduster.thumb': {
            'Meta': {'object_name': 'Thumb', 'db_table': "'cropduster4_thumb'"},
            'crop_h': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'crop_w': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'crop_x': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'crop_y': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'date_modified': ('django.db.models.fields.DateTimeField', [], {'auto_now': 'True', 'blank': 'True'}),
            'height': ('django.db.models.fields.PositiveIntegerField', [], {'default': '0', 'null': 'True', 'blank': 'True'}),
            'id': ('django.db.models.fields.AutoField', [], {'primary_key': 'True'}),
            'image': ('django.db.models.fields.related.ForeignKey', [], {'blank': 'True', 'related_name': "'+'", 'null': 'True', 'to': "orm['cropduster.Image']"}),
            'name': ('django.db.models.fields.CharField', [], {'max_length': '255', 'db_index': 'True'}),
            'reference_thumb': ('django.db.models.fields.related.ForeignKey', [], {'blank': 'True', 'related_name': "'auto_set'", 'null': 'True', 'to': "orm['cropduster.Thumb']"}),
            'width': ('django.db.models.fields.PositiveIntegerField', [], {'default': '0', 'null': 'True', 'blank': 'True'})
        }
    }

    complete_apps = ['cropduster']
 73  
...migrations/0009_auto__del_unique_image_field_identifier_object_id_content_type_prev_ob.py
@@ -0,0 +1,73 @@
# encoding: utf-8
import datetime
from south.db import db
from south.v2 import SchemaMigration
from django.db import models

class Migration(SchemaMigration):

    def forwards(self, orm):

        # Removing unique constraint on 'Image', fields ['field_identifier', 'object_id', 'content_type', 'prev_object_id']
        db.delete_unique('cropduster4_image', ['field_identifier', 'object_id', 'content_type_id', 'prev_object_id'])

        # Adding unique constraint on 'Image', fields ['field_identifier', 'object_id', 'content_type']
        db.create_unique('cropduster4_image', ['field_identifier', 'object_id', 'content_type_id'])


    def backwards(self, orm):

        # Adding unique constraint on 'Image', fields ['field_identifier', 'object_id', 'content_type', 'prev_object_id']
        db.create_unique('cropduster4_image', ['field_identifier', 'object_id', 'content_type_id', 'prev_object_id'])

        # Removing unique constraint on 'Image', fields ['field_identifier', 'object_id', 'content_type']
        db.delete_unique('cropduster4_image', ['field_identifier', 'object_id', 'content_type_id'])


    models = {
        'contenttypes.contenttype': {
            'Meta': {'unique_together': "(('app_label', 'model'),)", 'object_name': 'ContentType', 'db_table': "'django_content_type'"},
            'app_label': ('django.db.models.fields.CharField', [], {'max_length': '100'}),
            'id': ('django.db.models.fields.AutoField', [], {'primary_key': 'True'}),
            'model': ('django.db.models.fields.CharField', [], {'max_length': '100'}),
            'name': ('django.db.models.fields.CharField', [], {'max_length': '100'})
        },
        'cropduster.image': {
            'Meta': {'unique_together': "(('content_type', 'object_id', 'field_identifier'),)", 'object_name': 'Image', 'db_table': "'cropduster4_image'"},
            'attribution': ('django.db.models.fields.CharField', [], {'max_length': '255', 'null': 'True', 'blank': 'True'}),
            'attribution_link': ('django.db.models.fields.URLField', [], {'max_length': '255', 'null': 'True', 'blank': 'True'}),
            'caption': ('django.db.models.fields.TextField', [], {'null': 'True', 'blank': 'True'}),
            'content_type': ('django.db.models.fields.related.ForeignKey', [], {'to': "orm['contenttypes.ContentType']"}),
            'date_created': ('django.db.models.fields.DateTimeField', [], {'auto_now_add': 'True', 'blank': 'True'}),
            'date_modified': ('django.db.models.fields.DateTimeField', [], {'auto_now': 'True', 'blank': 'True'}),
            'field_identifier': ('django.db.models.fields.SlugField', [], {'db_index': 'True', 'max_length': '50', 'null': 'True', 'blank': 'True'}),
            'height': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'id': ('django.db.models.fields.AutoField', [], {'primary_key': 'True'}),
            'image': ('django.db.models.fields.files.ImageField', [], {'max_length': '100', 'db_column': "'path'", 'db_index': 'True'}),
            'object_id': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'prev_object_id': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'width': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'})
        },
        'cropduster.standaloneimage': {
            'Meta': {'object_name': 'StandaloneImage', 'db_table': "'cropduster4_standaloneimage'"},
            'id': ('django.db.models.fields.AutoField', [], {'primary_key': 'True'}),
            'image': ('cropduster.fields.CropDusterField', [], {'to': "orm['cropduster.Image']", 'max_length': '100', 'sizes': "[{'max_w': None, 'retina': 0, 'min_h': 1, 'name': 'crop', 'w': None, 'h': None, 'min_w': 1, '__type__': 'Size', 'max_h': None, 'label': u'Crop'}]"}),
            'md5': ('django.db.models.fields.CharField', [], {'max_length': '32'})
        },
        'cropduster.thumb': {
            'Meta': {'object_name': 'Thumb', 'db_table': "'cropduster4_thumb'"},
            'crop_h': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'crop_w': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'crop_x': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'crop_y': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'date_modified': ('django.db.models.fields.DateTimeField', [], {'auto_now': 'True', 'blank': 'True'}),
            'height': ('django.db.models.fields.PositiveIntegerField', [], {'default': '0', 'null': 'True', 'blank': 'True'}),
            'id': ('django.db.models.fields.AutoField', [], {'primary_key': 'True'}),
            'image': ('django.db.models.fields.related.ForeignKey', [], {'blank': 'True', 'related_name': "'+'", 'null': 'True', 'to': "orm['cropduster.Image']"}),
            'name': ('django.db.models.fields.CharField', [], {'max_length': '255', 'db_index': 'True'}),
            'reference_thumb': ('django.db.models.fields.related.ForeignKey', [], {'blank': 'True', 'related_name': "'auto_set'", 'null': 'True', 'to': "orm['cropduster.Thumb']"}),
            'width': ('django.db.models.fields.PositiveIntegerField', [], {'default': '0', 'null': 'True', 'blank': 'True'})
        }
    }

    complete_apps = ['cropduster']
 67  
cropduster/south_migrations/0010_auto__chg_field_image_field_identifier.py
@@ -0,0 +1,67 @@
# encoding: utf-8
import datetime
from south.db import db
from south.v2 import SchemaMigration
from django.db import models

class Migration(SchemaMigration):

    def forwards(self, orm):

        # Changing field 'Image.field_identifier'
        db.alter_column('cropduster4_image', 'field_identifier', self.gf('django.db.models.fields.SlugField')(max_length=50, blank=True))


    def backwards(self, orm):

        # Changing field 'Image.field_identifier'
        db.alter_column('cropduster4_image', 'field_identifier', self.gf('django.db.models.fields.SlugField')(blank=True, max_length=50, null=True))


    models = {
        'contenttypes.contenttype': {
            'Meta': {'unique_together': "(('app_label', 'model'),)", 'object_name': 'ContentType', 'db_table': "'django_content_type'"},
            'app_label': ('django.db.models.fields.CharField', [], {'max_length': '100'}),
            'id': ('django.db.models.fields.AutoField', [], {'primary_key': 'True'}),
            'model': ('django.db.models.fields.CharField', [], {'max_length': '100'}),
            'name': ('django.db.models.fields.CharField', [], {'max_length': '100'})
        },
        'cropduster.image': {
            'Meta': {'unique_together': "(('content_type', 'object_id', 'field_identifier'),)", 'object_name': 'Image', 'db_table': "'cropduster4_image'"},
            'attribution': ('django.db.models.fields.CharField', [], {'max_length': '255', 'null': 'True', 'blank': 'True'}),
            'attribution_link': ('django.db.models.fields.URLField', [], {'max_length': '255', 'null': 'True', 'blank': 'True'}),
            'caption': ('django.db.models.fields.TextField', [], {'null': 'True', 'blank': 'True'}),
            'content_type': ('django.db.models.fields.related.ForeignKey', [], {'to': "orm['contenttypes.ContentType']"}),
            'date_created': ('django.db.models.fields.DateTimeField', [], {'auto_now_add': 'True', 'blank': 'True'}),
            'date_modified': ('django.db.models.fields.DateTimeField', [], {'auto_now': 'True', 'blank': 'True'}),
            'field_identifier': ('django.db.models.fields.SlugField', [], {'default': "''", 'max_length': '50', 'db_index': 'True', 'blank': 'True'}),
            'height': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'id': ('django.db.models.fields.AutoField', [], {'primary_key': 'True'}),
            'image': ('django.db.models.fields.files.ImageField', [], {'max_length': '100', 'db_column': "'path'", 'db_index': 'True'}),
            'object_id': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'prev_object_id': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'width': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'})
        },
        'cropduster.standaloneimage': {
            'Meta': {'object_name': 'StandaloneImage', 'db_table': "'cropduster4_standaloneimage'"},
            'id': ('django.db.models.fields.AutoField', [], {'primary_key': 'True'}),
            'image': ('cropduster.fields.CropDusterField', [], {'to': "orm['cropduster.Image']", 'max_length': '100', 'sizes': "[{'max_w': None, 'retina': 0, 'min_h': 1, 'name': 'crop', 'w': None, 'h': None, 'min_w': 1, '__type__': 'Size', 'max_h': None, 'label': u'Crop'}]"}),
            'md5': ('django.db.models.fields.CharField', [], {'max_length': '32'})
        },
        'cropduster.thumb': {
            'Meta': {'object_name': 'Thumb', 'db_table': "'cropduster4_thumb'"},
            'crop_h': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'crop_w': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'crop_x': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'crop_y': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'date_modified': ('django.db.models.fields.DateTimeField', [], {'auto_now': 'True', 'blank': 'True'}),
            'height': ('django.db.models.fields.PositiveIntegerField', [], {'default': '0', 'null': 'True', 'blank': 'True'}),
            'id': ('django.db.models.fields.AutoField', [], {'primary_key': 'True'}),
            'image': ('django.db.models.fields.related.ForeignKey', [], {'blank': 'True', 'related_name': "'+'", 'null': 'True', 'to': "orm['cropduster.Image']"}),
            'name': ('django.db.models.fields.CharField', [], {'max_length': '255', 'db_index': 'True'}),
            'reference_thumb': ('django.db.models.fields.related.ForeignKey', [], {'blank': 'True', 'related_name': "'auto_set'", 'null': 'True', 'to': "orm['cropduster.Thumb']"}),
            'width': ('django.db.models.fields.PositiveIntegerField', [], {'default': '0', 'null': 'True', 'blank': 'True'})
        }
    }

    complete_apps = ['cropduster']
 61  
cropduster/south_migrations/0011_update_model_freeze.py
@@ -0,0 +1,61 @@
# encoding: utf-8
import datetime
from south.db import db
from south.v2 import SchemaMigration
from django.db import models

class Migration(SchemaMigration):

    def forwards(self, orm):
        pass

    def backwards(self, orm):
        pass

    models = {
        'contenttypes.contenttype': {
            'Meta': {'unique_together': "(('app_label', 'model'),)", 'object_name': 'ContentType', 'db_table': "'django_content_type'"},
            'app_label': ('django.db.models.fields.CharField', [], {'max_length': '100'}),
            'id': ('django.db.models.fields.AutoField', [], {'primary_key': 'True'}),
            'model': ('django.db.models.fields.CharField', [], {'max_length': '100'}),
            'name': ('django.db.models.fields.CharField', [], {'max_length': '100'})
        },
        'cropduster.image': {
            'Meta': {'unique_together': "(('content_type', 'object_id', 'field_identifier'),)", 'object_name': 'Image', 'db_table': "'cropduster4_image'"},
            'attribution': ('django.db.models.fields.CharField', [], {'max_length': '255', 'null': 'True', 'blank': 'True'}),
            'attribution_link': ('django.db.models.fields.URLField', [], {'max_length': '255', 'null': 'True', 'blank': 'True'}),
            'caption': ('django.db.models.fields.TextField', [], {'null': 'True', 'blank': 'True'}),
            'content_type': ('django.db.models.fields.related.ForeignKey', [], {'to': "orm['contenttypes.ContentType']"}),
            'date_created': ('django.db.models.fields.DateTimeField', [], {'auto_now_add': 'True', 'blank': 'True'}),
            'date_modified': ('django.db.models.fields.DateTimeField', [], {'auto_now': 'True', 'blank': 'True'}),
            'field_identifier': ('django.db.models.fields.SlugField', [], {'default': "''", 'max_length': '50', 'db_index': 'True', 'blank': 'True'}),
            'height': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'id': ('django.db.models.fields.AutoField', [], {'primary_key': 'True'}),
            'image': ('cropduster.fields.CropDusterSimpleImageField', [], {'max_length': '100', 'db_column': "'path'", 'db_index': 'True'}),
            'object_id': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'prev_object_id': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'width': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'})
        },
        'cropduster.standaloneimage': {
            'Meta': {'object_name': 'StandaloneImage', 'db_table': "'cropduster4_standaloneimage'"},
            'id': ('django.db.models.fields.AutoField', [], {'primary_key': 'True'}),
            'image': ('cropduster.fields.CropDusterField', [], {'to': "orm['cropduster.Image']", 'max_length': '100', 'sizes': "[{'min_w': 1, 'retina': 0, 'name': 'crop', 'h': None, 'required': True, '__type__': 'Size', 'max_h': None, 'label': u'Crop', 'max_w': None, 'min_h': 1, 'w': None}]"}),
            'md5': ('django.db.models.fields.CharField', [], {'max_length': '32'})
        },
        'cropduster.thumb': {
            'Meta': {'object_name': 'Thumb', 'db_table': "'cropduster4_thumb'"},
            'crop_h': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'crop_w': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'crop_x': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'crop_y': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'date_modified': ('django.db.models.fields.DateTimeField', [], {'auto_now': 'True', 'blank': 'True'}),
            'height': ('django.db.models.fields.PositiveIntegerField', [], {'default': '0', 'null': 'True', 'blank': 'True'}),
            'id': ('django.db.models.fields.AutoField', [], {'primary_key': 'True'}),
            'image': ('django.db.models.fields.related.ForeignKey', [], {'blank': 'True', 'related_name': "'+'", 'null': 'True', 'to': "orm['cropduster.Image']"}),
            'name': ('django.db.models.fields.CharField', [], {'max_length': '255', 'db_index': 'True'}),
            'reference_thumb': ('django.db.models.fields.related.ForeignKey', [], {'blank': 'True', 'related_name': "'auto_set'", 'null': 'True', 'to': "orm['cropduster.Thumb']"}),
            'width': ('django.db.models.fields.PositiveIntegerField', [], {'default': '0', 'null': 'True', 'blank': 'True'})
        }
    }

    complete_apps = ['cropduster']
 0  
cropduster3/templatetags/__init__.py ??? cropduster/south_migrations/__init__.py
File renamed without changes.
  104  
cropduster/standalone/metadata.py
@@ -2,13 +2,17 @@
import re	import re
import ctypes	import ctypes
import PIL.Image	import PIL.Image
import tempfile
from io import open


from django.core.exceptions import ImproperlyConfigured	from django.core.exceptions import ImproperlyConfigured
from django.core.files.storage import default_storage
from django.utils.encoding import force_bytes
from django.utils import six


from cropduster.files import ImageFile	from cropduster.files import ImageFile
from cropduster.utils import json	from cropduster.utils import json



try:	try:
    import libxmp	    import libxmp
except ImportError:	except ImportError:
@@ -28,9 +32,16 @@


if not libxmp:	if not libxmp:
    check_file_format = get_format_info = None	    check_file_format = get_format_info = None

    def file_to_dict(f):
        return {}
else:	else:
    check_file_format = libxmp._exempi.xmp_files_check_file_format	    try:
    get_format_info = libxmp._exempi.xmp_files_get_format_info	        exempi = libxmp._exempi
    except AttributeError:
        exempi = libxmp.exempi.EXEMPI
    check_file_format = exempi.xmp_files_check_file_format
    get_format_info = exempi.xmp_files_get_format_info


    if not check_file_format.argtypes:	    if not check_file_format.argtypes:
        check_file_format.argtypes = [ctypes.c_char_p]	        check_file_format.argtypes = [ctypes.c_char_p]
@@ -42,14 +53,19 @@
    if not get_format_info.restype:	    if not get_format_info.restype:
        get_format_info.restype = ctypes.c_bool	        get_format_info.restype = ctypes.c_bool


    try:
        from libxmp.utils import file_to_dict
    except ImportError:
        from libxmp import file_to_dict



class EnumerationMeta(type):	class EnumerationMeta(type):


    def __new__(cls, name, bases, attrs):	    def __new__(cls, name, bases, attrs):
        if '_lookup' not in attrs:	        if '_lookup' not in attrs:
            lookup = {}	            lookup = {}
            for k, v in attrs.iteritems():	            for k, v in six.iteritems(attrs):
                if isinstance(v, (int, long)):	                if isinstance(v, six.integer_types):
                    lookup.setdefault(v, k)	                    lookup.setdefault(v, k)
            attrs['_lookup'] = lookup	            attrs['_lookup'] = lookup


@@ -59,8 +75,8 @@ def __contains__(self, value):
        return value in self._lookup	        return value in self._lookup




@six.add_metaclass(EnumerationMeta)
class Enumeration(object):	class Enumeration(object):
    __metaclass__ = EnumerationMeta	
    @classmethod	    @classmethod
    def value_name(cls, value):	    def value_name(cls, value):
        return cls._lookup.get(value)	        return cls._lookup.get(value)
@@ -135,7 +151,7 @@ def file_format_supported(file_path):
        raise IOError("File %s could not be found" % file_path)	        raise IOError("File %s could not be found" % file_path)
    if not check_file_format:	    if not check_file_format:
        return False	        return False
    file_format = check_file_format(os.path.abspath(file_path))	    file_format = check_file_format(force_bytes(os.path.abspath(file_path)))
    format_options = ctypes.c_int()	    format_options = ctypes.c_int()
    if file_format != FileFormats.XMP_FT_UNKNOWN:	    if file_format != FileFormats.XMP_FT_UNKNOWN:
        format_options = get_format_info(	        format_options = get_format_info(
@@ -164,9 +180,22 @@ class MetadataDict(dict):
    """	    """


    def __init__(self, file_path):	    def __init__(self, file_path):
        self.file_path = file_path	        try:
        ns_dict = libxmp.file_to_dict(file_path)	            # Don't use temporary files if we're using FileSystemStorage
        for ns, values in ns_dict.iteritems():	            with open(default_storage.path(file_path), mode='rb') as f:
                self.file_path = f.name
        except:
            self.tmp_file = tempfile.NamedTemporaryFile()
            with default_storage.open(file_path) as f:
                self.tmp_file.write(f.read())
                self.tmp_file.flush()
                self.tmp_file.seek(0)
            self.file_path = self.tmp_file.name
        ns_dict = file_to_dict(self.file_path)
        self.clean(ns_dict)

    def clean(self, ns_dict):
        for ns, values in six.iteritems(ns_dict):
            for k, v, opts in values:	            for k, v, opts in values:
                current = self	                current = self
                bits = k.split('/')	                bits = k.split('/')
@@ -203,17 +232,19 @@ def __init__(self, file_path):
                        v = float(v)	                        v = float(v)
                    except (TypeError, ValueError):	                    except (TypeError, ValueError):
                        v = None	                        v = None
                elif k == 'DerivedFrom' and isinstance(v, basestring):	                elif k == 'DerivedFrom' and isinstance(v, six.string_types):
                    v = re.sub(r'^xmp\.did:', '', v).lower()	                    v = re.sub(r'^xmp\.did:', '', v).lower()
                elif ns_prefix == 'crop' and k == 'json':	                elif ns_prefix == 'crop' and k == 'json':
                    v = json.loads(v)	                    v = json.loads(v)
                elif ns_prefix == 'crop' and k == 'md5':
                    v = v.lower()


                m = re.search(r'^(.*)\[(\d+)\](?=\/|\Z)', k)	                m = re.search(r'^(.*)\[(\d+)\](?=\/|\Z)', k)
                if m:	                if m:
                    current = current.setdefault(m.group(1), [{}])	                    current = current.setdefault(m.group(1), [{}])
                    k = int(m.group(2)) - 1	                    k = int(m.group(2)) - 1


                if isinstance(current, list) and isinstance(k, int):	                if isinstance(current, list) and isinstance(k, six.integer_types):
                    if len(current) <= k:	                    if len(current) <= k:
                        current.append(*([{}] * (1 + k - len(current))))	                        current.append(*([{}] * (1 + k - len(current))))


@@ -284,4 +315,51 @@ class MetadataImageFile(ImageFile):
    def __init__(self, *args, **kwargs):	    def __init__(self, *args, **kwargs):
        super(MetadataImageFile, self).__init__(*args, **kwargs)	        super(MetadataImageFile, self).__init__(*args, **kwargs)
        if self:	        if self:
            self.metadata = MetadataDict(self.path)	            self.metadata = MetadataDict(self.name)


def get_xmp_from_file(file_path):
    return libxmp.XMPFiles(file_path=file_path).get_xmp()


def get_xmp_from_bytes(img_bytes):
    tmp = tempfile.NamedTemporaryFile(delete=False)
    tmp.write(img_bytes)
    tmp.close()
    try:
        return get_xmp_from_file(tmp.name)
    finally:
        os.unlink(tmp.name)


def get_xmp_from_storage(file_path, storage=default_storage):
    with storage.open(file_path, mode='rb') as f:
        return get_xmp_from_bytes(f.read())


def put_xmp_to_file(xmp_meta, file_path):
    xmp_file = libxmp.XMPFiles(file_path=file_path, open_forupdate=True)

    if not xmp_file.can_put_xmp(xmp_meta):
        if not file_format_supported(file_path):
            raise Exception("Image format of %s does not allow metadata" % (file_path))
        else:
            raise Exception("Could not add metadata to image %s" % (file_path))

    xmp_file.put_xmp(xmp_meta)
    xmp_file.close_file()


def put_xmp_to_storage(xmp_meta, file_path, storage=default_storage):
    tmp = tempfile.NamedTemporaryFile(delete=False)
    try:
        with default_storage.open(file_path, mode='rb') as f:
            tmp.write(f.read())
        tmp.close()
        put_xmp_to_file(xmp_meta, tmp.name)
        with open(tmp.name, mode='rb') as f:
            data = f.read()
        with storage.open(file_path, mode='wb') as f:
            f.write(data)
    finally:
        os.unlink(tmp.name)
  16  
cropduster/standalone/models.py
@@ -5,11 +5,12 @@
from django.core.files.uploadedfile import SimpleUploadedFile	from django.core.files.uploadedfile import SimpleUploadedFile
from django.db import models	from django.db import models


from generic_plus.utils import get_relative_media_url

from cropduster import settings as cropduster_settings	from cropduster import settings as cropduster_settings
from cropduster.fields import CropDusterField	from cropduster.fields import CropDusterField
from cropduster.files import VirtualFieldFile	from cropduster.files import VirtualFieldFile
from cropduster.resizing import Size	from cropduster.resizing import Size
from cropduster.utils import get_relative_media_url	




class StandaloneImageManager(models.Manager):	class StandaloneImageManager(models.Manager):
@@ -42,28 +43,29 @@ def get_from_file(self, file_path, upload_to=None, preview_w=None, preview_h=Non
        cropduster_image, created = Image.objects.get_or_create(	        cropduster_image, created = Image.objects.get_or_create(
            content_type=ContentType.objects.get_for_model(StandaloneImage),	            content_type=ContentType.objects.get_for_model(StandaloneImage),
            object_id=standalone.pk)	            object_id=standalone.pk)
        standalone.image.related_object = cropduster_image
        cropduster_image.image = file_path	        cropduster_image.image = file_path
        cropduster_image.save()	        cropduster_image.save()
        cropduster_image.save_preview(preview_w, preview_h)	        cropduster_image.save_preview(preview_w, preview_h)
        standalone.image.cropduster_image = cropduster_image	
        return standalone	        return standalone




class StandaloneImage(models.Model):	class StandaloneImage(models.Model):


    objects = StandaloneImageManager()	    objects = StandaloneImageManager()


    md5 = models.CharField(max_length=32)	    md5 = models.CharField(max_length=32, blank=True, default='')
    image = CropDusterField(sizes=[Size("crop")])	    image = CropDusterField(sizes=[Size("crop")], upload_to='')


    class Meta:	    class Meta:
        app_label = cropduster_settings.CROPDUSTER_APP_LABEL	        app_label = cropduster_settings.CROPDUSTER_APP_LABEL
        db_table = '%s_standaloneimage' % cropduster_settings.CROPDUSTER_DB_PREFIX	        db_table = '%s_standaloneimage' % cropduster_settings.CROPDUSTER_DB_PREFIX


    def save(self, **kwargs):	    def save(self, **kwargs):
        if not self.md5:	        if not self.md5 and self.image:
            md5_hash = hashlib.md5()	            md5_hash = hashlib.md5()
            with open(self.image.path) as f:	            with self.image.related_object.image as f:
                f.open()
                md5_hash.update(f.read())	                md5_hash.update(f.read())
            self.md5 = md5_hash.digest()	            self.md5 = md5_hash.hexdigest()
        super(StandaloneImage, self).save(**kwargs)	        super(StandaloneImage, self).save(**kwargs)
  135  
cropduster/standalone/static/ckeditor/ckeditor/plugins/cropduster/dialogs/cropduster.js
@@ -344,7 +344,10 @@ CKEDITOR.dialog.add('cropduster', function (editor) {


    var okButton = CKEDITOR.dialog.okButton.override({	    var okButton = CKEDITOR.dialog.okButton.override({
        onClick: function(evt) {	        onClick: function(evt) {
            var $j = cropdusterIframe.$.contentWindow.$;	            var contentWin = cropdusterIframe.iframeElement.$.contentWindow;
            var $j = (typeof contentWin.django === 'object')
              ? contentWin.django.jQuery
              : contentWin.$;
            if ($j) {	            if ($j) {
                var $cropButton = $j('#crop-button');	                var $cropButton = $j('#crop-button');
                if ($j.length && !$cropButton.hasClass('disabled')) {	                if ($j.length && !$cropButton.hasClass('disabled')) {
@@ -362,9 +365,10 @@ CKEDITOR.dialog.add('cropduster', function (editor) {
    var tabElements = [{	    var tabElements = [{
        id: 'iframe',	        id: 'iframe',
        type: 'html',	        type: 'html',
        html: '<div style="width:100%;text-align:center;">' + '<iframe style="border:0;width:650px;height:500px;font-size:20px" scrolling="no" frameborder="0" allowTransparency="true"></iframe>' + '</div>',	        html: '<div style="width:100%;text-align:center;">' + '<iframe style="border:0;width:650px;height:400px;font-size:20px" scrolling="no" frameborder="0" allowTransparency="true"></iframe>' + '</div>',
        onLoad: function (widget) {},	        onLoad: function (widget) {},
        setup: function (widget) {	        setup: function (widget) {

            var dialogElement = this.getDialog().getElement();	            var dialogElement = this.getDialog().getElement();
            dialogElement.addClass('cke_editor_cropduster_content_dialog');	            dialogElement.addClass('cke_editor_cropduster_content_dialog');
            var tabs = dialogElement.findOne('.cke_dialog_tabs');	            var tabs = dialogElement.findOne('.cke_dialog_tabs');
@@ -375,39 +379,55 @@ CKEDITOR.dialog.add('cropduster', function (editor) {
            if (contents) {	            if (contents) {
                contents.setStyles({'border-top': '0', 'margin-top': '0'});	                contents.setStyles({'border-top': '0', 'margin-top': '0'});
            }	            }
            var domId = this.domId.replace(/_uiElement$/, '');	
            var callback_fn = domId + '_callback';	            cropdusterIframe = {
            var image = widget.parts.image;	                setup: function (domId, baseUrl) {
            var url = widget.config.url + '?';	                    this.iframeElement = CKEDITOR.document.getById(domId).getChild(0)
            var params = {	                    this.iframeElement.$.src = 'about:blank';
                'callback_fn': callback_fn	                    try {
            };	                        this.iframeElement.$.contentDocument.body.innerHTML = "";
            if (widget.config.uploadTo) {	                    } catch(e) {}
                params['upload_to'] = widget.config.uploadTo;	                    this.baseUrl = baseUrl;
            }	                    this.callback_fn = domId.replace(/_uiElement$/, '') + '_callback';
            if (widget.config.previewSize) {	
                if (Object.prototype.toString.call(widget.config.previewSize) == '[object Array]') {	                    var image = widget.parts.image;
                    if (widget.config.previewSize.length == 2) {	                    var params = {'callback_fn': this.callback_fn};
                        params['preview_size'] = widget.config.previewSize.join('x');	                    if (widget.config.uploadTo) {
                        params['upload_to'] = widget.config.uploadTo;
                    }
                    if (widget.config.previewSize) {
                        if (Object.prototype.toString.call(widget.config.previewSize) == '[object Array]') {
                            if (widget.config.previewSize.length == 2) {
                                params['preview_size'] = widget.config.previewSize.join('x');
                            }
                        }
                    }
                    if (image.$.naturalWidth != image.$.width) {
                        params['max_w'] = image.$.width;
                    }
                    if (widget.data && widget.data.src) {
                        params['image'] = widget.data.src;
                    }
                    if (widget.config.urlParams && isPlainObject(widget.config.urlParams)) {
                        params = CKEDITOR.tools.extend({}, params, widget.config.urlParams);
                    }	                    }
                    this.params = params;
                    this.reload();
                },
                getUrl: function () {
                    var urlQuery = [];
                    for (var k in this.params) {
                        urlQuery.push([k, encodeURIComponent(this.params[k])].join('='));
                    }
                    return this.baseUrl + urlQuery.join('&');
                },
                reload: function () {
                    var url = this.getUrl();
                    this.iframeElement.$.src = url;
                }	                }
            }	            }
            if (image.$.naturalWidth != image.$.width) {	            cropdusterIframe.setup(this.domId, widget.config.url + '?');
                params['max_w'] = image.$.width;	            widget.cropdusterIframe = cropdusterIframe;
            }	
            if (widget.data && widget.data.src) {	
                params['image'] = widget.data.src;	
            }	
            if (widget.config.urlParams && isPlainObject(widget.config.urlParams)) {	
                params = CKEDITOR.tools.extend({}, params, widget.config.urlParams);	
            }	
            var url_query = [];	
            for (var k in params) {	
                url_query.push([k, encodeURIComponent(params[k])].join('='));	
            }	
            url += url_query.join('&');	
            cropdusterIframe = CKEDITOR.document.getById(this.domId).getChild(0);	
            cropdusterIframe.$.src = url;	


            var self = this;	            var self = this;
            var callback = function (prefix, data) {	            var callback = function (prefix, data) {
@@ -418,14 +438,14 @@ CKEDITOR.dialog.add('cropduster', function (editor) {
                    heightField.setValue(thumbData.height);	                    heightField.setValue(thumbData.height);
                    widget.setData('height', thumbData.height);	                    widget.setData('height', thumbData.height);
                    srcField.setValue(thumbData.url);	                    srcField.setValue(thumbData.url);
                    updateValue(url);	                    updateValue(cropdusterIframe.getUrl());
                }	                }
                var dialog = self.getDialog();	                var dialog = self.getDialog();
                if (dialog.fire('ok', {hide: true}).hide !== false) {	                if (dialog.fire('ok', {hide: true}).hide !== false) {
                    dialog.hide();	                    dialog.hide();
                }	                }
            };	            };
            window[callback_fn] = callback;	            window[cropdusterIframe.callback_fn] = callback;
        }	        }
    }, {	    }, {
        id: 'hasCaption',	        id: 'hasCaption',
@@ -461,6 +481,24 @@ CKEDITOR.dialog.add('cropduster', function (editor) {
        }	        }
    }	    }


    tabElements.push({
        id: 'alt',
        type: 'text',
        label: lang.alt,
        setup: function (widget) {
            this.setValue(widget.data.alt);
        },
        commit: function (widget) {
            widget.setData('alt', this.getValue());
        },
        validate: function () {
            if (editor.config.cropduster_requireAltText) {
                var value = this.getValue();
                return CKEDITOR.dialog.validate.notEmpty('Alt text describing the image is required for this field.')(value);
            }
        }
    });

    return {	    return {
        title: lang.title,	        title: lang.title,
        minWidth: 650,	        minWidth: 650,
@@ -474,7 +512,7 @@ CKEDITOR.dialog.add('cropduster', function (editor) {
        },	        },
        onShow: function () {	        onShow: function () {
            // Create a "global" reference to edited widget.	            // Create a "global" reference to edited widget.
            widget = this._.widget;	            widget = this.widget;
            // Create a "global" reference to widget's image.	            // Create a "global" reference to widget's image.
            image = widget.parts.image;	            image = widget.parts.image;
            // Reset global variables.	            // Reset global variables.
@@ -492,6 +530,19 @@ CKEDITOR.dialog.add('cropduster', function (editor) {
                toggleLockDimensions('check');	                toggleLockDimensions('check');
            });	            });
        },	        },
        onOk: function(evt) {
            var retval = CKEDITOR.dialog.validate.notEmpty(lang.urlMissing).call(this._.contents.info.src),
                invalid = typeof(retval) == 'string' || retval === false;
            if (invalid) {
                evt.data.hide = false;
                evt.stop();
                if (this.fire('cancel', {hide: true}).hide !== false) {
                    this.hide();
                }
                return false;
            }
            return true;
        },
        contents: [{	        contents: [{
            id: 'tab-basic',	            id: 'tab-basic',
            label: 'Basic',	            label: 'Basic',
@@ -516,16 +567,8 @@ CKEDITOR.dialog.add('cropduster', function (editor) {
                commit: function (widget) {	                commit: function (widget) {
                    widget.setData('src', this.getValue());	                    widget.setData('src', this.getValue());
                },	                },
                validate: CKEDITOR.dialog.validate.notEmpty(lang.urlMissing)	                validate: function() {
            }, {	                    return true;
                id: 'alt',	
                type: 'text',	
                label: lang.alt,	
                setup: function (widget) {	
                    this.setValue(widget.data.alt);	
                },	
                commit: function (widget) {	
                    widget.setData('alt', this.getValue());	
                }	                }
            }, {	            }, {
                type: 'hbox',	                type: 'hbox',
@@ -573,4 +616,4 @@ CKEDITOR.dialog.add('cropduster', function (editor) {
            }]	            }]
        }]	        }]
    };	    };
});	});
 BIN -359 Bytes (50%) 
...ter/standalone/static/ckeditor/ckeditor/plugins/cropduster/icons/cropduster.png

 BIN -719 Bytes 
...andalone/static/ckeditor/ckeditor/plugins/cropduster/icons/hidpi/cropduster.png
Binary file not shown.
  31  
cropduster/standalone/static/ckeditor/ckeditor/plugins/cropduster/plugin.js
@@ -71,11 +71,16 @@


            // Add toolbar button for this plugin.	            // Add toolbar button for this plugin.
            editor.ui.addButton && editor.ui.addButton('cropduster', {	            editor.ui.addButton && editor.ui.addButton('cropduster', {
                label: editor.lang.common.image,	                label: 'CropDuster Image',
                command: 'cropduster',	                command: 'cropduster',
                toolbar: 'insert,10'	                toolbar: 'insert,10'
            });	            });


            if (typeof editor.ui.items.Image == 'object') {
                editor.ui.items.Image.label = "Legacy Image Upload";
                editor.ui.items.Image.args[0].label = "Legacy Image Upload";
            }

            // Register context menu option for editing widget.	            // Register context menu option for editing widget.
            if (editor.contextMenu) {	            if (editor.contextMenu) {
                editor.addMenuGroup('cropduster', 10);	                editor.addMenuGroup('cropduster', 10);
@@ -278,6 +283,11 @@
            this.on('contextMenu', function(evt) {	            this.on('contextMenu', function(evt) {
                evt.data.cropduster = CKEDITOR.TRISTATE_OFF;	                evt.data.cropduster = CKEDITOR.TRISTATE_OFF;
            });	            });

            // Pass the reference to this widget to the dialog.
            this.on( 'dialog', function(evt) {
                evt.data.widget = this;
            }, this);
        },	        },


        upcast: upcastWidgetElement,	        upcast: upcastWidgetElement,
@@ -484,6 +494,7 @@
        // The other case is:	        // The other case is:
        //         <p style="text-align:center"><img></p>.	        //         <p style="text-align:center"><img></p>.
        // Then <p> takes charge of <figure> and nothing is to be changed.	        // Then <p> takes charge of <figure> and nothing is to be changed.
        image = el.getFirst('img') || (el.getFirst('a') ? el.getFirst('a').getFirst('img') : null);
        if (isCenterWrapper(el)) {	        if (isCenterWrapper(el)) {
            if (name == 'div') {	            if (name == 'div') {
                var figure = el.getFirst('figure');	                var figure = el.getFirst('figure');
@@ -492,11 +503,6 @@
            }	            }


            data.align = 'center';	            data.align = 'center';
            image = el.getFirst('img');	
        // No center wrapper has been found.	
        } else if (name == 'figure' && el.getFirst('img')) {	
            image = el.getFirst('img');	
        // Inline widget from plain img.	
        } else if (name == 'img') {	        } else if (name == 'img') {
            image = el;	            image = el;
        }	        }
@@ -577,7 +583,7 @@


        // The only child of centering wrapper can be <figure> with	        // The only child of centering wrapper can be <figure> with
        // class="caption" or plain <img>.	        // class="caption" or plain <img>.
        if (childName != 'img' && !(childName == 'figure' && child.getFirst('img'))) {	        if (childName != 'img' && !(childName == 'figure' && (child.getFirst('img') || child.getFirst('a')))) {
            return false;	            return false;
        }	        }


@@ -623,18 +629,19 @@


        // Inline widgets don't need a resizer wrapper as an image spans the entire widget.	        // Inline widgets don't need a resizer wrapper as an image spans the entire widget.
        if (!widget.inline) {	        if (!widget.inline) {
            var oldResizeWrapper = widget.element.getFirst(),	            var oldResizeWrapper = widget.element.findOne('span'),
                resizeWrapper = doc.createElement('span');	                resizeWrapper = doc.createElement('span');


            resizeWrapper.addClass('cke_cropduster_resizer_wrapper');	            resizeWrapper.addClass('cke_cropduster_resizer_wrapper');
            resizeWrapper.append(widget.parts.image);	            resizeWrapper.append(widget.parts.image.clone());
            resizeWrapper.replace(widget.parts.image);
            resizeWrapper.append(resizer);	            resizeWrapper.append(resizer);
            widget.element.append(resizeWrapper, true);	            widget.parts.image = resizeWrapper.findOne('img');


            // Remove the old wrapper which could came from e.g. pasted HTML	            // Remove the old wrapper which could came from e.g. pasted HTML
            // and which could be corrupted (e.g. resizer span has been lost).	            // and which could be corrupted (e.g. resizer span has been lost).
            if (oldResizeWrapper.is('span')) {	            if (oldResizeWrapper) {
                oldResizeWrapper.remove();	                resizeWrapper.replace(oldResizeWrapper);
            }	            }
        } else {	        } else {
            widget.wrapper.append(resizer);	            widget.wrapper.append(resizer);
  7  
cropduster/standalone/views.py
@@ -24,13 +24,14 @@ def image_file(self):
    def db_image(self):	    def db_image(self):
        if not self.image_file:	        if not self.image_file:
            return None	            return None
        md5 = self.image_file.metadata.get('md5') or self.image_file.metadata.get('DerivedFrom')
        try:	        try:
            standalone = StandaloneImage.objects.get(md5=self.image_file.metadata.get('DerivedFrom'))	            standalone = StandaloneImage.objects.get(md5=md5)
        except StandaloneImage.DoesNotExist:	        except StandaloneImage.DoesNotExist:
            (preview_w, preview_h) = self.preview_size	            (preview_w, preview_h) = self.preview_size
            standalone = StandaloneImage.objects.get_from_file(self.image_file.name,	            standalone = StandaloneImage.objects.get_from_file(self.image_file.name,
                upload_to=self.upload_to, preview_w=preview_w, preview_h=preview_h)	                upload_to=self.upload_to, preview_w=preview_w, preview_h=preview_h)
        db_image = standalone.image.cropduster_image	        db_image = standalone.image.related_object
        if not getattr(db_image, 'pk', None):	        if not getattr(db_image, 'pk', None):
            raise Exception("Image does not exist in database")	            raise Exception("Image does not exist in database")
        if not db_image.image and standalone.image.name:	        if not db_image.image and standalone.image.name:
@@ -56,6 +57,8 @@ def sizes(self):
        size = getattr(self.image_file.metadata, 'crop_size', None)	        size = getattr(self.image_file.metadata, 'crop_size', None)
        if not size:	        if not size:
            size = Size('crop', max_w=self.max_w)	            size = Size('crop', max_w=self.max_w)
        else:
            size.max_w = self.max_w
        return [size]	        return [size]


    @cached_property	    @cached_property
  291  
cropduster/static/cropduster/css/cropduster.css
@@ -1,16 +1,58 @@
.cropduster-form .grp-module {
    background: transparent;
}

.cropduster-form .image,
.cropduster-form .thumbs,
.cropduster-form .DELETE,
.cropduster-form .field_identifier,
.cropduster-form .field-image,
.cropduster-form .field-thumbs,
.cropduster-form .field-field_identifier,
.cropduster-form .inline-related .grp-collapse-handler {
    display: none;
}
.cropduster-form .inline-related,
.cropduster-form .inline-related .grp-module,
.cropduster-form .inline-related .grp-row,
.cropduster-form .inline-related .form-row {
    border: 0 !important;
}

.cropduster-form .inline-related .grp-module,
.cropduster-form .inline-related .module {
    clear: both;
}

.cropduster-form .inline-related .grp-row input {
    width: 588px;
}
.cropduster-form {	.cropduster-form {
    border: 0 !important;	    border: 0 !important;
}	}


.cropduster-form fieldset {	body.cropduster-debug .cropduster-form .image,
    display: none;	body.cropduster-debug .cropduster-form .thumbs,
body.cropduster-debug .cropduster-form .field-image,
body.cropduster-debug .cropduster-form .field-thumbs,
body.cropduster-debug .cropduster-form .DELETE,
body.cropduster-debug .cropduster-form .inline-related .grp-collapse-handler {
    display: block !important;
}

.cropduster-customfield {
    display: block;
    float: left;
}	}


body.cropduster-debug .cropduster-form fieldset {	.cropduster-form .delete {
    display: block;	    display: block;
    float: left;
    margin-left: 20px;
    margin-top: 5px;
}	}


.cropduster-customfield img{	.cropduster-customfield img {
    border: 0;	    border: 0;
}	}


@@ -20,23 +62,15 @@ body.cropduster-debug .cropduster-form fieldset {
}	}


/* buttons */	/* buttons */
.cropduster-upload-form .rounded-button,	.cropduster-upload-form .cropduster-button,
.cropduster-upload-form .rounded-button:visited,	.cropduster-upload-form .cropduster-button:visited,
.cropduster-upload-form .rounded-button:hover,	.cropduster-upload-form .cropduster-button:hover,
.cropduster-upload-form .rounded-button:active,	.cropduster-upload-form .cropduster-button:active {
.cropduster-upload-form input[type="submit"].rounded-button,	
.cropduster-upload-form input[type="submit"].rounded-button:visited,	
.cropduster-upload-form input[type="submit"].rounded-button:hover,	
.cropduster-upload-form input[type="submit"].rounded-button:active,	
.cropduster-upload-form input[type="button"].rounded-button,	
.cropduster-upload-form input[type="button"].rounded-button:visited,	
.cropduster-upload-form input[type="button"].rounded-button:hover,	
.cropduster-upload-form input[type="button"].rounded-button:active {	
	margin: 0;		margin: 0;
	display: inline-block; 		display: inline-block;
	padding: 6px 10px 7px 10px;		padding: 6px 10px 7px 10px;
	text-decoration: none;		text-decoration: none;
	-moz-border-radius: 6px; 		-moz-border-radius: 6px;
	-webkit-border-radius: 6px;		-webkit-border-radius: 6px;
	border-radius: 6px;		border-radius: 6px;
	border-bottom: 1px solid rgba(0,0,0,0.25);		border-bottom: 1px solid rgba(0,0,0,0.25);
@@ -62,16 +96,12 @@ body.cropduster-debug .cropduster-form fieldset {
	line-height: 1;		line-height: 1;
}	}


.cropduster-upload-form .rounded-button:hover,	.cropduster-upload-form .cropduster-button:hover {
.cropduster-upload-form input[type="submit"].rounded-button:hover,	
.cropduster-upload-form input[type="button"].rounded-button:hover {	
	background: -webkit-gradient(linear, 0% 0%, 0% 100%, from(#f4f4f4), to(#CACACA));		background: -webkit-gradient(linear, 0% 0%, 0% 100%, from(#f4f4f4), to(#CACACA));
	background: -moz-linear-gradient(top, #f4f4f4, #CACACA);		background: -moz-linear-gradient(top, #f4f4f4, #CACACA);
	background-color: #f4f4f4;		background-color: #f4f4f4;
}	}
.cropduster-upload-form .rounded-button:active,	.cropduster-upload-form .cropduster-button:active {
.cropduster-upload-form input[type="submit"].rounded-button:active,	
.cropduster-upload-form input[type="button"].rounded-button:active {	
	background: -webkit-gradient(linear, 0% 0%, 0% 100%, from(#D6D6D6), to(#f4f4f4));		background: -webkit-gradient(linear, 0% 0%, 0% 100%, from(#D6D6D6), to(#f4f4f4));
	background: -moz-linear-gradient(top, #D6D6D6, #f4f4f4);		background: -moz-linear-gradient(top, #D6D6D6, #f4f4f4);
	background-color: #D6D6D6;		background-color: #D6D6D6;
@@ -83,225 +113,52 @@ body.cropduster-debug .cropduster-form fieldset {
	text-shadow: rgba(255,255,255,0.5) 0 -1px 0;		text-shadow: rgba(255,255,255,0.5) 0 -1px 0;
}	}


.cropduster-upload-form .rounded-button.disabled,	.cropduster-upload-form .cropduster-button.disabled,
.cropduster-upload-form .rounded-button.disabled:hover,	.cropduster-upload-form .cropduster-button.disabled:hover,
.cropduster-upload-form .rounded-button.disabled:active,	.cropduster-upload-form .cropduster-button.disabled:active {
.cropduster-upload-form input[type="submit"].rounded-button.disabled,	
.cropduster-upload-form input[type="submit"].rounded-button.disabled:hover,	
.cropduster-upload-form input[type="submit"].rounded-button.disabled:active,	
.cropduster-upload-form input[type="button"].rounded-button.disabled,	
.cropduster-upload-form input[type="button"].rounded-button.disabled:hover,	
.cropduster-upload-form input[type="button"].rounded-button.disabled:active {	
	color: #888;		color: #888;
	cursor: default;		cursor: default;
	background: -webkit-gradient(linear, 0% 0%, 0% 100%, from(#ECECEC), to(#d1d1d1));		background: -webkit-gradient(linear, 0% 0%, 0% 100%, from(#ECECEC), to(#d1d1d1));
	background: -moz-linear-gradient(top, #ECECEC, #d1d1d1);		background: -moz-linear-gradient(top, #ECECEC, #d1d1d1);
	background-color: #ECECEC;		background-color: #ECECEC;
	border: 1px solid rgba(0, 0, 0, 0.36); /* #a3a3a3 */		border: 1px solid rgba(0, 0, 0, 0.36); /* #a3a3a3 */
	border-bottom: 1px solid rgba(0, 0, 0, 0.4); /* #9a9a9a */		border-bottom: 1px solid rgba(0, 0, 0, 0.4); /* #9a9a9a */
    outline: none;
}	}


.cropduster-upload-form .rounded-button.red,	.cropduster-upload-form .cropduster-button.small,
.cropduster-upload-form .rounded-button.red:visited,	.cropduster-upload-form .cropduster-button.small:visited,
.cropduster-upload-form .rounded-button.red:hover,	.cropduster-upload-form .cropduster-button.small:hover {
.cropduster-upload-form .rounded-button.red:active,	
.cropduster-upload-form input[type="submit"].rounded-button.red,	
.cropduster-upload-form input[type="submit"].rounded-button.red:visited,	
.cropduster-upload-form input[type="submit"].rounded-button.red:hover,	
.cropduster-upload-form input[type="submit"].rounded-button.red:active,	
.cropduster-upload-form input[type="button"].rounded-button.red,	
.cropduster-upload-form input[type="button"].rounded-button.red:visited,	
.cropduster-upload-form input[type="button"].rounded-button.red:hover,	
.cropduster-upload-form input[type="button"].rounded-button.red:active	
{	
	background: -webkit-gradient(linear, 0% 0%, 0% 100%, from(#b4463f), to(#731711));	
	background: -moz-linear-gradient(top, #b4463f, #731711);	
	background-color: #b4463f;	
	border: 1px solid #832922;	
	border-bottom: 1px solid #a43c34;	
	color: #fff;	
	-webkit-text-shadow: rgba(0,0,0,0.5) 0 -1px 0;	
	-moz-text-shadow: rgba(0,0,0,0.5) 0 -1px 0;	
	text-shadow: rgba(0,0,0,0.5) 0 -1px 0;	

}	
.cropduster-upload-form .rounded-button.red:hover,	
.cropduster-upload-form input[type="submit"].rounded-button.red:hover,	
.cropduster-upload-form input[type="button"].rounded-button.red:hover {	
	color: #fff;	
	background: -webkit-gradient(linear, 0% 0%, 0% 100%, from(#c2554e), to(#993129));	
	background: -moz-linear-gradient(top, #c2554e, #993129);	
	background-color: #c2554e;	
	border: 1px solid #ad4e47;	
	border-bottom: 1px solid #a0322a;	
}	
.cropduster-upload-form .rounded-button.red:active,	
.cropduster-upload-form input[type="submit"].rounded-button.red:active,	
.cropduster-upload-form input[type="button"].rounded-button.red:active {	
	background: -webkit-gradient(linear, 0% 0%, 0% 100%, from(#993129), to(#c2554e));	
	background: -moz-linear-gradient(top, #993129, #c2554e);	
	background-color: #993129;	
	border: 1px solid #a0322a;	
	border-bottom: 1px solid #ad4e47;	
}	


.cropduster-upload-form .rounded-button.small,	
.cropduster-upload-form .rounded-button.small:visited,	
.cropduster-upload-form .rounded-button.small:hover,	
.cropduster-upload-form input[type="submit"].rounded-button.small,	
.cropduster-upload-form input[type="submit"].rounded-button.small:visited,	
.cropduster-upload-form input[type="submit"].rounded-button.small:hover,	
.cropduster-upload-form input[type="button"].rounded-button.small,	
.cropduster-upload-form input[type="button"].rounded-button.small:visited,	
.cropduster-upload-form input[type="button"].rounded-button.small:hover {	
	padding: 3px 6px 4px 6px;		padding: 3px 6px 4px 6px;
	height: 23px;		height: 23px;
}	}


.cropduster-upload-form .rounded-button.small:active,	.cropduster-upload-form .cropduster-button.small:active {
.cropduster-upload-form input[type="submit"].rounded-button.small:active,	
.cropduster-upload-form input[type="button"].rounded-button.small:active {	
	padding: 4px 6px 3px 6px;		padding: 4px 6px 3px 6px;
	height: 23px;		height: 23px;
}	}


.cropduster-upload-form .rounded-button.green,	.cropduster-image-thumb {
.cropduster-upload-form .rounded-button.green:active,	
.cropduster-upload-form .rounded-button.green:hover,	
.cropduster-upload-form .rounded-button.green:visited,	
.cropduster-upload-form input[type="submit"].rounded-button.green,	
.cropduster-upload-form input[type="submit"].rounded-button.green:active,	
.cropduster-upload-form input[type="submit"].rounded-button.green:hover,	
.cropduster-upload-form input[type="submit"].rounded-button.green:visited,	
.cropduster-upload-form input[type="button"].rounded-button.green,	
.cropduster-upload-form input[type="button"].rounded-button.green:active,	
.cropduster-upload-form input[type="button"].rounded-button.green:hover,	
.cropduster-upload-form input[type="button"].rounded-button.green:visited {	
	color: #fff;	
	border: 0;	
	background: #3a4d00 url(../img/button-overlay.png) repeat-x 0 0;	
}	
.cropduster-upload-form .rounded-button.green:hover,	
.cropduster-upload-form input[type="submit"].rounded-button.green:hover,	
.cropduster-upload-form input[type="button"].rounded-button.green:hover	{	
	background-color: #749a02;	
}	

.cropduster-upload-form .rounded-button.blue,	
.cropduster-upload-form .rounded-button.blue:active,	
.cropduster-upload-form .rounded-button.blue:hover,	
.cropduster-upload-form .rounded-button.blue:visited,	
.cropduster-upload-form input[type="submit"].rounded-button.blue,	
.cropduster-upload-form input[type="submit"].rounded-button.blue:visited,	
.cropduster-upload-form input[type="submit"].rounded-button.blue:hover,	
.cropduster-upload-form input[type="submit"].rounded-button.blue:active,	
.cropduster-upload-form input[type="button"].rounded-button.blue,	
.cropduster-upload-form input[type="button"].rounded-button.blue:visited,	
.cropduster-upload-form input[type="button"].rounded-button.blue:hover,	
.cropduster-upload-form input[type="button"].rounded-button.blue:active {	
	color: #fff;	
	border: 0;	
	background: #162d3e url(../img/button-overlay.png) repeat-x 0 0;	
}	
.cropduster-upload-form .rounded-button.blue:hover,	
.cropduster-upload-form input[type="submit"].rounded-button.blue:hover,	
.cropduster-upload-form input[type="button"].rounded-button.blue:hover {	
	background-color: #224660;	
}	

.cropduster-upload-form .rounded-button.magenta,	
.cropduster-upload-form .rounded-button.magenta:active,	
.cropduster-upload-form .rounded-button.magenta:hover,	
.cropduster-upload-form .rounded-button.magenta:visited,	
.cropduster-upload-form input[type="submit"].rounded-button.magenta,	
.cropduster-upload-form input[type="submit"].rounded-button.magenta:visited,	
.cropduster-upload-form input[type="submit"].rounded-button.magenta:hover,	
.cropduster-upload-form input[type="submit"].rounded-button.magenta:active,	
.cropduster-upload-form input[type="button"].rounded-button.magenta,	
.cropduster-upload-form input[type="button"].rounded-button.magenta:visited,	
.cropduster-upload-form input[type="button"].rounded-button.magenta:hover,	
.cropduster-upload-form input[type="button"].rounded-button.magenta:active {	
	color: #fff;	
	border: 0;	
	background: #a9014b url(../img/button-overlay.png) repeat-x 0 0;	
}	
.cropduster-upload-form .rounded-button.magenta:hover,	
.cropduster-upload-form input[type="submit"].rounded-button.magenta:hover,	
.cropduster-upload-form input[type="button"].rounded-button.magenta:hover {	
	background-color: #630030;	
}	

.cropduster-upload-form .rounded-button.orange,	
.cropduster-upload-form .rounded-button.orange:active,	
.cropduster-upload-form .rounded-button.orange:hover,	
.cropduster-upload-form .rounded-button.orange:visited,	
.cropduster-upload-form input[type="submit"].rounded-button.orange,	
.cropduster-upload-form input[type="submit"].rounded-button.orange:visited,	
.cropduster-upload-form input[type="submit"].rounded-button.orange:hover,	
.cropduster-upload-form input[type="submit"].rounded-button.orange:active,	
.cropduster-upload-form input[type="button"].rounded-button.orange,	
.cropduster-upload-form input[type="button"].rounded-button.orange:visited,	
.cropduster-upload-form input[type="button"].rounded-button.orange:hover,	
.cropduster-upload-form input[type="button"].rounded-button.orange:active {	
	color: #fff;	
	border: 0;	
	background: #ff5c00 url(../img/button-overlay.png) repeat-x 0 0;	
}	
.cropduster-upload-form .rounded-button.orange:hover,	
.cropduster-upload-form input[type="submit"].rounded-button.orange:hover,	
.cropduster-upload-form input[type="button"].rounded-button.orange:hover {	
	background-color: #d45500;	
}	

.cropduster-upload-form .rounded-button.yellow,	
.cropduster-upload-form .rounded-button.yellow:active,	
.cropduster-upload-form .rounded-button.yellow:hover,	
.cropduster-upload-form .rounded-button.yellow:visited,	
.cropduster-upload-form input[type="submit"].rounded-button.yellow,	
.cropduster-upload-form input[type="submit"].rounded-button.yellow:visited,	
.cropduster-upload-form input[type="submit"].rounded-button.yellow:hover,	
.cropduster-upload-form input[type="submit"].rounded-button.yellow:active,	
.cropduster-upload-form input[type="button"].rounded-button.yellow,	
.cropduster-upload-form input[type="button"].rounded-button.yellow:visited,	
.cropduster-upload-form input[type="button"].rounded-button.yellow:hover,	
.cropduster-upload-form input[type="button"].rounded-button.yellow:active {	
	color: #fff;	
	border: 0;	
	background: #ffb515 url(../img/button-overlay.png) repeat-x 0 0;	
}	
.cropduster-upload-form .rounded-button.yellow:hover,	
.cropduster-upload-form input[type="submit"].rounded-button.yellow:hover,	
.cropduster-upload-form input[type="button"].rounded-button.yellow:hover {	
	background-color: #fc9200;	
}	

table.striped tfoot .rounded-button,	
table.striped tfoot .rounded-button:active,	
table.striped tfoot .rounded-button:hover,	
table.striped tfoot .rounded-button:visited {	
	padding: 4px 6px 5px;	
}	
table.striped tfoot .rounded-button:active {	
	padding: 5px 6px 4px;	
}	

.cropduster-image span {	
    background-repeat: none;	
    background-position: 0 0;	
    background-size: 100%;	
}	
.cropduster-image span {	
    display: block;	    display: block;
    float: left;	
    -webkit-box-shadow: 0px 1px 4px rgba(0, 0, 0, 0.8);	    -webkit-box-shadow: 0px 1px 4px rgba(0, 0, 0, 0.8);
       -moz-box-shadow: 0px 1px 4px rgba(0, 0, 0, 0.8);	       -moz-box-shadow: 0px 1px 4px rgba(0, 0, 0, 0.8);
            box-shadow: 0px 1px 4px rgba(0, 0, 0, 0.8);	            box-shadow: 0px 1px 4px rgba(0, 0, 0, 0.8);
}	}


.cropduster-form .cropduster-images.thumbs {
    display: block;
}
.cropduster-images .cropduster-image {	.cropduster-images .cropduster-image {
    display: none;	    display: none;
}	}
.cropduster-images .cropduster-image:first-child {	.cropduster-images .cropduster-image:first-child {
    display: block;	    display: block;
}	}

#content.colM .cropduster-form .module.aligned {
    margin-left: 8em;
    padding-left: 10px;
}
#content.colM .cropduster-form.nested-inline-form .module.aligned {
    margin-left: 0;
}
  90  
cropduster/static/cropduster/css/upload.css
@@ -1,3 +1,16 @@
body.cropduster-upload-form.grp-popup #grp-content {
    top: 0;
}

body.cropduster-upload-form .module, body.cropduster-upload-form .grp-module {
    float: none;
}

body.cropduster-upload-form ul.messagelist,
body.cropduster-upload-form ul.grp-messagelist {
    overflow: hidden;
}

body.cropduster-upload-form #crop-form {	body.cropduster-upload-form #crop-form {
    margin-top: 15px;	    margin-top: 15px;
}	}
@@ -132,9 +145,9 @@ body.cropduster-debug form#upload .row.hidden {
#nav-left {	#nav-left {
    border-right: 1px solid #000;	    border-right: 1px solid #000;
}	}
body.cropduster-upload-form #nav-left.rounded-button,	body.cropduster-upload-form #nav-left.cropduster-button,
body.cropduster-upload-form #nav-left.rounded-button:active,	body.cropduster-upload-form #nav-left.cropduster-button:active,
body.cropduster-upload-form #nav-left.rounded-button:hover {	body.cropduster-upload-form #nav-left.cropduster-button:hover {
    width: 25px;	    width: 25px;
    -webkit-border-top-left-radius: 5px;	    -webkit-border-top-left-radius: 5px;
    -webkit-border-top-right-radius: 0;	    -webkit-border-top-right-radius: 0;
@@ -152,9 +165,9 @@ body.cropduster-upload-form #nav-left.rounded-button:hover {
    margin: 0;	    margin: 0;
	padding: 4px 5px 5px 5px !important;		padding: 4px 5px 5px 5px !important;
}	}
body.cropduster-upload-form #nav-right.rounded-button,	body.cropduster-upload-form #nav-right.cropduster-button,
body.cropduster-upload-form #nav-right.rounded-button:active,	body.cropduster-upload-form #nav-right.cropduster-button:active,
body.cropduster-upload-form #nav-right.rounded-button:hover {	body.cropduster-upload-form #nav-right.cropduster-button:hover {
    width: 25px;	    width: 25px;
    -webkit-border-top-right-radius: 5px;	    -webkit-border-top-right-radius: 5px;
    -webkit-border-bottom-right-radius: 5px;	    -webkit-border-bottom-right-radius: 5px;
@@ -171,13 +184,14 @@ body.cropduster-upload-form #nav-right.rounded-button:hover {
    margin: 0;	    margin: 0;
    padding: 4px 5px 5px 5px !important;	    padding: 4px 5px 5px 5px !important;
}	}
body.cropduster-upload-form #nav-left.rounded-button:active,	body.cropduster-upload-form #nav-left.cropduster-button:active,
body.cropduster-upload-form #nav-right.rounded-button:active {	body.cropduster-upload-form #nav-right.cropduster-button:active {
    padding: 5px 5px 4px 5px !important;	    padding: 5px 5px 4px 5px !important;
}	}


body.cropduster-upload-form h1#step-header {	body.cropduster-upload-form h1#step-header {
    margin: 24px 0 8px;	    margin: 0 0 8px;
    padding: 15px 0 5px;
}	}


body.cropduster-upload-form #content-main {	body.cropduster-upload-form #content-main {
@@ -193,6 +207,7 @@ body.cropduster-upload-form form#size .row {
    width: 50%;	    width: 50%;
    float: left;	    float: left;
    padding: 8px 0;	    padding: 8px 0;
    clear: none;
}	}
body.cropduster-upload-form form#size .row,	body.cropduster-upload-form form#size .row,
body.cropduster-upload-form form#size .row:first-child,	body.cropduster-upload-form form#size .row:first-child,
@@ -237,4 +252,59 @@ body.cropduster-upload-form.cropduster-standalone form#upload #reupload-button {
}	}
body.cropduster-upload-form.cropduster-standalone #grp-content #content-inner {	body.cropduster-upload-form.cropduster-standalone #grp-content #content-inner {
    bottom: 0;	    bottom: 0;
}	}

/* Django styles without grappelli */
body.cropduster-upload-form #container {
    position: absolute;
    height: 100%;
}
body.cropduster-upload-form #content.colM {
    position: absolute;
    width: 100%;
    height: 100%;
    margin: 0;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    padding: 0 15px 10px 15px;
    box-sizing: border-box;
    -moz-box-sizing: border-box;
}
body.cropduster-upload-form #content.colM footer {
    border: 0;
    border-top: 1px solid #111;
    position: absolute;
    width: auto;
    height: 34px;
    bottom: 0;
    left: 0;
    right: 0;
    margin: 0;
    padding: 2px 5px;
    line-height: 17px;
    color: #fff;
    background: #333;
    background: -moz-linear-gradient(top, #444, #333);
    background: -webkit-gradient(linear, left top, left bottom, from(#444), to(#333));
    background: -o-linear-gradient(top, #444, #333);
    box-sizing: border-box;
    -moz-box-sizing: border-box;
    -webkit-box-sizing: border-box;
}
body.cropduster-upload-form #content.colM footer ul,
body.cropduster-upload-form #content.colM footer ul li {
    margin: 0;
    padding: 0;
    list-style-type: none;
}
body.cropduster-upload-form #content.colM footer ul li {
    float: right;
    margin-left: 10px;
}

/* Help Text: Minimum image size*/
body.cropduster-upload-form #upload-min-size-help {
    float:right;
}
  234  
cropduster/static/cropduster/js/cropduster.js
@@ -3,6 +3,106 @@ window.CropDuster = {};


(function($) {	(function($) {


    // Backport jQuery.fn.data and jQuery.fn.on/off for jQuery 1.4.2,
    // which ships with Django 1.4
    if ($.prototype.jquery == '1.4.2') {
        var rbrace = /^(?:\{[\w\W]*\}|\[[\w\W]*\])$/,
            rdashAlpha = /-([\da-z])/gi,
            rmultiDash = /([A-Z])/g,
            // Used by jQuery.camelCase as callback to replace()
            fcamelCase = function( all, letter ) {
                 return letter.toUpperCase();
             };
        $.camelCase = function(string) {
            return string.replace(rdashAlpha, fcamelCase);
        };
        $.prototype.data = (function (originalDataMethod) {
            // the parse value function is copied from the jQuery source
             function parseValue(data) {
                 if (typeof data === "string") {
                     try {
                         data = data === "true" ? true :
                             data === "false" ? false :
                             data === "null" ? null :
                             // Only convert to a number if it doesn't change the string
                             +data + "" === data ? +data :
                             rbrace.test(data) ? $.parseJSON(data) : data;
                     } catch (e) {}
                 } else {
                     data = undefined;
                 }
                 return data;
             }

             return function(key, val) {
                 var data;
                 if (typeof key === "undefined") {
                     if (this.length) {
                         data = $.data(this[0]);
                         if (this[0].nodeType === 1) {
                             var attr = this[0].attributes, name;
                             for (var i = 0, l = attr.length; i < l; i++) {
                                 name = attr[i].name;
                                 if (name.indexOf("data-") === 0) {
                                     name = $.camelCase(name.substring(5));
                                     var value = parseValue(attr[i].value);
                                     $(this[0]).data(name, value);
                                     data[name] = value;
                                 }
                             }
                         }
                     }
                     return data;
                 }

                 var result = originalDataMethod.apply(this, arguments);

                 // only when it's an getter and the result from the original data method is null
                 if ((result === null || result === undefined) && val === undefined) {
                     var attrValue = this.attr("data-" + key.replace(rmultiDash, "-$1").toLowerCase());
                     return parseValue(attrValue);
                 }
                 return result;
             };
        })($.prototype.data);

        /**
         * add support for on and off methods
         * @type {Function|*|on}
         */
        $.prototype.on = $.prototype.on || function(/* events [,selector] [,data], handler */) {
            var args = arguments;

            // delegation bind has minimal 3 arguments
            if(args.length >= 3) {
                var events = args[0],
                    selector = args[1],
                    data = (args[3]) ? args[2] : null,
                    handler = (args[3]) ? args[3] : args[2];

                this.bind(events, data, function(ev) {
                    var $target = $(ev.target).closest(selector);
                    if($target.length) {
                        handler.call($target[0], ev);
                    }
                });
            } else {
                this.bind.apply(this, args);
            }

            return this;
        };

        $.prototype.off = $.prototype.off || function(/* events [,selector] [,handler] */) {
            if(arguments.length == 3) {
                throw new Error("Delegated .off is not implemented.");
            } else {
                this.unbind.apply(this, arguments);
            }
            return this;
        };
    }

    var randomDigits = function(length) {	    var randomDigits = function(length) {
        length = parseInt(length, 10);	        length = parseInt(length, 10);
        if (!length) {	        if (!length) {
@@ -12,21 +112,6 @@ window.CropDuster = {};
        return (zeroes + Math.ceil(Math.random() * Math.pow(10, length)).toString()).slice(-1 * length);	        return (zeroes + Math.ceil(Math.random() * Math.pow(10, length)).toString()).slice(-1 * length);
    };	    };


    var image_css = function(src, width, height, opts, is_ie) {	
        var css = '';	
        src = encodeURI(src || '') + '?v=' + randomDigits(9);	
        css += 'background-image:url("' + src + '");';	
        css += 'width:' + width + 'px;';	
        css += 'height:' + height + 'px;';	
        if (is_ie) {	
            var filter = 'progid:DXImageTransform.Microsoft.AlphaImageLoader(src=\'' + src + '\', sizingMethod=\'scale\')';	
            css += 'filter:' + filter + ';';	
            css += '-ms-filter:"' + filter + '";';	
        }	
        return css;	
    };	


    var GET_params = (function() {	    var GET_params = (function() {
        var url = window.location.search.substr(1);	        var url = window.location.search.substr(1);
        var parts = url.split('&');	        var parts = url.split('&');
@@ -45,20 +130,15 @@ window.CropDuster = {};


    // jsrender templates	    // jsrender templates
    if ($.views) {	    if ($.views) {
        $.views.helpers({	
            image_css: image_css,	
            ie_image_css: function(src, width, height, opts) {	
                return image_css.call(this, src, width, height, opts, true);	
            }	
        });	

        $.templates({	        $.templates({
            cropdusterImage: '<a target="_blank" class="cropduster-image cropduster-image-{{>size_slug}}" href="{{>image_url}}">' +	            cropdusterImage: [
                '<!' + '--[if lt IE 9]' + '>' +	                '<a target="_blank"',
                '<span style="{{>~ie_image_css(image_url, width, height)}}"></span>' +	                ' class="cropduster-image cropduster-image-{{>size_slug}}"',
                '<![endif]--><![if gte IE 9]>' +	                ' href="{{>image_url}}">',
                '   <span style="{{>~image_css(image_url, width, height)}}"></span>' +	                '<img class="cropduster-image-thumb cropduster-image-thumb-{{>size_slug}}"',
                '<![endif]></a>'	                ' src="{{>image_url}}" width="{{>width}}" height="{{>height}}"/>',
                '</a>'
            ].join(""),
        });	        });
    }	    }


@@ -109,6 +189,7 @@ window.CropDuster = {};
                    'value': thumb.id,	                    'value': thumb.id,
                    'data-width': thumb.width,	                    'data-width': thumb.width,
                    'data-height': thumb.height,	                    'data-height': thumb.height,
                    'data-url': thumb.url,
                    'data-tmp-file': 'true',	                    'data-tmp-file': 'true',
                    'selected': 'selected'	                    'selected': 'selected'
                });	                });
@@ -117,13 +198,10 @@ window.CropDuster = {};
        },	        },


        complete: function(prefix, data) {	        complete: function(prefix, data) {
            var formData = {	
                'id': data.crop.image_id,	
                'image': data.crop.orig_image	
            };	
            $('#id_' + prefix + '-0-id').val(data.crop.image_id);	            $('#id_' + prefix + '-0-id').val(data.crop.image_id);
            if ($('#id_' + prefix + '-0-image').val() != data.crop.orig_image) {	            // If no image id, set INITIAL_FORM count to 0
                formData['id'] = '';	            if ($('#id_' + prefix + '-0-id').val() == '') {
                $('#id_' + prefix + '-INITIAL_FORMS').val('0');
            }	            }
            $('#id_' + prefix + '-0-image').val(data.crop.orig_image);	            $('#id_' + prefix + '-0-image').val(data.crop.orig_image);
            $('#id_' + prefix).val(data.crop.orig_image);	            $('#id_' + prefix).val(data.crop.orig_image);
@@ -132,7 +210,13 @@ window.CropDuster = {};
                return;	                return;
            }	            }
            CropDuster.setThumbnails(prefix, data.crop.thumbs);	            CropDuster.setThumbnails(prefix, data.crop.thumbs);

            // add preview_url, height, and width from context data onto input field for preview rendering
            $("#id_" + prefix).data('previewUrl', data.preview_url);
            $("#id_" + prefix).data('previewW', data.preview_w);
            $("#id_" + prefix).data('previewH', data.preview_h);
            CropDuster.createThumbnails(prefix);	            CropDuster.createThumbnails(prefix);
            $(document).trigger('cropduster:update', [prefix, data]);
        },	        },


        /**	        /**
@@ -141,13 +225,14 @@ window.CropDuster = {};
        registerInput: function(input) {	        registerInput: function(input) {
            var $input = $(input);	            var $input = $(input);
            var data = $input.data();	            var data = $input.data();
            data.prefix = $input.attr('id').replace(/^id_/, '');
            var $customField = $input.parent().find('> .cropduster-customfield');	            var $customField = $input.parent().find('> .cropduster-customfield');


            $customField.click(function(e) {	            $customField.click(function(e) {
                var $target = $(e.target).closest('.cropduster-customfield');	                var $target = $(e.target).closest('.cropduster-customfield');
                e.preventDefault();	                e.preventDefault();
                e.stopPropagation();	                e.stopPropagation();
                var $targetInput = $target.closest('.row,.grp-row').find('.cropduster-data-field').eq(0);	                var $targetInput = $target.closest('.form-row,.row,.grp-row').find('.cropduster-data-field').eq(0);
                if (!$targetInput.length) {	                if (!$targetInput.length) {
                    return;	                    return;
                }	                }
@@ -161,7 +246,7 @@ window.CropDuster = {};
                CropDuster.show(fieldName, cropdusterUrl);	                CropDuster.show(fieldName, cropdusterUrl);
            });	            });


            var $inlineForm = $input.parent().find('.cropduster-form').first();	            var $inlineForm = $input.closest('.cropduster-form');


            CropDuster.mediaUrl = $inlineForm.data('mediaUrl');	            CropDuster.mediaUrl = $inlineForm.data('mediaUrl');


@@ -171,7 +256,7 @@ window.CropDuster = {};
                name = matches[1];	                name = matches[1];
            }	            }


            var $inputRow = $input.parents('.grp-row.' + name + ',.row.' + name);	            var $inputRow = $input.closest('.grp-row.' + name + ',.row.' + name + ',.form-row.field-' + name);
            if ($inputRow.length) {	            if ($inputRow.length) {
                var inputLabel = $inputRow.find('label').html();	                var inputLabel = $inputRow.find('label').html();
                if (inputLabel) {	                if (inputLabel) {
@@ -184,11 +269,11 @@ window.CropDuster = {};
            }	            }


            $inlineForm.find('span.delete input').change(function() {	            $inlineForm.find('span.delete input').change(function() {
                form = $(this).parents('.cropduster-form');	                var $row = $(this).closest('.cropduster-form');
                if (this.checked) {	                if (this.checked) {
                    form.addClass('pre-delete');	                    $row.addClass('predelete grp-predelete');
                } else {	                } else {
                    form.removeClass('pre-delete');	                    $row.removeClass('predelete grp-predelete');
                }	                }
            });	            });
            // Re-initialize thumbnail images. This is necessary in the event that	            // Re-initialize thumbnail images. This is necessary in the event that
@@ -200,12 +285,15 @@ window.CropDuster = {};
        },	        },


        createThumbnails: function(prefix) {	        createThumbnails: function(prefix) {
            $input = $("input[data-prefix='" + prefix + "']");	            var $input = $("#id_" + prefix);
            var data = $input.data();	            var data = $input.data();
            if (!$input.length) {	            if (!$input.length) {
                return;	                return;
            }	            }
            var image = $('#id_' + prefix + '-0-image').val();	            var image = $('#id_' + prefix + '-0-image').val();
            if (!image) {
                return;
            }
            // The groups in this regex correspond to the path, basename (sans	            // The groups in this regex correspond to the path, basename (sans
            // extension), and file extension of a file path or url.	            // extension), and file extension of a file path or url.
            var matches = image.match(/^(.*)(\/(?:[^\/](?!\.[^\.\/\?]+))*[^\.\/\?])(\.[^\.\/\?]+)?$/);	            var matches = image.match(/^(.*)(\/(?:[^\/](?!\.[^\.\/\?]+))*[^\.\/\?])(\.[^\.\/\?]+)?$/);
@@ -234,26 +322,68 @@ window.CropDuster = {};
                if (data.tmpFile) {	                if (data.tmpFile) {
                    name += "_tmp";	                    name += "_tmp";
                }	                }
                var url = [CropDuster.mediaUrl, path, name + ext].join('/');	
                // This is in place of a negative lookbehind. It replaces all	
                // double slashes that don't follow a colon.	
                url = url.replace(/(:)?\/+/g, function($0, $1) { return $1 ? $0 : '/'; });	
                thumbData[slug] = {	                thumbData[slug] = {
                    'image_url': url,	                    'image_url': data.url,
                    'size_slug': slug,	                    'size_slug': slug,
                    'width': data.width,	                    'width': data.width,
                    'height': data.height	                    'height': data.height
                };	                };
            });	            });
            var $thumb = $input.closest('.row,.grp-row').find('.cropduster-images');	            var $thumb = $input.closest('.cropduster-form').find('.cropduster-images');
            $thumb.find('a').remove();	            $thumb.find('a').remove();
            preview_img = {
                'image_url': data.previewUrl,
                'size_slug': 'preview',
                'width': data.previewW,
                'height': data.previewH
            }
            $thumb.html($.render.cropdusterImage(preview_img) + $thumb.html());
        },


            $.each(data.sizes, function(i, size) {	        removeSize: function(prefix, sizeName) {
                if (!size || !size.name) return;	            var $selector = $('#id_' + prefix);
                if (thumbData[size.name]) {	
                    $thumb.html($thumb.html() + $.render.cropdusterImage(thumbData[size.name]));	            var sizes = $selector.data('sizes');

            for (var i = 0; i < sizes.length; i++) {
                if (sizes[i].name == sizeName) {
                    break;
                }	                }
            });	            }

            // Check that we found the size we need
            if (i == sizes.length) {
                return;
            }

            // values returned from $.fn.data() are references, so any modifications
            // we make to the array will persist across calls to $.fn.data()
            var removedSizes = sizes.splice(i, 1);

            var removedSizesData = $selector.data('removedSizes') || {};
            if ($.isEmptyObject(removedSizesData)) {
                $selector.data('removedSizes', removedSizesData);
            }

            removedSizesData[sizeName] = {
                index: i,
                size: removedSizes[0]
            };
        },

        restoreSize: function(prefix, sizeName) {
            var $selector = $('#id_' + prefix);
            var sizes = $selector.data('sizes');
            var removedSizesData = $selector.data('removedSizes');

            // If no size with sizeName has yet been removed, return
            if (!removedSizesData || !removedSizesData[sizeName]) {
                return;
            }

            var sizeToRestore = removedSizesData[sizeName];
            sizes.splice(sizeToRestore.index, 0, sizeToRestore.size);
            delete removedSizesData[sizeName];
        }	        }


    };	    };
  2  
cropduster/static/cropduster/js/jquery.form.js
@@ -88,7 +88,7 @@ $.fn.ajaxSubmit = function(options) {
		url:  url,			url:  url,
		success: $.ajaxSettings.success,			success: $.ajaxSettings.success,
		type: this[0].getAttribute('method') || 'GET', // IE7 massage (see issue 57)			type: this[0].getAttribute('method') || 'GET', // IE7 massage (see issue 57)
		iframeSrc: /^https/i.test(window.location.href || '') ? 'javascript:false' : 'about:blank'			iframeSrc: 'about:blank'
	}, options);		}, options);


	// hook for manipulating the form data before it is extracted;		// hook for manipulating the form data before it is extracted;
  144  
cropduster/static/cropduster/js/jquery.jcrop.js
@@ -62,6 +62,13 @@
    function setOptions(opt) //{{{	    function setOptions(opt) //{{{
    {	    {
      if (typeof(opt) !== 'object') opt = {};	      if (typeof(opt) !== 'object') opt = {};

      if (opt.aspectRatio) {
        opt.minAspectRatio = opt.aspectRatio;
        opt.maxAspectRatio = opt.aspectRatio;
        delete opt.aspectRatio;
      }

      options = $.extend(options, opt);	      options = $.extend(options, opt);


      $.each(['onChange','onSelect','onRelease','onDblClick'],function(i,e) {	      $.each(['onChange','onSelect','onRelease','onDblClick'],function(i,e) {
@@ -84,14 +91,15 @@


      Coords.setPressed(Coords.getCorner(opp));	      Coords.setPressed(Coords.getCorner(opp));
      Coords.setCurrent(opc);	      Coords.setCurrent(opc);
      Coords.setWidthHeight(fc.w, fc.h);


      Tracker.activateHandlers(dragmodeHandler(mode, fc), doneSelect, touch);	      Tracker.activateHandlers(dragmodeHandler(mode, fc), doneSelect, touch);
    }	    }
    //}}}	    //}}}
    function dragmodeHandler(mode, f) //{{{	    function dragmodeHandler(mode, f) //{{{
    {	    {
      return function (pos) {	      return function (pos) {
        if (!options.aspectRatio) {	        if (!options.minAspectRatio || !options.maxAspectRatio) {
          switch (mode) {	          switch (mode) {
          case 'e':	          case 'e':
            pos[1] = f.y2;	            pos[1] = f.y2;
@@ -122,7 +130,7 @@
            break;	            break;
          }	          }
        }	        }
        Coords.setCurrent(pos);	        Coords.setCurrent(pos, mode);
        Selection.update();	        Selection.update();
      };	      };
    }	    }
@@ -227,15 +235,11 @@
    //}}}	    //}}}
    function newSelection(e) //{{{	    function newSelection(e) //{{{
    {	    {
      var c = Coords.getFixed();	
      if ((c.w > options.minSelect[0]) && c.h > options.minSelect[1]) {	
        return false;	
      }	
      if (options.disabled) {	      if (options.disabled) {
        return false;	        return;
      }	      }
      if (!options.allowSelect) {	      if (!options.allowSelect) {
        return false;	        return;
      }	      }
      btndown = true;	      btndown = true;
      docOffset = getPos($img);	      docOffset = getPos($img);
@@ -463,7 +467,7 @@
          y1 = 0,	          y1 = 0,
          x2 = 0,	          x2 = 0,
          y2 = 0,	          y2 = 0,
          ox, oy;	          ox, oy, iw, ih;


      function setPressed(pos) //{{{	      function setPressed(pos) //{{{
      {	      {
@@ -472,13 +476,54 @@
        y2 = y1 = pos[1];	        y2 = y1 = pos[1];
      }	      }
      //}}}	      //}}}
      function setCurrent(pos) //{{{	      function setCurrent(pos, mode) //{{{
      {	      {
        pos = rebound(pos);	        pos = rebound(pos);
        var c1, c2, old_x1 = x1, old_y1 = y1;
        if (typeof mode != 'undefined') {
          c1 = Coords.getFixed();
          x1 = old_x1;
          y1 = old_y1;
        }
        ox = pos[0] - x2;	        ox = pos[0] - x2;
        oy = pos[1] - y2;	        oy = pos[1] - y2;
        x2 = pos[0];	        x2 = pos[0];
        y2 = pos[1];	        y2 = pos[1];
        if (typeof mode == 'undefined') {
          return;
        }
        c2 = Coords.getFixed();
        x1 = old_x1;
        y1 = old_y1;
        if (c1.w == c2.w && c1.h == c2.h) {
          return;
        }
        if (ox !== 0 && oy !== 0) {
          return;
        }
        var aspect = c2.w / c2.h,
            minAspect = options.minAspectRatio,
            maxAspect = options.maxAspectRatio;
        if (minAspect && aspect <= minAspect || maxAspect && aspect >= maxAspect) {
          switch (mode) {
            case 'n':
            case 's':
              var dx = c1.x2 - c2.x2;
              x1 += dx / 2;
              break;
            case 'e':
            case 'w':
              var dy = c1.y2 - c2.y2;
              y1 += dy / 2;
              break;
          }
        }
      }
      //}}}
      function setWidthHeight(w, h) //{{{
      {
        iw = w;
        ih = h;
      }	      }
      //}}}	      //}}}
      function getOffset() //{{{	      function getOffset() //{{{
@@ -528,11 +573,12 @@
      //}}}	      //}}}
      function getFixed() //{{{	      function getFixed() //{{{
      {	      {
        if (!options.aspectRatio) {	        if (!options.minAspectRatio && !options.maxAspectRatio) {
          return getRect();	          return getRect();
        }	        }
        // This function could use some optimization I think...	        // This function could use some optimization I think...
        var aspect = options.aspectRatio,	        var minAspect = options.minAspectRatio,
            maxAspect = options.maxAspectRatio,
            min_x = options.minSize[0] / xscale,	            min_x = options.minSize[0] / xscale,




@@ -544,43 +590,49 @@
            rwa = Math.abs(rw),	            rwa = Math.abs(rw),
            rha = Math.abs(rh),	            rha = Math.abs(rh),
            real_ratio = rwa / rha,	            real_ratio = rwa / rha,
            xx, yy, w, h;	            xx, yy, w, h, aspect,
            vertical = function() {
                yy = y2;
                w = rha * aspect;
                xx = rw < 0 ? x1 - w : w + x1;

                if (xx < 0) {
                  xx = 0;
                } else if (xx > boundx) {
                  xx = boundx;
                }
                h = Math.abs((xx - x1) / aspect);
                yy = rh < 0 ? y1 - h : h + y1;
            },
            horizontal = function() {
                xx = x2;
                h = rwa / aspect;
                yy = rh < 0 ? y1 - h : y1 + h;
                if (yy < 0) {
                  yy = 0;
                } else if (yy > boundy) {
                  yy = boundy;
                }
                w = Math.abs((yy - y1) * aspect);
                xx = rw < 0 ? x1 - w : w + x1;
            };


        if (max_x === 0) {	        if (max_x === 0) {
          max_x = boundx * 10;	          max_x = boundx * 10;
        }	        }
        if (max_y === 0) {	        if (max_y === 0) {
          max_y = boundy * 10;	          max_y = boundy * 10;
        }	        }
        if (real_ratio < aspect) {	        if (minAspect && real_ratio < minAspect) {
          yy = y2;	          aspect = minAspect;
          w = rha * aspect;	        } else if (maxAspect && real_ratio > maxAspect) {
          xx = rw < 0 ? x1 - w : w + x1;	          aspect = maxAspect;

          if (xx < 0) {	
            xx = 0;	
            h = Math.abs((xx - x1) / aspect);	
            yy = rh < 0 ? y1 - h : h + y1;	
          } else if (xx > boundx) {	
            xx = boundx;	
            h = Math.abs((xx - x1) / aspect);	
            yy = rh < 0 ? y1 - h : h + y1;	
          }	
        } else {	        } else {
          xx = x2;	          return getRect();
          h = rwa / aspect;	
          yy = rh < 0 ? y1 - h : y1 + h;	
          if (yy < 0) {	
            yy = 0;	
            w = Math.abs((yy - y1) * aspect);	
            xx = rw < 0 ? x1 - w : w + x1;	
          } else if (yy > boundy) {	
            yy = boundy;	
            w = Math.abs(yy - y1) * aspect;	
            xx = rw < 0 ? x1 - w : w + x1;	
          }	
        }	        }


        Math.abs(rwa - iw) > Math.abs(rha - ih) ? horizontal() : vertical();

        // Magic %-)	        // Magic %-)
        if (xx > x1) { // right side	        if (xx > x1) { // right side
          if (xx - x1 < min_x) {	          if (xx - x1 < min_x) {
@@ -633,7 +685,7 @@
        if (p[0] > boundx) p[0] = boundx;	        if (p[0] > boundx) p[0] = boundx;
        if (p[1] > boundy) p[1] = boundy;	        if (p[1] > boundy) p[1] = boundy;


        return [p[0], p[1]];	        return [Math.round(p[0]), Math.round(p[1])];
      }	      }
      //}}}	      //}}}
      function flipCoords(x1, y1, x2, y2) //{{{	      function flipCoords(x1, y1, x2, y2) //{{{
@@ -659,11 +711,11 @@
            ysize = y2 - y1,	            ysize = y2 - y1,
            delta;	            delta;


        if (xlimit && (Math.abs(xsize) > xlimit)) {	        if (xlimit && (Math.abs(xsize) > xlimit / xscale)) {
          x2 = (xsize > 0) ? (x1 + xlimit) : (x1 - xlimit);	          x2 = (xsize > 0) ? (x1 + xlimit / xscale) : (x1 - xlimit / xscale);
        }	        }
        if (ylimit && (Math.abs(ysize) > ylimit)) {	        if (ylimit && (Math.abs(ysize) > ylimit / yscale)) {
          y2 = (ysize > 0) ? (y1 + ylimit) : (y1 - ylimit);	          y2 = (ysize > 0) ? (y1 + ylimit / yscale) : (y1 - ylimit / yscale);
        }	        }


        if (ymin / yscale && (Math.abs(ysize) < ymin / yscale)) {	        if (ymin / yscale && (Math.abs(ysize) < ymin / yscale)) {
@@ -730,6 +782,7 @@
        flipCoords: flipCoords,	        flipCoords: flipCoords,
        setPressed: setPressed,	        setPressed: setPressed,
        setCurrent: setCurrent,	        setCurrent: setCurrent,
        setWidthHeight: setWidthHeight,
        getOffset: getOffset,	        getOffset: getOffset,
        moveOffset: moveOffset,	        moveOffset: moveOffset,
        getCorner: getCorner,	        getCorner: getCorner,
@@ -1664,7 +1717,8 @@
    handleOpacity: 0.5,	    handleOpacity: 0.5,
    handleSize: null,	    handleSize: null,


    aspectRatio: 0,	    minAspectRatio: 0,
    maxAspectRatio: 0,
    keySupport: true,	    keySupport: true,
    createHandles: ['n','s','e','w','nw','ne','se','sw'],	    createHandles: ['n','s','e','w','nw','ne','se','sw'],
    createDragbars: ['n','s','e','w'],	    createDragbars: ['n','s','e','w'],
 19  
cropduster/static/cropduster/js/jquery.jcrop.min.js
Large diffs are not rendered by default.

 219  
cropduster/static/cropduster/js/upload.js
Large diffs are not rendered by default.

  19  
cropduster/templates/cropduster/custom_field.html
@@ -1,17 +1,21 @@
{% load i18n adminmedia %}	{% load i18n %}

<div class="module cropduster-form nested-inline-form" id="{{ inline_admin_formset.formset.prefix }}-group" data-media-url="{{ media_url }}">


<input type="hidden" id="{{ final_attrs.id }}-0-id" name="{{ final_attrs.name }}-0-id" value="{{ final_attrs.value }}"/>	<input type="hidden" id="{{ final_attrs.id }}-0-id" name="{{ final_attrs.name }}-0-id" value="{{ final_attrs.value }}"/>
<input type="text"	<input type="text"
       id="{{ final_attrs.id }}"	       id="{{ final_attrs.id }}"
       name="{{ final_attrs.name }}"	       name="{{ final_attrs.name }}"
       value="{{ image_value }}"	       value="{{ file_value }}"
       class="cropduster-data-field cropduster-text-field"	       class="cropduster-data-field cropduster-text-field"
       data-sizes="{{ final_attrs.sizes }}"	       data-sizes="{{ sizes }}"
       data-upload-to="{{ upload_to }}"	       data-preview-url="{{ preview_url }}"
       data-prefix="{{ prefix }}"/>	       data-preview-w="{{ preview_w }}"
       data-preview-h="{{ preview_h }}"
       data-upload-to="{{ upload_to }}"/>


<a href="#" class="cropduster-customfield cropduster-upload-form" data-cropduster-url="{% url cropduster-index %}?pop=1">	<a href="#" class="cropduster-customfield cropduster-upload-form" data-cropduster-url="{% url 'cropduster-index' %}?pop=1">
    <div class="rounded-button">Upload Image</div>	    <div class="cropduster-button">Upload Image</div>
    <div style="clear:both; height:3px"></div>	    <div style="clear:both; height:3px"></div>
</a>	</a>


@@ -24,3 +28,4 @@
<div style="clear:both"></div>	<div style="clear:both"></div>




</div>
 8  
cropduster/templates/cropduster/inline.html
@@ -1,18 +1,14 @@
{% load i18n adminmedia %}	{% load i18n %}

<div class="module cropduster-form" id="{{ inline_admin_formset.formset.prefix }}-group" data-media-url="{{ media_url }}">	


{{ inline_admin_formset.formset.management_form }}	{{ inline_admin_formset.formset.management_form }}
{{ inline_admin_formset.formset.non_form_errors }}	{{ inline_admin_formset.formset.non_form_errors }}


{% for inline_admin_form in inline_admin_formset %}	{% for inline_admin_form in inline_admin_formset %}
    <div class="inline-related{% if forloop.last %} empty-form last-related{% endif %}" id="{{ inline_admin_formset.formset.prefix }}-{% if not forloop.last %}{{ forloop.counter0 }}{% else %}empty{% endif %}">	    <div class="{% if forloop.last %} empty-form grp-empty-form last-related{% endif %}" id="{{ inline_admin_formset.formset.prefix }}-{% if not forloop.last %}{{ forloop.counter0 }}{% else %}empty{% endif %}">
        {% if inline_admin_formset.formset.can_delete and inline_admin_form.original %}<span class="delete">{{ inline_admin_form.deletion_field.field }} {{ inline_admin_form.deletion_field.label_tag }}</span>{% endif %}	        {% if inline_admin_formset.formset.can_delete and inline_admin_form.original %}<span class="delete">{{ inline_admin_form.deletion_field.field }} {{ inline_admin_form.deletion_field.label_tag }}</span>{% endif %}
        {% if inline_admin_form.form.non_field_errors %}{{ inline_admin_form.form.non_field_errors }}{% endif %}	        {% if inline_admin_form.form.non_field_errors %}{{ inline_admin_form.form.non_field_errors }}{% endif %}
        {% for fieldset in inline_admin_form %}	        {% for fieldset in inline_admin_form %}
            {% include "admin/includes/fieldset.html" %}	            {% include "admin/includes/fieldset.html" %}
        {% endfor %}	        {% endfor %}
        {{ inline_admin_form.fk_field.field }}	
    </div>	    </div>
{% endfor %}	{% endfor %}
</div>	
  69  
cropduster/templates/cropduster/upload.html
@@ -1,9 +1,15 @@
{% extends parent_template %}	{% extends parent_template %}


<!-- LOADING -->	<!-- LOADING -->
{% load i18n adminmedia %}	{% load i18n %}


{% block extrahead %}	{% block extrahead %}
    {% if django_is_gte_19 %}
    <script type="text/javascript" src="{{ STATIC_URL }}admin/js/vendor/jquery/jquery.min.js"></script>
    {% else %}
    <script type="text/javascript" src="{{ STATIC_URL }}admin/js/jquery.min.js"></script>
    {% endif %}
    <script type="text/javascript" src="{{ STATIC_URL }}admin/js/jquery.init.js"></script>
    {{ block.super }}	    {{ block.super }}
    {{ crop_form.media }}	    {{ crop_form.media }}
    {{ thumb_formset.media }}	    {{ thumb_formset.media }}
@@ -25,47 +31,50 @@
<h1 id="step-header">Upload, Crop, and Generate Thumbnails</h1>	<h1 id="step-header">Upload, Crop, and Generate Thumbnails</h1>
{% endif %}	{% endif %}
<div id="content-main">	<div id="content-main">
    <fieldset class="module aligned">	    <fieldset class="module grp-module aligned">


        <form id="upload" action="{% url cropduster.views.upload %}{% if standalone %}?standalone=1{% endif %}" method="POST">	        <form id="upload" action="{% url 'cropduster-upload' %}{% if standalone %}?standalone=1{% endif %}" method="POST">
            {% for field in upload_form %}	            {% for field in upload_form %}
                <div class="row {{ field.name }}{% if field.name != 'image' %} hidden{% endif %}">	                <div class="grp-row row {{ field.name }}{% if field.name != 'image' %} hidden{% endif %}">
                    {% if field.name != "image" %}{{ field.label_tag|safe }}{% endif %}	                    {% if field.name != "image" %}{{ field.label_tag|safe }}{% endif %}
                    {{ field }}	                    {{ field }}
                    {% if field.name == "image" %}
                        <div id="upload-min-size-help"></div>
                    {% endif %}
                </div>	                </div>
            {% endfor %}	            {% endfor %}
            {% if standalone %}	            {% if standalone %}
            {# <li class="submit-button-container"> #}	
                <div id="upload-footer"{% if not image_id %} style="display: none"{% endif %}>	                <div id="upload-footer"{% if not image_id %} style="display: none"{% endif %}>
                <input id="upload-button" class="rounded-button disabled{% if standalone %} small{% endif %}" type="submit" name="_save" value='Upload'  onclick="return uploadSubmit();"/>	                    <input id="upload-button" class="cropduster-button disabled{% if standalone %} small{% endif %}" type="submit" name="_save" value='Upload'  onclick="return uploadSubmit(this);"/>
                </div>	                </div>
                <div id="crop-footer"{% if image_id %} style="display: none"{% endif %}>	                <div id="crop-footer"{% if image_id %} style="display: none"{% endif %}>
                <input id="reupload-button" class="rounded-button disabled{% if standalone %} small{% endif %}" type="submit" name="_save" value='Re-Upload' onclick="return uploadSubmit();" />	                    <input id="reupload-button" class="cropduster-button disabled{% if standalone %} small{% endif %}" type="submit" name="_save" value='Re-Upload' onclick="return uploadSubmit(this);" />
                </div>	                </div>
            {# </li> #}	
            {% endif %}	            {% endif %}
        </form>	        </form>


        {% if standalone %}	        {% if standalone %}
        <form id="size" action="" onsubmit="return false">	        <form id="size" action="" onsubmit="return false">
                <div class="row cells-1 width">	            <div class="row form-row grp-row cells-1 grp-cells-1 width">
                    <div class="column span-4">	                <div class="field-box l-2c-fluid l-d-4">
                    <div class="column span-4 c-1">
                        <label for="id_size-width">Width</label>	                        <label for="id_size-width">Width</label>
                    </div>	                    </div>
                    <div class="column span-flexible">	                    <div class="column span-flexible c-2">
                        <input type="text" name="size-width" id="id_size-width" />	                        <input type="text" name="size-width" id="id_size-width" />
                    </div>	                    </div>
                    <div class="float-clear-div" style="clear:both;height:0;width:0"></div>	
                </div>	                </div>
                <div class="row cells-1 height">	            </div>
                    <div class="column span-4">	            <div class="row form-row grp-row cells-1 grp-cells-1 height">
                <div class="field-box l-2c-fluid l-d-4">
                    <div class="column span-4 c-1">
                        <label for="id_size-height">Height</label>	                        <label for="id_size-height">Height</label>
                    </div>	                    </div>
                    <div class="column span-flexible">	                    <div class="column span-flexible c-2">
                        <input type="text" name="size-height" id="id_size-height" />	                        <input type="text" name="size-height" id="id_size-height" />
                    </div>	                    </div>
                    <div class="float-clear-div" style="clear:both;height:0;height:0"></div>	
                </div>	                </div>
            </div>
        </form>	        </form>
        {% endif %}	        {% endif %}


@@ -75,7 +84,7 @@ <h1 id="step-header">Upload, Crop, and Generate Thumbnails</h1>
        <p class="errornote"></p>	        <p class="errornote"></p>
    </div>	    </div>


    <form action="{% url cropduster.views.crop %}" method="POST" id="crop-form">	    <form action="{% url 'cropduster-crop' %}" method="POST" id="crop-form">
        <div id="image-container">	        <div id="image-container">
            <img src="{{ image }}" id="cropbox" />	            <img src="{{ image }}" id="cropbox" />
        </div>	        </div>
@@ -90,35 +99,35 @@ <h1 id="step-header">Upload, Crop, and Generate Thumbnails</h1>
                {% endfor %}	                {% endfor %}
            </div>	            </div>
        </div>	        </div>
        <div class="module footer">	        <footer class="module grp-module grp-submit-row footer grp-fixed-footer">
            <div id="crop-nav">	            <div id="crop-nav">
                <div id="nav-left" class="rounded-button disabled"><span></span></div>	                <div id="nav-left" class="cropduster-button disabled"><span></span></div>
                <div id="nav-right" class="rounded-button disabled"><span></span></div>	                <div id="nav-right" class="cropduster-button disabled"><span></span></div>
            </div>	            </div>
            <div id="current-thumb-info">	            <div id="current-thumb-info">
                <div id="current-thumb-index"></div>	                <div id="current-thumb-index"></div>
                <div id="thumb-total-count"></div>	                <div id="thumb-total-count"></div>
                <div id="current-thumb-label"></div>	                <div id="current-thumb-label"></div>
            </div>	            </div>
            {% if not standalone %}	            {% if not standalone %}
            <ul class="submit-row" id="upload-footer"{% if not image_id %} style="display: none"{% endif %}>	            <ul class="submit-row grp-submit-row" id="upload-footer"{% if not image_id %} style="display: none"{% endif %}>
                <li class="submit-button-container">	                <li class="submit-button-container grp-submit-button-container">
                    <input id="upload-button" class="rounded-button disabled{% if standalone %} small{% endif %}" type="submit" name="_save" value='Upload'  onclick="return uploadSubmit();"/>	                    <input id="upload-button" class="cropduster-button disabled{% if standalone %} small{% endif %}" type="submit" name="_save" value='Upload'  onclick="return uploadSubmit(this);"/>
                </li>	                </li>
            </ul>	            </ul>
            {% endif %}	            {% endif %}
            <ul class="submit-row" id="crop-footer"{% if image_id %} style="display: none"{% endif %}>	            <ul class="grp-submit-row submit-row" id="crop-footer"{% if image_id %} style="display: none"{% endif %}>
                <li class="submit-button-container">	                <li class="submit-button-container grp-submit-button-container">
                    <input id="crop-button" class="rounded-button{% if standalone %} small{% endif %}" type="submit" name="crop" value="Crop and Continue" />	                    <input id="crop-button" class="cropduster-button{% if standalone %} small{% endif %}" type="submit" name="crop" value="Crop and Continue" />
                </li>	                </li>
                {% if not standalone %}	                {% if not standalone %}
                <li class="submit-button-container">	                <li class="submit-button-container grp-submit-button-container">
                    <input id="reupload-button" class="rounded-button disabled{% if standalone %} small{% endif %}" type="submit" name="_save" value='Re-Upload' onclick="return uploadSubmit();" />	                    <input id="reupload-button" class="cropduster-button disabled{% if standalone %} small{% endif %}" type="submit" name="_save" value='Re-Upload' onclick="return uploadSubmit(this);" />
                </li>	                </li>
                {% endif %}	                {% endif %}
            </ul>	            </ul>
        </div>	        </footer>
    </form>	    </form>


</div>	</div>
{% endblock %}	{% endblock %}
 67  
cropduster/templatetags/cropduster_tags.py
@@ -1,33 +1,74 @@
import time
import warnings

import django
from django import template	from django import template
from cropduster.models import Image
from cropduster.resizing import Size


register = template.Library()	register = template.Library()


@register.assignment_tag	
def get_crop(image, crop_name):	if django.VERSION >= (1, 9):
    tag_decorator = register.simple_tag
else:
    tag_decorator = register.assignment_tag


@tag_decorator
def get_crop(image, crop_name, **kwargs):
    """	    """
    Get the crop of an image. Usage:	    Get the crop of an image. Usage:
    {% get_crop article.image 'square_thumbnail' as crop %}	    {% get_crop article.image 'square_thumbnail' attribution=1 as img %}
    will return a dictionary of	    will assign to `img` a dictionary that looks like:
    {	    {
        "url": /media/path/to/my.jpg,	        "url": '/media/path/to/my.jpg',
        "width": 150,	        "width": 150,
        "height" 150,	        "height" 150,
        "attribution": 'Stock Photoz',
        "attribution_link": 'http://stockphotoz.com',
        "caption": 'Woman laughing alone with salad.',
        "alt_text": 'Woman laughing alone with salad.'
    }	    }
    For use in an image tag or style block.	    For use in an image tag or style block like:
        <img src="{{ img.url }}">
    The `exact_size` kwarg is deprecated.
    Omitting the `attribution` kwarg will omit the attribution, attribution_link,
    and caption.
    """	    """


    # If this isn't a cropduster field, abort	    if "exact_size" in kwargs:
    if not getattr(image, 'cropduster_image', None):	        warnings.warn("get_crop's `exact_size` kwarg is deprecated.", DeprecationWarning)

    if not image or not image.related_object:
        return None	        return None
    w, h = image.cropduster_image.get_image_size(size_name=crop_name)	
    url = image.cropduster_image.get_image_url(size_name=crop_name)	


    url = getattr(Image.get_file_for_size(image, crop_name), 'url', None)

    thumbs = {thumb.name: thumb for thumb in image.related_object.thumbs.all()}
    try:
        thumb = thumbs[crop_name]
    except KeyError:
        if crop_name == "original":
            thumb = image.related_object
        else:
            return None

    cache_buster = str(time.mktime(thumb.date_modified.timetuple()))[:-2]
    return {	    return {
        "width": w,	        "url": "%s?%s" % (url, cache_buster),
        "height": h,	        "width": thumb.width,
        "url": url,	        "height": thumb.height,
        "attribution": image.related_object.attribution,
        "attribution_link": image.related_object.attribution_link,
        "caption": image.related_object.caption,
        "alt_text": image.related_object.alt_text,
    }	    }
 20  
cropduster/urls.py
@@ -1,12 +1,12 @@
try:	from django.conf.urls import url
    from django.conf.urls import patterns, url	
except ImportError:	
    from django.conf.urls.defaults import patterns, url	


import cropduster.views
import cropduster.standalone.views


urlpatterns = patterns('',	
    url(r'^$', 'cropduster.views.index', name='cropduster-index'),	urlpatterns = [
    url(r'^crop/', 'cropduster.views.crop', name='cropduster-crop'),	    url(r'^$', cropduster.views.index, name='cropduster-index'),
    url(r'^upload/', 'cropduster.views.upload', name='cropduster-upload'),	    url(r'^crop/', cropduster.views.crop, name='cropduster-crop'),
    url(r'^standalone/', 'cropduster.standalone.views.index', name='cropduster-standalone'),	    url(r'^upload/', cropduster.views.upload, name='cropduster-upload'),
)	    url(r'^standalone/', cropduster.standalone.views.index, name='cropduster-standalone'),
]
 8  
cropduster/utils/__init__.py
@@ -1,4 +1,8 @@
from .image import get_image_extension	from .image import (
from .paths import get_upload_foldername, get_media_path, get_relative_media_url	    get_image_extension, is_transparent, exif_orientation,
    correct_colorspace, is_animated_gif, has_animated_gif_support, process_image,
    smart_resize)
from .paths import get_upload_foldername
from .sizes import get_min_size	from .sizes import get_min_size
from .thumbs import set_as_auto_crop, unset_as_auto_crop
from . import jsonutils as json	from . import jsonutils as json
 55  
cropduster/utils/gifsicle.py
@@ -0,0 +1,55 @@
import logging
import os
import subprocess

from cropduster.settings import CROPDUSTER_GIFSICLE_PATH
from django.core.files.storage import default_storage


logger = logging.getLogger(__name__)


class GifsicleImage(object):

    def __init__(self, im):
        if not CROPDUSTER_GIFSICLE_PATH:
            raise Exception(
                "Cannot use GifsicleImage without the gifsicle binary in the PATH")

        self.pil_image = im
        self.size = im.size
        self.cmd_args = [CROPDUSTER_GIFSICLE_PATH, '-O3', '-I', '-I', '-w']
        self.crop_args = []
        self.resize_args = []

    @property
    def args(self):
        return self.cmd_args + self.crop_args + self.resize_args

    def crop(self, box):
        x1, y1, x2, y2 = box
        if x2 < x1:
            x2 = x1
        if y2 < y1:
            y2 = y1

        self.size = (x2 - x1, y2 - y1)
        self.crop_args = ['--crop', "%d,%d-%d,%d" % (x1, y1, x2, y2)]
        return self

    def resize(self, size, method):
        # Ignore method, PIL's algorithms don't match up
        self.resize_args = [
            "--resize-fit", "%dx%d" % size,
            "--resize-method", "mix",
            "--resize-colors", "128",
        ]
        return self

    def save(self, buf, **kwargs):
        proc = subprocess.Popen(self.args, stdin=subprocess.PIPE, stdout=subprocess.PIPE, stderr=subprocess.PIPE)
        with default_storage.open(self.pil_image.filename, 'rb') as f:
            out, err = proc.communicate(input=f.read())
        logger.debug(err)
        buf.write(out)
        buf.seek(0)
  188  
cropduster/utils/image.py
@@ -1,9 +1,35 @@
from __future__ import division	from __future__ import division


from io import BytesIO
import os
import warnings
import math
from distutils.version import LooseVersion

import PIL.Image	import PIL.Image
from PIL import ImageFile, JpegImagePlugin

from django.core.files.storage import default_storage
from django.utils import six
from django.utils.six.moves import xrange

from cropduster.settings import (
    get_jpeg_quality, JPEG_SAVE_ICC_SUPPORTED, CROPDUSTER_GIFSICLE_PATH)

from .gifsicle import GifsicleImage



__all__ = (
    'get_image_extension', 'is_transparent', 'exif_orientation',
    'correct_colorspace', 'is_animated_gif', 'has_animated_gif_support',
    'process_image', 'smart_resize')


__all__ = ('get_image_extension')	
# workaround for https://github.com/python-pillow/Pillow/issues/1138
# without this hack, pillow misidenfifies some jpeg files as "mpo" files
JpegImagePlugin._getmp = lambda x: None  # noqa

ImageFile.MAXBLOCK = 4096 * 4096 * 8




IMAGE_EXTENSIONS = {	IMAGE_EXTENSIONS = {
@@ -14,16 +40,174 @@
    "MSP":  ".msp",   "Palm": ".palm",  "PCD":  ".pcd",   "PCX":  ".pcx",   "PDF":  ".pdf",	    "MSP":  ".msp",   "Palm": ".palm",  "PCD":  ".pcd",   "PCX":  ".pcx",   "PDF":  ".pdf",
    "PNG":  ".png",   "PPM":  ".ppm",   "PSD":  ".psd",   "SGI":  ".rgb",   "SUN":  ".ras",	    "PNG":  ".png",   "PPM":  ".ppm",   "PSD":  ".psd",   "SGI":  ".rgb",   "SUN":  ".ras",
    "TGA":  ".tga",   "TIFF": ".tiff",  "WMF":  ".wmf",   "XBM":  ".xbm",   "XPM":  ".xpm",	    "TGA":  ".tga",   "TIFF": ".tiff",  "WMF":  ".wmf",   "XBM":  ".xbm",   "XPM":  ".xpm",
    "MPO":  ".jpg",  # Pillow mislabels some jpeg images as MPO files
}	}




def get_image_extension(img):	def get_image_extension(img):
    if img.format in IMAGE_EXTENSIONS:	    if img.format in IMAGE_EXTENSIONS:
        return IMAGE_EXTENSIONS[img.format]	        return IMAGE_EXTENSIONS[img.format]
    else:	    else:
        for ext, format in PIL.Image.EXTENSION.iteritems():	        for ext, format in six.iteritems(PIL.Image.EXTENSION):
            if format == img.format:	            if format == img.format:
                return ext	                return ext
        # Our fallback is the PIL format name in lowercase,	        # Our fallback is the PIL format name in lowercase,
        # which is probably the file extension	        # which is probably the file extension
        return ".%s" % img.format.lower()	        return ".%s" % img.format.lower()


def is_transparent(image):
    """
    Check to see if an image is transparent.
    """
    if not isinstance(image, PIL.Image.Image):
        # Can only deal with PIL images, fall back to the assumption that that
        # it's not transparent.
        return False
    return (image.mode in ('RGBA', 'LA') or
            (image.mode == 'P' and 'transparency' in image.info))


def exif_orientation(im):
    """
    Rotate and/or flip an image to respect the image's EXIF orientation data.
    """
    try:
        exif = im._getexif()
    except (AttributeError, IndexError, KeyError, IOError):
        exif = None
    if exif:
        orientation = exif.get(0x0112)
        if orientation == 2:
            im = im.transpose(PIL.Image.FLIP_LEFT_RIGHT)
        elif orientation == 3:
            im = im.rotate(180)
        elif orientation == 4:
            im = im.transpose(PIL.Image.FLIP_TOP_BOTTOM)
        elif orientation == 5:
            im = im.rotate(-90).transpose(PIL.Image.FLIP_LEFT_RIGHT)
        elif orientation == 6:
            im = im.rotate(-90)
        elif orientation == 7:
            im = im.rotate(90).transpose(PIL.Image.FLIP_LEFT_RIGHT)
        elif orientation == 8:
            im = im.rotate(90)
    return im


def correct_colorspace(im, bw=False):
    """
    Convert images to the correct color space.
    bw
        Make the thumbnail grayscale (not really just black & white).
    """
    if bw:
        if im.mode in ('L', 'LA'):
            return im
        if is_transparent(im):
            return im.convert('LA')
        else:
            return im.convert('L')

    if im.mode in ('L', 'RGB'):
        return im

    return im.convert('RGB')


def is_animated_gif(im):
    info = getattr(im, 'info', None) or {}
    return bool((im.format == 'GIF' or not im.format) and info.get('extension'))


def has_animated_gif_support():
    return bool(CROPDUSTER_GIFSICLE_PATH)


def process_image(im, save_filename=None, callback=lambda i: i, nq=0, save_params=None):
    is_animated = is_animated_gif(im)
    images = [im]

    if is_animated:
        if not CROPDUSTER_GIFSICLE_PATH:
            warnings.warn(
                u"This server does not have animated gif support; your uploaded image "
                u"has been made static.")
        else:
            images = [GifsicleImage(im)]

    new_images = [callback(i) for i in images]

    if is_animated and not save_filename:
        raise Exception("Animated gifs must be saved on each processing.")

    if save_filename:
        save_params = save_params or {}
        if im.format == 'JPEG':
            save_params.setdefault('quality', get_jpeg_quality(new_images[0].size[0], new_images[0].size[1]))
        if im.format in ('JPEG', 'PNG') and JPEG_SAVE_ICC_SUPPORTED:
            save_params.setdefault('icc_profile', im.info.get('icc_profile'))
        img = new_images[0]
        buf = BytesIO()
        img.save(buf, format=im.format, **save_params)
        with default_storage.open(save_filename, 'wb') as f:
            f.write(buf.getvalue())
        with default_storage.open(save_filename, mode='rb') as f:
            content = f.read()
            pil_image = PIL.Image.open(BytesIO(content))
        pil_image.filename = save_filename
        return pil_image

    return new_images[0]


def smart_resize(im, final_w, final_h):
    """
    Resizes a given image in multiple steps to ensure maximum quality and performance
    :param im: PIL.Image instance the image to be resized
    :param final_w: int the intended final width of the image
    :param final_h: int the intended final height of the image
    """

    (orig_w, orig_h) = im.size
    if orig_w <= final_w and orig_h <= final_h:
        # If the image is already the right size, don't change it
        return im

    # Pillow 2.7.0 greatly improved the bicubic resize algorithm, which makes
    # our multiple-step resizing unnecessary
    pillow_version = getattr(PIL, '__version__', None)
    if pillow_version and LooseVersion(pillow_version) >= LooseVersion('2.7.0'):
        return im.resize((final_w, final_h), PIL.Image.BICUBIC)

    # Attempt to resize the image 1/8, 2/8, such that it is at least 1.5x bigger
    # than the final size
    # (Libjpg-Turbo has optimizations for resizing images by a ratio of eights)
    (goal_w, goal_h) = (final_w * 1.5, final_h * 1.5)
    # Ratios from 1/8, 2/8... 7/8
    for i in xrange(1, 8):
        ratio = i / 8
        scaled_w = orig_w * ratio
        scaled_h = orig_h * ratio
        if scaled_w >= goal_w and scaled_h >= goal_h:

            # The image may need to be cropped slightly to ensure an even
            # size reduction
            crop_w = orig_w % 8
            crop_h = orig_h % 8
            if not crop_w or not crop_h:
                im.crop((math.floor(crop_w / 2),
                         math.floor(crop_h / 2),
                         orig_w - math.ceil(crop_w / 2),
                         orig_h - math.ceil(crop_h / 2)))
                (orig_w, orig_h) = im.size

            # Resize part of the way using the fastest algorithm
            im = im.resize((int(orig_w * ratio), int(orig_w * ratio)),
                           PIL.Image.NEAREST)
            break

    # Return the image with the final resizing done at best quality
    return im.resize((final_w, final_h), PIL.Image.ANTIALIAS)
  20  
cropduster/utils/jsonutils.py
@@ -1,9 +1,15 @@
from jsonutil import jsonutil	import json
from django.utils import six
from django.utils.six.moves import filter

from cropduster.resizing import Size	from cropduster.resizing import Size




__all__ = ('dumps', 'loads')


def json_default(obj):	def json_default(obj):
    if callable(getattr(obj, '__serialize__', None)):	    if six.callable(getattr(obj, '__serialize__', None)):
        dct = obj.__serialize__()	        dct = obj.__serialize__()
        module = obj.__module__	        module = obj.__module__
        if module == '__builtin__':	        if module == '__builtin__':
@@ -24,22 +30,26 @@ def object_hook(dct):
    if dct.get('__type__') in ['Size', 'cropduster.resizing.Size']:	    if dct.get('__type__') in ['Size', 'cropduster.resizing.Size']:
        return Size(	        return Size(
            name=dct.get('name'),	            name=dct.get('name'),
            label=dct.get('label'),
            w=dct.get('w'),	            w=dct.get('w'),
            h=dct.get('h'),	            h=dct.get('h'),
            min_w=dct.get('min_w'),	            min_w=dct.get('min_w'),
            min_h=dct.get('min_h'),	            min_h=dct.get('min_h'),
            max_w=dct.get('max_w'),	            max_w=dct.get('max_w'),
            max_h=dct.get('max_h'),	            max_h=dct.get('max_h'),
            retina=dct.get('retina'),	            retina=dct.get('retina'),
            auto=dct.get('auto'))	            auto=dct.get('auto'),
            required=dct.get('required'))
    return dct	    return dct




def dumps(obj, *args, **kwargs):	def dumps(obj, *args, **kwargs):
    kwargs.setdefault('default', json_default)	    kwargs.setdefault('default', json_default)
    return jsonutil.dumps(obj, *args, **kwargs)	    return json.dumps(obj, *args, **kwargs)




def loads(s, *args, **kwargs):	def loads(s, *args, **kwargs):
    if isinstance(s, six.binary_type):
        s = s.decode('utf-8')
    kwargs.setdefault('object_hook', object_hook)	    kwargs.setdefault('object_hook', object_hook)
    return jsonutil.loads(s, *args, **kwargs)	    return json.loads(s, *args, **kwargs)
  56  
cropduster/utils/paths.py
@@ -1,19 +1,15 @@
from __future__ import unicode_literals

import os	import os
import re	import re


from django.core.files.storage import default_storage, FileSystemStorage
from django.conf import settings	from django.conf import settings
from django.db.models.fields.files import FileField	from django.db.models.fields.files import FileField
from django.utils import six




__all__ = ('get_upload_foldername', 'get_media_path', 'get_relative_media_url')	__all__ = ('get_upload_foldername')


MEDIA_ROOT = os.path.abspath(settings.MEDIA_ROOT)	

re_media_root = re.compile(r'^%s' % re.escape(MEDIA_ROOT))	
re_media_url = re.compile(r'^%s' % re.escape(settings.MEDIA_URL))	
re_url_slashes = re.compile(r'(?:\A|(?<=/))/')	
re_path_slashes = re.compile(r'(?<=/)/')	




def get_upload_foldername(file_name, upload_to='%Y/%m'):	def get_upload_foldername(file_name, upload_to='%Y/%m'):
@@ -23,28 +19,24 @@ def get_upload_foldername(file_name, upload_to='%Y/%m'):
        file_name = 'no_name'	        file_name = 'no_name'
    filename = file_field.generate_filename(None, file_name)	    filename = file_field.generate_filename(None, file_name)
    filename = re.sub(r'[_\-]+', '_', filename)	    filename = re.sub(r'[_\-]+', '_', filename)

    if six.PY2 and isinstance(filename, unicode):
        filename = filename.encode('utf-8')

    root_dir = os.path.splitext(filename)[0]	    root_dir = os.path.splitext(filename)[0]
    root_dir = dir_name = os.path.join(settings.MEDIA_ROOT, root_dir)	    parent_dir, _, basename = root_dir.rpartition('/')
    image_dir = ''
    i = 1	    i = 1
    while os.path.exists(dir_name):	    dir_name = basename
        dir_name = u'%s-%d' % (root_dir, i)	    while not image_dir:
        i += 1	        try:
    os.makedirs(dir_name)	            sub_dirs, _ = default_storage.listdir(parent_dir)
    return dir_name	            while dir_name in sub_dirs:

                dir_name = "%s-%d" % (basename, i)

                i += 1
def get_media_path(url):	        except OSError:
    """Determine media URL's system file."""	            os.makedirs(os.path.join(settings.MEDIA_ROOT, parent_dir))
    path = MEDIA_ROOT + '/' + re_media_url.sub('', url)	        else:
    return re_path_slashes.sub('', path)	            image_dir = os.path.join(parent_dir, dir_name)



    return image_dir
def get_relative_media_url(path, clean_slashes=True):	
    """Determine system file's media URL without MEDIA_URL prepended."""	
    if path.startswith(settings.MEDIA_URL):	
        url = re_media_url.sub('', path)	
    else:	
        url = re_media_root.sub('', path)	
    if clean_slashes:	
        url = re_url_slashes.sub('', url)	
    return url	
  11  
cropduster/utils/sizes.py
@@ -1,5 +1,7 @@
from __future__ import division	from __future__ import division


from django.utils import six

from . import jsonutils as json	from . import jsonutils as json
from ..resizing import Size	from ..resizing import Size


@@ -10,14 +12,15 @@
def get_min_size(sizes):	def get_min_size(sizes):
    """Determine the minimum required width & height from a list of sizes."""	    """Determine the minimum required width & height from a list of sizes."""
    min_w, min_h = 0, 0	    min_w, min_h = 0, 0
    if sizes == u'null':	    if sizes == 'null':
        return (0, 0)	        return (0, 0)
    if isinstance(sizes, basestring):	    if isinstance(sizes, six.string_types):
        sizes = json.loads(sizes)	        sizes = json.loads(sizes)
    if not sizes:	    if not sizes:
        return (0, 0)	        return (0, 0)
    # The min width and height for the image = the largest w / h of the sizes	    # The min width and height for the image = the largest w / h of the sizes
    for size in Size.flatten(sizes):	    for size in Size.flatten(sizes):
        min_w = max(size.min_w, min_w)	        if size.required:
        min_h = max(size.min_h, min_h)	            min_w = max(size.min_w, min_w)
            min_h = max(size.min_h, min_h)
    return (min_w, min_h)	    return (min_w, min_h)
 60  
cropduster/utils/thumbs.py
@@ -0,0 +1,60 @@
from ..resizing import Crop
from ..exceptions import CropDusterException


class DummyImage(object):
    def __init__(self, image):
        self.size = [image.width, image.height]


def set_as_auto_crop(thumb, reference_thumb, force=False):
    """
    Sometimes you need to move crop sizes into different crop groups. This
    utility takes a Thumb and a new reference thumb that will become its
    parent.
    This function can be destructive so, by default, it does not re-set the
    parent crop if the new crop box is different than the old crop box.
    """
    dummy_image = DummyImage(thumb.image)
    current_best_fit = Crop(thumb.get_crop_box(), dummy_image).best_fit(thumb.width, thumb.height)
    new_best_fit = Crop(reference_thumb.get_crop_box(), dummy_image).best_fit(thumb.width, thumb.height)

    if current_best_fit.box != new_best_fit.box and not force:
        raise CropDusterException("Current image crop based on '%s' is "
            "different than new image crop based on '%s'." % (thumb.reference_thumb.name, reference_thumb.name))

    if reference_thumb.reference_thumb:
        raise CropDusterException("Reference thumbs cannot have reference thumbs.")

    if not thumb.reference_thumb:
        thumb.crop_w = None
        thumb.crop_h = None
        thumb.crop_x = None
        thumb.crop_y = None
    thumb.reference_thumb = reference_thumb
    thumb.save()


def unset_as_auto_crop(thumb):
    """
    Crop information is normalized on the parent Thumb row so auto-crops do not
    have crop height/width/x/y associated with them.
    This function takes a Thumb as an argument, generates the best_fit from
    its reference_thumb, sets the relevant geometry, and clears the original
    reference_thumb foreign key.
    """
    if not thumb.reference_thumb:
        return

    reference_thumb_box = thumb.reference_thumb.get_crop_box()
    crop = Crop(reference_thumb_box, DummyImage(thumb.image))
    best_fit = crop.best_fit(thumb.width, thumb.height)

    thumb.reference_thumb = None
    thumb.crop_w = best_fit.box.w
    thumb.crop_h = best_fit.box.h
    thumb.crop_x = best_fit.box.x1
    thumb.crop_y = best_fit.box.y1
    thumb.save()
 189  
cropduster/views/__init__.py
@@ -1,27 +1,65 @@
"""
View functions used by the cropduster dialog.
index() (defined in CropDusterIndex)
====================================
The initial page that a user sees when clicking on the "Upload Image" button.
This view renders the form used to interact with upload() and crop() via ajax.
standalone() (defined in CropDusterStandalone)
==============================================
Subclass of CropDusterIndex used for "standalone mode", which saves minimal
information in the database and instead stores information about the original
image and crop dimensions in metadata on the generated image. The intended use
case for standalone mode is a dialog in a WYSIWYG editor.
upload() / crop()
=================
Both upload() and crop() interact with the index page's html in the same way:
they receive a POST with data from the django forms and formsets, create new
image and thumb instances (respectively), and return a JSON object that map
back onto fields on the index page's forms / formsets.
"""
from __future__ import division	from __future__ import division


from io import BytesIO
import os	import os
import copy	import copy
import shutil	import shutil
import time


import django
from django.conf import settings	from django.conf import settings
from django.contrib.auth.decorators import login_required
from django.contrib.contenttypes.models import ContentType	from django.contrib.contenttypes.models import ContentType
from django.core.files.storage import default_storage
from django.db.models import Q	from django.db.models import Q
from django.forms.models import modelformset_factory	from django.forms.models import modelformset_factory
from django.http import HttpResponse	from django.http import HttpResponse
from django.shortcuts import render_to_response	from django.shortcuts import render
from django.template import RequestContext	from django.template import RequestContext
from django.utils.decorators import method_decorator
from django.utils.encoding import force_text
from django.utils.functional import cached_property	from django.utils.functional import cached_property
from django.utils import six
from django.utils.six.moves import filter, map, zip
from django.views.decorators.csrf import csrf_exempt	from django.views.decorators.csrf import csrf_exempt


import PIL.Image	import PIL.Image


from generic_plus.utils import get_relative_media_url

from cropduster.files import ImageFile	from cropduster.files import ImageFile
from cropduster.models import Thumb, Size, StandaloneImage, Image	from cropduster.models import Thumb, Size, StandaloneImage, Image
from cropduster.settings import (	from cropduster.settings import (
    CROPDUSTER_PREVIEW_WIDTH as PREVIEW_WIDTH,	    CROPDUSTER_PREVIEW_WIDTH as PREVIEW_WIDTH,
    CROPDUSTER_PREVIEW_HEIGHT as PREVIEW_HEIGHT)	    CROPDUSTER_PREVIEW_HEIGHT as PREVIEW_HEIGHT)
from cropduster.utils import json, get_relative_media_url	from cropduster.utils import (
    json, is_animated_gif, has_animated_gif_support, process_image)
from cropduster.exceptions import json_error, CropDusterResizeException, full_exc_info	from cropduster.exceptions import json_error, CropDusterResizeException, full_exc_info


from .base import View	from .base import View
@@ -35,6 +73,7 @@ class CropDusterIndex(View):


    is_standalone = False	    is_standalone = False


    @method_decorator(login_required)
    def dispatch(self, request, *args, **kwargs):	    def dispatch(self, request, *args, **kwargs):
        self.request = request	        self.request = request
        self.upload_to = self.request.GET.get('upload_to') or None	        self.upload_to = self.request.GET.get('upload_to') or None
@@ -94,7 +133,8 @@ def thumbs(self):
        else:	        else:
            thumbs = Thumb.objects.filter(pk__in=thumb_ids)	            thumbs = Thumb.objects.filter(pk__in=thumb_ids)
        thumb_dict = dict([(t.name, t) for t in thumbs])	        thumb_dict = dict([(t.name, t) for t in thumbs])
        ordered_thumbs = [thumb_dict.get(s.name, Thumb(name=s.name)) for s in self.sizes]	        ordered_thumbs = [
            thumb_dict.get(s.name, Thumb(name=s.name)) for s in self.sizes if not s.is_alias]
        return FakeQuerySet(ordered_thumbs, thumbs)	        return FakeQuerySet(ordered_thumbs, thumbs)


    @cached_property	    @cached_property
@@ -106,17 +146,23 @@ def orig_image(self):


    def get(self, *args, **kwargs):	    def get(self, *args, **kwargs):
        orig_image = self.orig_image	        orig_image = self.orig_image
        orig_w = getattr(orig_image, 'width', None) or 0	        try:
        orig_h = getattr(orig_image, 'height', None) or 0	            orig_w = getattr(orig_image, 'width', None) or 0
            orig_h = getattr(orig_image, 'height', None) or 0
            orig_image_name = getattr(orig_image, 'name', None)
        except Exception:
            # If original image not found, allow it to be re-uploaded
            orig_w, orig_h = 0, 0
            orig_image_name = None


        initial = {	        initial = {
            'standalone': self.is_standalone,	            'standalone': self.is_standalone,
            'sizes': json.dumps(self.sizes),	            'sizes': json.dumps(self.sizes),
            'thumbs': json.dumps(dict([	            'thumbs': json.dumps(dict([
                (t['name'], t)	                (t['name'], t)
                for t in self.thumbs.queryset.values('id', 'name', 'width', 'height')])),	                for t in self.thumbs.queryset.values('id', 'name', 'width', 'height')])),
            'image_id': getattr(self.db_image, 'pk', None),	            'image_id': getattr(self.db_image, 'pk', None) if orig_image else None,
            'orig_image': getattr(orig_image, 'name', None),	            'orig_image': orig_image_name,
            'orig_w': orig_w,	            'orig_w': orig_w,
            'orig_h': orig_h,	            'orig_h': orig_h,
        }	        }
@@ -139,7 +185,8 @@ def get(self, *args, **kwargs):
                'changed': False,	                'changed': False,
            })	            })


        return render_to_response('cropduster/upload.html', RequestContext(self.request, {	        return render(self.request, 'cropduster/upload.html', {
            'django_is_gte_19': (django.VERSION[:2] >= (1, 9)),
            'is_popup': True,	            'is_popup': True,
            'orig_image': '',	            'orig_image': '',
            'parent_template': get_admin_base_template(),	            'parent_template': get_admin_base_template(),
@@ -155,69 +202,86 @@ def get(self, *args, **kwargs):
            }),	            }),
            'crop_form': CropForm(initial=initial, prefix='crop'),	            'crop_form': CropForm(initial=initial, prefix='crop'),
            'thumb_formset': thumb_formset,	            'thumb_formset': thumb_formset,
        }))	        })






index = CropDusterIndex.as_view()	index = CropDusterIndex.as_view()




@csrf_exempt	@csrf_exempt
@login_required
def upload(request):	def upload(request):
    if request.method == 'GET':	    if request.method == 'GET':
        return index(request)	        return index(request)


    # The data we'll be returning as JSON
    data = {
        'warning': [],
    }

    form = UploadForm(request.POST, request.FILES)	    form = UploadForm(request.POST, request.FILES)


    if not form.is_valid():	    if not form.is_valid():
        errors = form['image'].errors or form.errors	        errors = form['image'].errors or form.errors
        return json_error(request, 'upload', action="uploading file",	        return json_error(request, 'upload', action="uploading file",
                errors=[unicode(errors)])	                errors=[force_text(errors)])


    form_data = form.cleaned_data	    form_data = form.cleaned_data
    is_standalone = bool(form_data.get('standalone'))


    orig_file_path = form_data['image'].name	    orig_file_path = form_data['image'].name
    if six.PY2 and isinstance(orig_file_path, six.text_type):
        orig_file_path = orig_file_path.encode('utf-8')
    orig_image = get_relative_media_url(orig_file_path)	    orig_image = get_relative_media_url(orig_file_path)
    img = PIL.Image.open(orig_file_path)	
    with default_storage.open(orig_image, mode='rb') as f:
        img = PIL.Image.open(BytesIO(f.read()))
        img.filename = f.name

    (w, h) = (orig_w, orig_h) = img.size	    (w, h) = (orig_w, orig_h) = img.size


    if is_animated_gif(img) and not has_animated_gif_support():
        data['warning'].append(
            u"This server does not have animated gif support; your uploaded image "
            u"has been made static.")

    tmp_image = Image(image=orig_image)	    tmp_image = Image(image=orig_image)
    preview_w = form_data.get('preview_width') or PREVIEW_WIDTH	    preview_w = form_data.get('preview_width') or PREVIEW_WIDTH
    preview_h = form_data.get('preview_height') or PREVIEW_HEIGHT	    preview_h = form_data.get('preview_height') or PREVIEW_HEIGHT


    # First pass resize if it's too large	    # First pass resize if it's too large
    resize_ratio = min(preview_w / w, preview_h / h)	    resize_ratio = min(preview_w / w, preview_h / h)
    if resize_ratio < 1:	
        w = int(round(w * resize_ratio))	
        h = int(round(h * resize_ratio))	
        preview_img = img.resize((w, h), PIL.Image.ANTIALIAS)	
    else:	
        preview_img = img	


    preview_file_path = tmp_image.get_image_path('_preview')	    def fit_preview(im):

        (w, h) = im.size
    img_save_params = {}	        if resize_ratio < 1:
    if preview_img.format == 'JPEG':	            w = int(round(w * resize_ratio))
        img_save_params['quality'] = 95	            h = int(round(h * resize_ratio))
            preview_img = im.resize((w, h), PIL.Image.ANTIALIAS)
        else:
            preview_img = im
        return preview_img


    preview_img.save(preview_file_path, **img_save_params)	    if not is_standalone:
        preview_file_path = tmp_image.get_image_path('_preview')
        process_image(img, preview_file_path, fit_preview)


    data = {	    data.update({
        'crop': {	        'crop': {
            'orig_image': orig_image,	            'orig_image': orig_image,
            'orig_w': orig_w,	            'orig_w': orig_w,
            'orig_h': orig_h,	            'orig_h': orig_h,
            'image_id': None,
        },	        },
        'url': tmp_image.get_image_url('_preview'),	        'url': tmp_image.get_image_url('_preview'),
        'orig_image': orig_image,	        'orig_image': orig_image,
        'orig_w': orig_w,	        'orig_w': orig_w,
        'orig_h': orig_h,	        'orig_h': orig_h,
        'width': w,	        'width': w,
        'height': h,	        'height': h,
    }	    })
    if not form_data.get('standalone'):	    if not is_standalone:
        return HttpResponse(json.dumps(data), mimetype='application/json')	        return HttpResponse(json.dumps(data), content_type='application/json')


    size = Size('crop', w=img.size[0], h=img.size[1])	    size = Size('crop', w=img.size[0], h=img.size[1])


@@ -233,7 +297,20 @@ def upload(request):


    if not cropduster_image.image:	    if not cropduster_image.image:
        cropduster_image.image = orig_image	        cropduster_image.image = orig_image
    thumb = cropduster_image.save_size(size, standalone=True)	        cropduster_image.save()
    elif cropduster_image.image.name != orig_image:
        data['crop']['orig_image'] = data['orig_image'] = cropduster_image.image.name
        data['url'] = cropduster_image.get_image_url('_preview')

    with cropduster_image.image as f:
        f.open()
        img = PIL.Image.open(BytesIO(f.read()))
        img.filename = f.name
    preview_file_path = cropduster_image.get_image_path('_preview')
    if not default_storage.exists(preview_file_path):
        process_image(img, preview_file_path, fit_preview)

    thumb = cropduster_image.save_size(size, standalone=True, commit=False)


    sizes = form_data.get('sizes') or []	    sizes = form_data.get('sizes') or []
    if len(sizes) == 1:	    if len(sizes) == 1:
@@ -259,10 +336,11 @@ def upload(request):
        'image_id': cropduster_image.pk,	        'image_id': cropduster_image.pk,
        'sizes': json.dumps([size]),	        'sizes': json.dumps([size]),
    })	    })
    return HttpResponse(json.dumps(data), mimetype='application/json')	    return HttpResponse(json.dumps(data), content_type='application/json')




@csrf_exempt	@csrf_exempt
@login_required
def crop(request):	def crop(request):
    if request.method == "GET":	    if request.method == "GET":
        return json_error(request, 'crop', action="cropping image",	        return json_error(request, 'crop', action="cropping image",
@@ -274,9 +352,17 @@ def crop(request):
                log=True, exc_info=full_exc_info())	                log=True, exc_info=full_exc_info())


    crop_data = copy.deepcopy(crop_form.cleaned_data)	    crop_data = copy.deepcopy(crop_form.cleaned_data)
    db_image = Image(image=crop_data['orig_image'])	
    if crop_data.get('image_id'):
        db_image = Image.objects.get(pk=crop_data['image_id'])
    else:
        db_image = Image(image=crop_data['orig_image'])

    try:	    try:
        pil_image = PIL.Image.open(db_image.image.path)	        with db_image.image as f:
            f.open()
            pil_image = PIL.Image.open(BytesIO(f.read()))
            pil_image.filename = f.name
    except IOError:	    except IOError:
        pil_image = None	        pil_image = None


@@ -299,6 +385,13 @@ def crop(request):


    standalone_mode = crop_data['standalone']	    standalone_mode = crop_data['standalone']


    # Address a standalone mode issue where, because the thumbs don't have a pk value,
    # Django no longer returns them in Formset.save() if they are in initial_forms
    if standalone_mode and not cropped_thumbs and len(thumb_formset.initial_forms):
        thumb_form = thumb_formset.initial_forms[0]
        obj = thumb_form.instance
        cropped_thumbs = [thumb_formset.save_existing(thumb_form, obj, commit=False)]

    for i, (thumb, thumb_form) in enumerate(zip(cropped_thumbs, thumb_formset)):	    for i, (thumb, thumb_form) in enumerate(zip(cropped_thumbs, thumb_formset)):
        changed_fields = set(thumb_form.changed_data) - non_model_fields	        changed_fields = set(thumb_form.changed_data) - non_model_fields
        thumb_form._changed_data = list(changed_fields)	        thumb_form._changed_data = list(changed_fields)
@@ -316,7 +409,7 @@ def crop(request):
                new_thumbs = db_image.save_size(size, thumb, tmp=True, standalone=standalone_mode)	                new_thumbs = db_image.save_size(size, thumb, tmp=True, standalone=standalone_mode)
            except CropDusterResizeException as e:	            except CropDusterResizeException as e:
                return json_error(request, 'crop',	                return json_error(request, 'crop',
                                  action="saving size", errors=[unicode(e)])	                                  action="saving size", errors=[force_text(e)])


            if not new_thumbs:	            if not new_thumbs:
                continue	                continue
@@ -336,18 +429,22 @@ def crop(request):
                'url': db_image.get_image_url(thumb.name),	                'url': db_image.get_image_url(thumb.name),
            })	            })


            for name, new_thumb in new_thumbs.iteritems():	            for name, new_thumb in six.iteritems(new_thumbs):
                thumb_data = dict([(k, getattr(new_thumb, k)) for k in json_thumb_fields])	                thumb_data = dict([(k, getattr(new_thumb, k)) for k in json_thumb_fields])
                thumb_data['url'] = db_image.get_image_url(name, tmp=not(new_thumb.image_id))
                crop_data['thumbs'].update({name: thumb_data})	                crop_data['thumbs'].update({name: thumb_data})
                if new_thumb.reference_thumb_id:	                if new_thumb.reference_thumb_id:
                    continue	                    continue
                thumbs_data[i]['thumbs'].update({name: thumb_data})	                thumbs_data[i]['thumbs'].update({name: thumb_data})
        elif thumb.pk and thumb.name and thumb.crop_w and thumb.crop_h:	        elif thumb.pk and thumb.name and thumb.crop_w and thumb.crop_h:
            thumb_path = db_image.get_image_path(thumb.name, tmp=False)	            thumb_path = db_image.get_image_path(thumb.name, tmp=False)
            tmp_thumb_path = db_image.get_image_path(thumb.name, tmp=True)	            tmp_thumb_path = db_image.get_image_path(thumb.name, tmp=True)
            if os.path.exists(thumb_path):	
                if not thumb_form.cleaned_data.get('changed') or not os.path.exists(tmp_thumb_path):	            if default_storage.exists(thumb_path):
                    shutil.copy(thumb_path, tmp_thumb_path)	                if not thumb_form.cleaned_data.get('changed') or not default_storage.exists(tmp_thumb_path):
                    with default_storage.open(thumb_path) as f:
                        with default_storage.open(tmp_thumb_path, 'wb') as tmp_file:
                            tmp_file.write(f.read())


        if not thumb.pk and not thumb.crop_w and not thumb.crop_h:	        if not thumb.pk and not thumb.crop_w and not thumb.crop_h:
            if not len(thumbs_with_crops):	            if not len(thumbs_with_crops):
@@ -361,14 +458,28 @@ def crop(request):
                    'crop_w': best_fit.box.w,	                    'crop_w': best_fit.box.w,
                    'crop_h': best_fit.box.h,	                    'crop_h': best_fit.box.h,
                    'changed': True,	                    'changed': True,
                    'id': None,
                })	                })


    for thumb_data in thumbs_data:	    for thumb_data in thumbs_data:
        if isinstance(thumb_data['id'], Thumb):	        if isinstance(thumb_data['id'], Thumb):
            thumb_data['id'] = thumb_data['id'].pk	            thumb_data['id'] = thumb_data['id'].pk


    preview_url = db_image.get_image_url('_preview')
    preview_w = PREVIEW_WIDTH
    preview_h = PREVIEW_HEIGHT
    orig_width, orig_height = crop_data['orig_w'], crop_data['orig_h']
    if (orig_width and orig_height):
        resize_ratio = min(PREVIEW_WIDTH / float(orig_width), PREVIEW_HEIGHT / float(orig_height))
        if resize_ratio < 1:
            preview_w = int(round(orig_width * resize_ratio))
            preview_h = int(round(orig_height * resize_ratio))

    return HttpResponse(json.dumps({	    return HttpResponse(json.dumps({
        'crop': crop_data,	        'crop': crop_data,
        'thumbs': thumbs_data,	        'thumbs': thumbs_data,
        'initial': True,	        'initial': True,
    }), mimetype='application/json')	        'preview_url': preview_url,
        'preview_w': preview_w,
        'preview_h': preview_h
    }), content_type='application/json')
 8  
cropduster/views/base.py
 68  
cropduster/views/forms.py
 18  
cropduster/views/utils.py
 210  
cropduster/widgets.py
This file was deleted.

 2  
cropduster3/__init__.py
This file was deleted.

 29  
cropduster3/admin.py
This file was deleted.

 28  
cropduster3/media/css/CropDuster.css
This file was deleted.

 BIN  
cropduster3/media/css/Jcrop.gif
Binary file not shown.
 60  
cropduster3/media/css/admin.cropduster.css
This file was deleted.

 BIN  
cropduster3/media/css/blank.gif
Binary file not shown.
 86  
cropduster3/media/css/jquery.Jcrop.css
This file was deleted.

 28  
cropduster3/media/css/jquery.Jcrop.min.css
This file was deleted.

 BIN  
cropduster3/media/img/blank.gif
Binary file not shown.
 BIN  
cropduster3/media/img/cropduster_icon_upload_hover.png
Binary file not shown.
 BIN  
cropduster3/media/img/cropduster_icon_upload_select.png
Binary file not shown.
 BIN  
cropduster3/media/img/cropduster_icon_upload_select_small.png
Binary file not shown.
 BIN  
cropduster3/media/img/progressbar.gif
Binary file not shown.
 183  
cropduster3/media/js/CropDuster.js
This file was deleted.

 102  
cropduster3/media/js/admin.cropduster.js
This file was deleted.

 13  
cropduster3/media/js/init.js
This file was deleted.

 4  
cropduster3/media/js/jquery-1.7.2.min.js
This file was deleted.

 1,695  
cropduster3/media/js/jquery.Jcrop.js
This file was deleted.

 22  
cropduster3/media/js/jquery.Jcrop.min.js
This file was deleted.

 60  
cropduster3/media/js/jquery.class.js
This file was deleted.

 123  
cropduster3/media/js/jquery.color.js
This file was deleted.

 925  
cropduster3/media/js/jquery.form.js
This file was deleted.

 4  
cropduster3/media/js/jquery.min.js
This file was deleted.

 108  
cropduster3/media/js/jquery.progressbar.js
This file was deleted.

 20  
cropduster3/media/js/jquery.progressbar.min.js
This file was deleted.

 483  
cropduster3/media/js/json2.js
This file was deleted.

 1,036  
cropduster3/media/js/jsrender.js
This file was deleted.

 164  
cropduster3/media/js/upload.js
This file was deleted.

 809  
cropduster3/models.py
This file was deleted.

 20  
cropduster3/settings.py
This file was deleted.

 71  
cropduster3/templates/admin/complete.html
This file was deleted.

 203  
cropduster3/templates/admin/crop_images.html
This file was deleted.

 45  
cropduster3/templates/admin/inline.html
This file was deleted.

 103  
cropduster3/templates/admin/inline_tabular.html
This file was deleted.

 143  
cropduster3/templates/admin/upload.html
This file was deleted.

 50  
cropduster3/templates/admin/upload_image.html
This file was deleted.

 11  
cropduster3/templates/templatetags/html4.html
This file was deleted.

 11  
cropduster3/templates/templatetags/image.html
This file was deleted.

 54  
cropduster3/templatetags/cropdusteradmin.py
This file was deleted.

 30  
cropduster3/templatetags/cropdusterimages.py
This file was deleted.

 15  
cropduster3/templatetags/cropdustermedia.py
This file was deleted.

 9  
cropduster3/urls.py
This file was deleted.

 166  
cropduster3/utils.py
This file was deleted.

 362  
cropduster3/views.py
This file was deleted.

 93  
cropduster3/widgets.py
This file was deleted.

 192  
docs/Makefile
 5  
docs/changelog.rst
 296  
docs/conf.py
 16  
docs/customization.rst
 67  
docs/how_it_works.rst
 39  
docs/index.rst
 112  
docs/quickstart.rst
 6  
pytest.ini
@@ -0,0 +1,6 @@
[pytest]
DJANGO_SETTINGS_MODULE = tests.settings
addopts = --tb=short --create-db --cov=cropduster
django_find_project = false
python_files = tests.py test_*.py *_tests.py
testpaths = tests
 11  
setup.cfg
@@ -0,0 +1,11 @@
[bumpversion]
current_version = 4.13.0
commit = True
tag = True
message = v{new_version} [ci skip]

[bdist_wheel]
universal = 1

[bumpversion:file:setup.py]

 31  
setup.py
 100644 ??? 100755
@@ -12,23 +12,32 @@
    name='django-cropduster',	    name='django-cropduster',
    version=__import__('cropduster').__version__,	    version=__import__('cropduster').__version__,
    author='The Atlantic',	    author='The Atlantic',
    author_email='atmoprogrammers@theatlantic.com',	    author_email='programmers@theatlantic.com',
    url='http://github.com/theatlantic/django-cropduster',	    url='https://github.com/theatlantic/django-cropduster',
    description='Image uploader and cropping tool',	    description='Django image uploader and cropping tool',
    packages=find_packages(),	    packages=find_packages(exclude=["tests"]),
    zip_safe=False,	    zip_safe=False,
    long_description=open('README.rst').read(),
    license='BSD',
    platforms='any',
    install_requires=[	    install_requires=[
        'Pillow',	        'Pillow',
        'jsonutil',	
        'Django>=1.2',	
        'python-xmp-toolkit',	        'python-xmp-toolkit',
        'django-generic-plus>=2.0.3',
    ],	    ],
    include_package_data=True,	    include_package_data=True,
    classifiers=[	    classifiers=[
        'Framework :: Django',	        'Development Status :: 5 - Production/Stable',
        'Environment :: Web Environment',
        'Intended Audience :: Developers',	        'Intended Audience :: Developers',
        'Intended Audience :: System Administrators',	        'Natural Language :: English',
        'Operating System :: OS Independent',	        'Operating System :: OS Independent',
        'Topic :: Software Development'	        'Framework :: Django',
    ],	        'Programming Language :: Python',
)	        "Programming Language :: Python :: 2",
        'Programming Language :: Python :: 2.7',
        'Programming Language :: Python :: 3',
        'Programming Language :: Python :: 3.4',
        'Programming Language :: Python :: 3.5',
        'Programming Language :: Python :: 3.6',
    ])
 0  
cropduster/templates/cropduster/blank.html ??? tests/__init__.py
File renamed without changes.
 8  
tests/admin.py
@@ -0,0 +1,8 @@
from django.contrib import admin
from .models import Author, Article, OptionalSizes, OrphanedThumbs


admin.site.register(Author)
admin.site.register(Article)
admin.site.register(OptionalSizes)
admin.site.register(OrphanedThumbs)
 16  
tests/conftest.py
@@ -0,0 +1,16 @@
import warnings

import pytest
from django.test import TestCase


TestCase.pytestmark = pytest.mark.django_db(transaction=True, reset_sequences=True)


@pytest.fixture(autouse=True)
def suppress_warnings():
    warnings.simplefilter("error", Warning)
    warnings.filterwarnings('ignore', message='.*?ckeditor')
    warnings.filterwarnings('ignore', message='.*?collections')
    warnings.filterwarnings('ignore', message='.*?Resampling')
    warnings.filterwarnings('ignore', message='.*?distutils')
 BIN  
tests/data/animated-duration.gif

 BIN  
tests/data/animated.gif

 BIN  
tests/data/best-fit-off-by-one-bug.png

 BIN  
tests/data/cmyk.jpg

 BIN  
tests/data/img.jpg

 BIN  
tests/data/img.png

 BIN  
tests/data/img2.jpg

 BIN  
tests/data/size-order-bug.png

 BIN  
tests/data/transparent.png

 86  
tests/helpers.py
@@ -0,0 +1,86 @@
from io import open
import tempfile
import os
import shutil
import uuid

import PIL.Image

from django.core.files.storage import default_storage
from django.core.files.base import ContentFile
from django.test import override_settings

from .utils import repr_rgb


PATH = os.path.split(__file__)[0]
ORIG_IMG_PATH = os.path.join(PATH, 'data')


class CropdusterTestCaseMediaMixin(object):

    def _pre_setup(self):
        super(CropdusterTestCaseMediaMixin, self)._pre_setup()
        self.temp_media_root = tempfile.mkdtemp(prefix='TEST_MEDIA_ROOT_')
        self.override = override_settings(MEDIA_ROOT=self.temp_media_root)
        self.override.enable()

    def _post_teardown(self):
        if hasattr(default_storage, 'bucket'):
            default_storage.bucket.objects.filter(Prefix=default_storage.location).delete()
        shutil.rmtree(self.temp_media_root)
        self.override.disable()
        super(CropdusterTestCaseMediaMixin, self)._post_teardown()

    def setUp(self):
        super(CropdusterTestCaseMediaMixin, self).setUp()

        random = uuid.uuid4().hex
        self.TEST_IMG_DIR = ORIG_IMG_PATH
        self.TEST_IMG_DIR_RELATIVE = os.path.join(random, 'data')

    def assertImageColorEqual(self, element, image):
        self.selenium.execute_script('arguments[0].scrollIntoView()', element)
        scroll_top = -1 * self.selenium.execute_script(
            'return document.body.getBoundingClientRect().top')
        tmp_file = tempfile.NamedTemporaryFile(suffix='.png')
        pixel_density = self.selenium.execute_script('return window.devicePixelRatio') or 1
        x1 = int(round(element.location['x'] + (element.size['width'] // 2.0)))
        y1 = int(round(element.location['y'] - scroll_top + (element.size['height'] // 2.0)))

        image_path = os.path.join(os.path.dirname(__file__), 'data', image)
        ref_im = PIL.Image.open(image_path).convert('RGB')
        w, h = ref_im.size
        x2, y2 = int(round(w // 2.0)), int(round(h // 2.0))
        ref_rgb = ref_im.getpixel((x2, y2))
        ref_im.close()

        def get_screenshot_rgb():
            if not self.selenium.save_screenshot(tmp_file.name):
                raise Exception("Failed to save screenshot")
            im = PIL.Image.open(tmp_file.name).convert('RGB')
            rgb = im.getpixel((x1 * pixel_density, y1 * pixel_density))
            im.close()
            return rgb

        self.wait_until(
            lambda d: get_screenshot_rgb() == ref_rgb,
            message=(
                "Colors differ: %s != %s" % (repr_rgb(ref_rgb), repr_rgb(get_screenshot_rgb()))))

    def create_unique_image(self, image):
        image_uuid = uuid.uuid4().hex

        ext = os.path.splitext(image)[1]
        image_name = os.path.join(
            self.TEST_IMG_DIR_RELATIVE, image_uuid, "original%s" % ext)
        preview_image_name = os.path.join(                                                                            
            self.TEST_IMG_DIR_RELATIVE, image_uuid, "_preview%s" % ext) 

        with open("%s/%s" % (ORIG_IMG_PATH, image), mode='rb') as f:
            default_storage.save(image_name, ContentFile(f.read()))

        with open("%s/%s" % (ORIG_IMG_PATH, image), mode='rb') as f:
            default_storage.save(preview_image_name, ContentFile(f.read()))

        return image_name
 119  
tests/models.py
@@ -0,0 +1,119 @@
from django.db import models
from django.utils.encoding import python_2_unicode_compatible

from cropduster.fields import ReverseForeignRelation
from cropduster.models import CropDusterField, Size


class Author(models.Model):
    name = models.CharField(max_length=255)
    HEADSHOT_SIZES = [
        Size('main', w=220, h=180, auto=[
            Size('thumb', w=110, h=90),
        ]),
    ]
    headshot = CropDusterField(upload_to="author/headshots/%Y/%m", sizes=HEADSHOT_SIZES,
        related_name="author_headshotset")


class Article(models.Model):
    title = models.CharField(max_length=255)
    author = models.ForeignKey(to=Author, blank=True, null=True,
        on_delete=models.SET_NULL)
    LEAD_IMAGE_SIZES = [
        Size(u'main', w=600, h=480, auto=[
            Size(u'thumb', w=110, h=90),
        ]),
        Size(u'no_height', w=600),
    ]
    ALT_IMAGE_SIZES = [
        Size(u'wide', w=600, h=300),
    ]
    lead_image = CropDusterField(upload_to="article/lead_image/%Y/%m",
                                db_column='image',
                                related_name="test_article_lead_image",
                                sizes=LEAD_IMAGE_SIZES)
    alt_image = CropDusterField(upload_to="article/alt_image/%Y/%m",
                                related_name="test_article_alt_image",
                                sizes=ALT_IMAGE_SIZES,
                                field_identifier="alt")


class OptionalSizes(models.Model):

    TEST_SIZES = [
        Size('main', w=600, h=480, auto=[
            Size('optional', w=1200, h=960, required=False),
        ])]

    slug = models.SlugField()
    image = CropDusterField(upload_to="test", sizes=TEST_SIZES)


class OrphanedThumbs(models.Model):

    TEST_SIZES = [
        Size('main', w=600, h=480, auto=[
            Size('main@2x', w=1200, h=960),
        ]),
        Size('secondary', w=600, h=480, auto=[
            Size('secondary@2x', w=1200, h=960),
        ])]

    slug = models.SlugField()
    image = CropDusterField(upload_to="test", sizes=TEST_SIZES)


class MultipleFieldsInheritanceParent(models.Model):

    slug = models.SlugField()
    image = CropDusterField(upload_to="test", sizes=[Size(u'main', w=600, h=480)])


class MultipleFieldsInheritanceChild(MultipleFieldsInheritanceParent):

    image2 = CropDusterField(upload_to="test", sizes=[Size(u'main', w=600, h=480)],
        field_identifier="2")


@python_2_unicode_compatible
class ReverseForeignRelA(models.Model):
    slug = models.SlugField()
    c = models.ForeignKey('ReverseForeignRelC', on_delete=models.CASCADE)
    a_type = models.CharField(max_length=10, choices=(
        ("x", "X"),
        ("y", "Y"),
        ("z", "Z"),
    ))

    def __str__(self):
        return self.slug


@python_2_unicode_compatible
class ReverseForeignRelB(models.Model):
    slug = models.SlugField()
    c = models.ForeignKey('ReverseForeignRelC', on_delete=models.CASCADE)

    def __str__(self):
        return self.slug


@python_2_unicode_compatible
class ReverseForeignRelC(models.Model):
    slug = models.SlugField()
    rel_a = ReverseForeignRelation(
        ReverseForeignRelA, field_name='c', limit_choices_to={'a_type': 'x'})
    rel_b = ReverseForeignRelation(ReverseForeignRelB, field_name='c')

    def __str__(self):
        return self.slug


@python_2_unicode_compatible
class ReverseForeignRelM2M(models.Model):
    slug = models.SlugField()
    m2m = models.ManyToManyField(ReverseForeignRelC)

    def __str__(self):
        return self.slug
 70  
tests/settings.py
@@ -0,0 +1,70 @@
import os
import uuid

import django
from django.core.signals import setting_changed
from django.dispatch import receiver
from django.utils.functional import lazy
from django.urls import reverse

from selenosis.settings import *


lazy_reverse = lazy(reverse, str)


if django.VERSION > (1, 11):
    MIGRATION_MODULES = {
        'auth': None,
        'contenttypes': None,
        'sessions': None,
        'cropduster': None,
    }

INSTALLED_APPS += (
    'generic_plus',
    'cropduster',
    'cropduster.standalone',
    'tests',
    'tests.standalone',
    'ckeditor',
)

ROOT_URLCONF = 'tests.urls'

TEMPLATES[0]['OPTIONS']['debug'] = True

if os.environ.get('S3') == '1':
    DEFAULT_FILE_STORAGE = 'storages.backends.s3boto3.S3Boto3Storage'
    AWS_STORAGE_BUCKET_NAME = 'ollie-cropduster-media-test-bucket-dev'
    AWS_DEFAULT_ACL = 'public-read'
    AWS_LOCATION = 'cropduster/%s/' % uuid.uuid4().hex
    AWS_S3_SIGNATURE_VERSION = 's3v4'
else:
    DEFAULT_FILE_STORAGE = 'django.core.files.storage.FileSystemStorage'

CKEDITOR_CONFIGS = {
    'default': {
        'extraPlugins': 'cropduster',
        'removePlugins': 'flash,forms,contextmenu,liststyle,table,tabletools,iframe',
        'disableAutoInline': True,
        "height": 450,
        "width": 840,
        'cropduster_uploadTo': 'ckeditor',
        'cropduster_previewSize': [570, 300],
        'cropduster_url': lazy_reverse('cropduster-standalone'),
        'cropduster_urlParams': {'max_w': 672, 'full_w': 960},
    },
}

CKEDITOR_UPLOAD_PATH = "%s/upload" % MEDIA_ROOT
CROPDUSTER_CREATE_THUMBS = True


@receiver(setting_changed)
def reload_settings(**kwargs):
    if kwargs['setting'] == 'CROPDUSTER_CREATE_THUMBS':
        from cropduster import settings as cropduster_settings
        cropduster_settings.CROPDUSTER_CREATE_THUMBS = kwargs['value']

os.makedirs(CKEDITOR_UPLOAD_PATH)
 1  
tests/standalone/__init__.py
@@ -0,0 +1 @@
default_app_config = 'tests.standalone.apps.StandaloneTestConfig'
 6  
tests/standalone/admin.py
@@ -0,0 +1,6 @@
from django.contrib import admin

from .models import Article


admin.site.register(Article)
 6  
tests/standalone/apps.py
@@ -0,0 +1,6 @@
from django.apps import AppConfig


class StandaloneTestConfig(AppConfig):
    name = 'tests.standalone'
    label = 'standalone_test'
 7  
tests/standalone/models.py
@@ -0,0 +1,7 @@
from django.db import models

from ckeditor.fields import RichTextField


class Article(models.Model):
    content = RichTextField(blank=True, config_name='default')
 194  
tests/standalone/test_admin.py
@@ -0,0 +1,194 @@
from __future__ import absolute_import

import contextlib
import re
import time
from unittest import SkipTest
import os

import django
from django.core.files.storage import default_storage
from django.test import override_settings

import PIL.Image
from selenosis import AdminSelenosisTestCase

from cropduster.models import Image, Thumb
from tests.helpers import CropdusterTestCaseMediaMixin

from .models import Article


class TestStandaloneAdmin(CropdusterTestCaseMediaMixin, AdminSelenosisTestCase):

    root_urlconf = 'tests.urls'

    @property
    def available_apps(self):
        apps = [
            'django.contrib.auth',
            'django.contrib.contenttypes',
            'django.contrib.messages',
            'django.contrib.sessions',
            'django.contrib.sites',
            'django.contrib.staticfiles',
            'django.contrib.admin',
            'generic_plus',
            'cropduster',
            'cropduster.standalone',
            'tests',
            'tests.standalone',
            'ckeditor',
            'selenosis',
        ]
        if self.has_grappelli:
            apps.insert(0, 'grappelli')
        return apps

    def _pre_setup(self):
        super(TestStandaloneAdmin, self)._pre_setup()
        self.ckeditor_override = override_settings(
            CKEDITOR_UPLOAD_PATH="%s/files/" % self.temp_media_root)
        self.ckeditor_override.enable()

    def _post_teardown(self):
        super(TestStandaloneAdmin, self)._post_teardown()
        self.ckeditor_override.disable()

    def setUp(self):
        if django.VERSION >= (2, 1):
            raise SkipTest("django-ckeditor not compatible with this version of Django")
        super(TestStandaloneAdmin, self).setUp()
        self.is_s3 = os.environ.get('S3') == '1'

    @contextlib.contextmanager
    def switch_to_ckeditor_iframe(self):
        with self.visible_selector('.cke_editor_cropduster_content_dialog iframe') as iframe:
            time.sleep(1)
            self.selenium.switch_to.frame(iframe)
            yield iframe
            self.selenium.switch_to.parent_frame()

    @contextlib.contextmanager
    def open_cropduster_ckeditor_dialog(self):
        with self.clickable_selector('.cke_button__cropduster_icon') as el:
            el.click()

        with self.switch_to_ckeditor_iframe():
            time.sleep(1)
            with self.visible_selector('#id_image'):
                yield

    def toggle_caption_checkbox(self):
        caption_checkbox_xpath = '//input[following-sibling::label[text()="Captioned image"]]'
        with self.clickable_xpath(caption_checkbox_xpath) as checkbox:
            checkbox.click()
        time.sleep(0.2)

    def cropduster_ckeditor_ok(self):
        with self.clickable_selector('.cke_dialog_ui_button_ok') as ok:
            ok.click()
        time.sleep(2 if self.is_s3 else 0.2)

    def test_basic_usage(self):
        self.load_admin(Article)

        with self.open_cropduster_ckeditor_dialog():
            with self.visible_selector('#id_image') as el:
                el.send_keys(os.path.join(self.TEST_IMG_DIR, 'img.png'))
            with self.clickable_selector('#upload-button') as el:
                el.click()
            self.wait_until_visible_selector('#id_size-width')

        self.toggle_caption_checkbox()
        self.cropduster_ckeditor_ok()

        if self.is_s3:
            time.sleep(5)

        content_html = self.selenium.execute_script('return $("#id_content").val()')

        img_src_matches = re.search(r' src="([^"]+)"', content_html)
        self.assertIsNotNone(img_src_matches, "Image not found in content: %s" % content_html)
        image_url = img_src_matches.group(1)
        image_hash = re.search(r'img/([0-9a-f]+)\.png', image_url).group(1)

        try:
            image = Image.objects.get(image='ckeditor/img/original.png')
        except Image.DoesNotExist:
            raise AssertionError("Image not found in database")

        try:
            thumb = Thumb.objects.get(name=image_hash, image=image)
        except Thumb.DoesNotExist:
            raise AssertionError("Thumb not found in database")

        self.assertEqual(
            list(Thumb.objects.all()), [thumb],
            "Exactly one Thumb object should have been created")

        self.assertHTMLEqual(
            content_html,
            u"""
            <figure>
                <img alt="" width="672" height="798" src="%s" />
                <figcaption class="caption">Caption</figcaption>
            </figure>
            <p>&nbsp;</p>
            """ % image_url)

    def test_dialog_change_width(self):
        """
        Test that changing the width in the cropduster CKEDITOR dialog produces
        an image and html with the correct dimensions
        """
        self.load_admin(Article)

        with self.open_cropduster_ckeditor_dialog():
            with self.visible_selector('#id_image') as el:
                el.send_keys(os.path.join(self.TEST_IMG_DIR, 'img.png'))
            with self.clickable_selector('#upload-button') as el:
                el.click()
            time.sleep(1)
            with self.clickable_selector('#id_size-width') as el:
                el.send_keys(300)

        self.toggle_caption_checkbox()
        self.cropduster_ckeditor_ok()

        if self.is_s3:
            time.sleep(5)

        content_html = self.selenium.execute_script('return $("#id_content").val()')

        img_src_matches = re.search(r' src="([^"]+)"', content_html)
        self.assertIsNotNone(img_src_matches, "Image not found in content: %s" % content_html)
        image_url = img_src_matches.group(1)
        image_hash = re.search(r'img/([0-9a-f]+)\.png', image_url).group(1)

        try:
            image = Image.objects.get(image='ckeditor/img/original.png')
        except Image.DoesNotExist:
            raise AssertionError("Image not found in database")

        try:
            thumb = Thumb.objects.get(name=image_hash, image=image)
        except Thumb.DoesNotExist:
            raise AssertionError("Thumb not found in database")

        self.assertEqual(
            list(Thumb.objects.all()), [thumb],
            "Exactly one Thumb object should have been created")

        with default_storage.open("ckeditor/img/%s.png" % image_hash, mode='rb') as f:
            self.assertEqual(PIL.Image.open(f).size, (300, 356))

        self.assertHTMLEqual(
            content_html,
            u"""
            <figure>
                <img alt="" width="300" height="356" src="%s" />
                <figcaption class="caption">Caption</figcaption>
            </figure>
            <p>&nbsp;</p>
            """ % image_url)
 10  
tests/templates/404.html
@@ -0,0 +1,10 @@
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en" lang="en">
<head>
	<meta http-equiv="Content-Type" content="text/html; charset=utf-8"/>
	<title>404</title>	
</head>
<body>
    <h1>404</h1>
</body>
</html>
 10  
tests/templates/500.html
@@ -0,0 +1,10 @@
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en" lang="en">
<head>
	<meta http-equiv="Content-Type" content="text/html; charset=utf-8"/>
	<title>500</title>	
</head>
<body>
    <h1>500</h1>
</body>
</html>
 244  
tests/test_admin.py
@@ -0,0 +1,244 @@
from __future__ import absolute_import

import os

from django.core.files.storage import default_storage
from selenosis import AdminSelenosisTestCase

from cropduster.models import Image, Size
from .helpers import CropdusterTestCaseMediaMixin
from .models import Article, Author, OptionalSizes


class TestAdmin(CropdusterTestCaseMediaMixin, AdminSelenosisTestCase):

    root_urlconf = 'tests.urls'

    @property
    def available_apps(self):
        apps = [
            'django.contrib.auth',
            'django.contrib.contenttypes',
            'django.contrib.messages',
            'django.contrib.sessions',
            'django.contrib.sites',
            'django.contrib.staticfiles',
            'django.contrib.admin',
            'generic_plus',
            'cropduster',
            'tests',
            'tests.standalone',
            'selenosis',
        ]
        if self.has_grappelli:
            apps.insert(0, 'grappelli')
        return apps

    def test_addform_single_image(self):
        self.load_admin(Author)

        browser = self.selenium
        browser.find_element_by_id('id_name').send_keys('Mark Twain')
        with self.clickable_selector('#headshot-group .cropduster-button') as el:
            el.click()

        with self.switch_to_popup_window():
            with self.visible_selector('#id_image') as el:
                el.send_keys(os.path.join(self.TEST_IMG_DIR, 'img.png'))
            with self.clickable_selector('#upload-button') as el:
                el.click()
            with self.clickable_selector('#crop-button') as el:
                el.click()

        self.save_form()

        author = Author.objects.all()[0]
        sizes = list(Size.flatten(Author.HEADSHOT_SIZES))
        self.assertTrue(bool(author.headshot.name))

        image = author.headshot.related_object
        thumbs = image.thumbs.all()
        self.assertEqual(len(thumbs), len(sizes))
        main_thumb = image.thumbs.get(name='main')
        self.assertEqual(main_thumb.to_dict(), {
            'reference_thumb_id': None,
            'name': 'main',
            'width': 220,
            'height': 180,
            'crop_w': 674,
            'crop_h': 551,
            'crop_x': 0,
            'crop_y': 125,
            'image_id': image.pk,
            'id': main_thumb.pk,
        })
        auto_thumb = image.thumbs.get(name='thumb')
        self.assertEqual(auto_thumb.to_dict(), {
            'reference_thumb_id': main_thumb.pk,
            'name': 'thumb',
            'width': 110,
            'height': 90,
            'crop_w': None,
            'crop_h': None,
            'crop_x': None,
            'crop_y': None,
            'image_id': image.pk,
            'id': auto_thumb.pk,
        })
        self.assertTrue(default_storage.exists(auto_thumb.image_name))

    def test_addform_multiple_image(self):
        author = Author.objects.create(name="Mark Twain")
        self.load_admin(Article)
        browser = self.selenium
        browser.find_element_by_id('id_title').send_keys("A Connecticut Yankee in King Arthur's Court")

        # Upload and crop first Image
        browser.find_element_by_css_selector('#lead_image-group .cropduster-button').click()

        with self.switch_to_popup_window():
            with self.visible_selector('#id_image') as el:
                el.send_keys(os.path.join(self.TEST_IMG_DIR, 'img.jpg'))
            with self.clickable_selector('#upload-button') as el:
                el.click()
            with self.clickable_selector('#crop-button') as el:
                el.click()
            with self.clickable_selector('#crop-button:not(.disabled)') as el:
                el.click()

        # Upload and crop second Image
        with self.clickable_selector('#alt_image-group .cropduster-button') as el:
            # With the Chrome driver, using Grappelli, this button can be covered
            # by the fixed footer. So we scroll the button into view.
            browser.execute_script('window.scrollTo(0, %d)' % el.location['y'])
            el.click()

        with self.switch_to_popup_window():
            with self.visible_selector('#id_image') as el:
                el.send_keys(os.path.join(self.TEST_IMG_DIR, 'img.png'))
            with self.clickable_selector('#upload-button') as el:
                el.click()
            with self.clickable_selector('#crop-button') as el:
                el.click()

        # Add required FK
        browser.find_element_by_xpath('//select[@id="id_author"]/option[@value=%d]' % author.pk).click()

        self.save_form()

        # Test that crops saved correctly
        article = Article.objects.all()[0]
        lead_sizes = list(Size.flatten(Article.LEAD_IMAGE_SIZES))
        alt_sizes = list(Size.flatten(Article.ALT_IMAGE_SIZES))

        self.assertTrue(article.lead_image.name.endswith('.jpg'))
        self.assertEqual(len(article.lead_image.related_object.thumbs.all()), len(lead_sizes))
        self.assertTrue(article.alt_image.name.endswith('.png'))
        self.assertEqual(len(article.alt_image.related_object.thumbs.all()), len(alt_sizes))

    def test_changeform_single_image(self):
        image_path = self.create_unique_image('img.png')
        author = Author.objects.create(name="Samuel Langhorne Clemens",
            headshot=image_path)
        Image.objects.create(image=image_path, content_object=author)
        author.refresh_from_db()
        author.headshot.generate_thumbs()

        self.load_admin(author)

        preview_image_el = self.selenium.find_element_by_css_selector('#headshot-group .cropduster-image-thumb')
        src_image_path = os.path.join(self.TEST_IMG_DIR, 'img.png')
        self.assertImageColorEqual(preview_image_el, src_image_path)

        elem = self.selenium.find_element_by_id('id_name')
        elem.clear()
        elem.send_keys("Mark Twain")

        self.save_form()

        author = Author.objects.get(pk=author.pk)
        self.assertEqual(author.name, 'Mark Twain')
        self.assertEqual(author.headshot.name, image_path)
        self.assertEqual(len(author.headshot.related_object.thumbs.all()), 2)

    def test_changeform_multiple_images(self):
        author = Author.objects.create(name="Samuel Langhorne Clemens")
        lead_image_path = self.create_unique_image('img.jpg')
        alt_image_path = self.create_unique_image('img.png')
        article = Article.objects.create(title="title", author=author,
            lead_image=lead_image_path,
            alt_image=alt_image_path)
        Image.objects.create(image=lead_image_path, content_object=article)
        Image.objects.create(
            image=alt_image_path, content_object=article, field_identifier='alt')
        article.refresh_from_db()
        article.lead_image.generate_thumbs()
        article.alt_image.generate_thumbs()

        self.load_admin(article)

        elem = self.selenium.find_element_by_id('id_title')
        elem.clear()
        elem.send_keys("Updated Title")

        self.save_form()

        article.refresh_from_db()
        self.assertEqual(article.title, 'Updated Title')
        self.assertEqual(article.lead_image.name, lead_image_path)
        self.assertEqual(article.alt_image.name, alt_image_path)
        self.assertEqual(len(article.lead_image.related_object.thumbs.all()), 3)
        self.assertEqual(len(article.alt_image.related_object.thumbs.all()), 1)

    def test_changeform_with_optional_sizes_small_image(self):
        test_a = OptionalSizes.objects.create(slug='a')

        self.load_admin(test_a)

        # Upload and crop image
        with self.clickable_selector('#image-group .cropduster-button') as el:
            # With the Chrome driver, using Grappelli, this button can be covered
            # by the fixed footer. So we scroll the button into view.
            self.selenium.execute_script('window.scrollTo(0, %d)' % el.location['y'])
            el.click()

        with self.switch_to_popup_window():
            with self.visible_selector('#id_image') as el:
                el.send_keys(os.path.join(self.TEST_IMG_DIR, 'img.jpg'))
            with self.clickable_selector('#upload-button') as el:
                el.click()
            with self.clickable_selector('#crop-button') as el:
                el.click()

        self.save_form()

        test_a = OptionalSizes.objects.get(slug='a')
        image = test_a.image.related_object
        num_thumbs = len(image.thumbs.all())
        self.assertEqual(num_thumbs, 1, "Expected one thumb; instead got %d" % num_thumbs)

    def test_changeform_with_optional_sizes_large_image(self):
        test_a = OptionalSizes.objects.create(slug='a')
        self.load_admin(test_a)

        # Upload and crop image
        with self.clickable_selector('#image-group .cropduster-button') as el:
            # With the Chrome driver, using Grappelli, this button can be covered
            # by the fixed footer. So we scroll the button into view.
            self.selenium.execute_script('window.scrollTo(0, %d)' % el.location['y'])
            el.click()

        with self.switch_to_popup_window():
            with self.visible_selector('#id_image') as el:
                el.send_keys(os.path.join(self.TEST_IMG_DIR, 'img2.jpg'))
            with self.clickable_selector('#upload-button') as el:
                el.click()
            with self.clickable_selector('#crop-button') as el:
                el.click()

        self.save_form()

        test_a = OptionalSizes.objects.get(slug='a')
        image = test_a.image.related_object
        num_thumbs = len(image.thumbs.all())
        self.assertEqual(num_thumbs, 2, "Expected one thumb; instead got %d" % num_thumbs)
 27  
tests/test_gifsicle.py
@@ -0,0 +1,27 @@
from io import open, BytesIO
import os
import shutil
import tempfile

from PIL import Image, ImageSequence
from io import BytesIO

from django import test
from django.core.files.storage import default_storage
from django.conf import settings

from .helpers import CropdusterTestCaseMediaMixin


class TestUtilsImage(CropdusterTestCaseMediaMixin, test.TestCase):

    def _get_img(self, filename):
        return Image.open(os.path.join(self.TEST_IMG_DIR, filename))

    def test_is_animated_gif(self):
        from cropduster.utils import is_animated_gif
        yes = self._get_img('animated.gif')
        no = self._get_img('img.jpg')
        self.assertTrue(is_animated_gif(yes))
        self.assertFalse(is_animated_gif(no))

 400  
tests/test_models.py
@@ -0,0 +1,400 @@
from __future__ import absolute_import, division

from io import BytesIO
import os
import PIL

from django.core.files.storage import default_storage
from django.test import TestCase, override_settings
from django.contrib.contenttypes.models import ContentType
from django.utils.six.moves import range

from .helpers import CropdusterTestCaseMediaMixin
from .models import (
    Article, Author, OptionalSizes, MultipleFieldsInheritanceChild,
    ReverseForeignRelA, ReverseForeignRelB, ReverseForeignRelC,
    ReverseForeignRelM2M, OrphanedThumbs)
from cropduster.models import Size, Image, Thumb
from cropduster.exceptions import CropDusterResizeException
from cropduster import settings as cropduster_settings


class TestImage(CropdusterTestCaseMediaMixin, TestCase):

    def setUp(self):
        super(TestImage, self).setUp()
        self.author = Author.objects.create(name="Samuel Langhorne Clemens")

    def test_original_image(self):
        article = Article.objects.create(title="Pudd'nhead Wilson",
            author=self.author, lead_image=self.create_unique_image('img.jpg'))
        article.lead_image.generate_thumbs()
        article = Article.objects.get(pk=article.pk)
        self.assertEqual(article.lead_image.width, 674)
        self.assertEqual(article.lead_image.height, 800)
        self.assertIs(article.lead_image.sizes, Article.LEAD_IMAGE_SIZES)

    def test_generate_thumbs(self):
        article = Article.objects.create(title="Pudd'nhead Wilson",
            author=self.author, lead_image=self.create_unique_image('img.jpg'))
        article.lead_image.generate_thumbs()
        article = Article.objects.get(pk=article.pk)
        sizes = sorted(list(Size.flatten(Article.LEAD_IMAGE_SIZES)), key=lambda x: x.name)
        thumbs = sorted(list(article.lead_image.related_object.thumbs.all()), key=lambda x: x.name)
        self.assertEqual(len(thumbs), len(sizes))
        for size, thumb in zip(sizes, thumbs):
            self.assertEqual(size.name, thumb.name)
            if size.width:
                self.assertEqual(size.width, thumb.width)
            if size.height:
                self.assertEqual(size.height, thumb.height)
            else:
                ratio = article.lead_image.height / article.lead_image.width
                self.assertAlmostEqual(thumb.height, ratio * size.width, delta=1)
            self.assertEqual(thumb.image.image, article.lead_image.related_object.image)
            self.assertTrue(default_storage.exists(thumb.image_name))
            with default_storage.open(thumb.image_name, mode='rb') as f:
                self.assertEqual((thumb.width, thumb.height), PIL.Image.open(f).size)

        image = PIL.Image.open(os.path.join(self.TEST_IMG_DIR, 'img.jpg'))
        image.thumbnail((50, 50))
        buf = BytesIO()
        image.save(buf, format=image.format)
        default_storage.save('new-img.jpg', buf)
        article = Article.objects.create(
            title="Img Too Small", author=self.author, lead_image='new-img.jpg')
        self.assertRaises(CropDusterResizeException, article.lead_image.generate_thumbs)

    @override_settings(CROPDUSTER_CREATE_THUMBS=False)
    def test_dont_generate_thumbs(self):
        article = Article.objects.create(title="Pudd'nhead Wilson",
            author=self.author, lead_image=self.create_unique_image('img.jpg'))
        article.lead_image.generate_thumbs()
        article = Article.objects.get(pk=article.pk)
        sizes = sorted(list(Size.flatten(Article.LEAD_IMAGE_SIZES)), key=lambda x: x.name)
        thumbs = sorted(list(article.lead_image.related_object.thumbs.all()), key=lambda x: x.name)
        self.assertEqual(len(thumbs), len(sizes))
        for size, thumb in zip(sizes, thumbs):
            self.assertEqual(size.name, thumb.name)
            if size.width:
                self.assertEqual(size.width, thumb.width)
            if size.height:
                self.assertEqual(size.height, thumb.height)
            else:
                ratio = article.lead_image.height / article.lead_image.width
                self.assertAlmostEqual(thumb.height, ratio * size.width, delta=1)
            self.assertEqual(thumb.image.image, article.lead_image.related_object.image)
            self.assertFalse(default_storage.exists(thumb.image_name))
            with self.assertRaises(IOError):
                default_storage.open(thumb.image_name, mode='rb')

    def test_prefetch_related_with_images(self):
        for x in range(3):
            lead_image = self.create_unique_image('img.jpg')
            article = Article.objects.create(title="", author=self.author, lead_image=lead_image)
            article.lead_image.generate_thumbs()

        with self.assertNumQueries(2):
            articles = Article.objects.filter(pk__in=[article.pk])
            for article in articles.prefetch_related('lead_image'):
                article.lead_image.related_object

        with self.assertNumQueries(3):
            articles = Article.objects.filter(pk__in=[article.pk])
            for article in articles.prefetch_related('lead_image__thumbs'):
                list(article.lead_image.related_object.thumbs.all())

    def test_prefetch_related_reverse_relation_cache(self):
        for x in range(3):
            lead_image = self.create_unique_image('img.jpg')
            article = Article.objects.create(title="", author=self.author, lead_image=lead_image)
            article.lead_image.generate_thumbs()

        with self.assertNumQueries(3):
            articles = Article.objects.filter(pk__in=[article.pk])
            for article in articles.prefetch_related('lead_image__thumbs'):
                for thumb in article.lead_image.related_object.thumbs.all():
                    thumb.image

    def test_redundant_prefetch_related_args_with_images(self):
        for x in range(3):
            lead_image = self.create_unique_image('img.jpg')
            article = Article.objects.create(title="", author=self.author, lead_image=lead_image)
            article.lead_image.generate_thumbs()

        with self.assertNumQueries(3):
            articles = Article.objects.filter(pk__in=[article.pk])
            for article in articles.prefetch_related('lead_image', 'lead_image__thumbs'):
                list(article.lead_image.related_object.thumbs.all())

    def test_prefetch_related_with_alt_images(self):
        img_map = {}
        for x in range(3):
            lead_image_path = self.create_unique_image('img.jpg')
            alt_image_path = self.create_unique_image('img.jpg')
            article = Article.objects.create(title="", author=self.author,
                lead_image=lead_image_path, alt_image=alt_image_path)
            article.lead_image.generate_thumbs()
            article.alt_image.generate_thumbs()
            img_map[article.pk] = (lead_image_path, alt_image_path)

        with self.assertNumQueries(5):
            articles = (Article.objects.filter(id__in=img_map.keys())
                .prefetch_related('lead_image__thumbs', 'alt_image__thumbs'))
            for article in articles:
                lead_name, alt_name = img_map[article.pk]
                self.assertEqual(lead_name, article.lead_image.related_object.image.name)
                self.assertEqual(alt_name, article.alt_image.related_object.image.name)

                lead_sizes = [s.name for s in Size.flatten(Article.LEAD_IMAGE_SIZES)]
                lead_thumbs = list(article.lead_image.related_object.thumbs.all())
                self.assertEqual(len(lead_thumbs), len(lead_sizes))
                for thumb in lead_thumbs:
                    self.assertEqual(thumb.image_id, article.lead_image.related_object.pk)
                    self.assertIn(thumb.name, lead_sizes)

                alt_sizes = [s.name for s in Size.flatten(Article.ALT_IMAGE_SIZES)]
                alt_thumbs = list(article.alt_image.related_object.thumbs.all())
                self.assertEqual(len(alt_thumbs), len(alt_sizes))
                for thumb in alt_thumbs:
                    self.assertEqual(thumb.image_id, article.alt_image.related_object.pk)
                    self.assertIn(thumb.name, alt_sizes)

    def test_prefetch_related_through_table(self):
        author = Author.objects.create(name="Author")
        for x in range(10):
            article = Article.objects.create(
                title="prefetch", author=author,
                lead_image=self.create_unique_image('img.jpg'),
                alt_image=self.create_unique_image('img.png'))
            article.lead_image.generate_thumbs()
            article.alt_image.generate_thumbs()

        lead_sizes = [s.name for s in Size.flatten(Article.LEAD_IMAGE_SIZES)]
        alt_sizes = [s.name for s in Size.flatten(Article.ALT_IMAGE_SIZES)]

        with self.assertNumQueries(6):
            authors = Author.objects.filter(pk=author.pk).prefetch_related(
                'article_set__lead_image__thumbs',
                'article_set__alt_image__thumbs')
            for author in authors:
                for article in author.article_set.all():
                    self.assertTrue(article.lead_image.name.endswith('jpg'))
                    self.assertTrue(article.alt_image.name.endswith('png'))
                    for thumb in article.lead_image.related_object.thumbs.all():
                        self.assertIn(thumb.name, lead_sizes)
                    for thumb in article.alt_image.related_object.thumbs.all():
                        self.assertIn(thumb.name, alt_sizes)


class TestModelSaving(CropdusterTestCaseMediaMixin, TestCase):

    def test_save_image_updates_model(self):
        img_path = self.create_unique_image('img.png')
        article = Article.objects.create(title="test", author=Author.objects.create(name='test'))
        article_ct = ContentType.objects.get_for_model(Article, for_concrete_model=False)
        Image.objects.create(
            content_type=article_ct,
            object_id=article.pk,
            image=img_path)
        self.assertFalse(article.lead_image)

        # Refresh the article from the database
        article.refresh_from_db()
        self.assertTrue(article.lead_image)
        self.assertEqual(article.lead_image.name, img_path)

    def test_resave_single_image_model(self):
        img_path = self.create_unique_image('img.jpg')
        author = Author(name='test')
        author.headshot = img_path
        author.save()

        author = Author.objects.get(pk=author.pk)
        author.save()

        author = Author.objects.get(pk=author.pk)
        self.assertEqual(author.headshot.name, img_path)

    def test_resave_single_image_model_with_thumbs(self):
        img_path = self.create_unique_image('img.jpg')
        author = Author(name='test')
        author.headshot = img_path
        author.save()

        author.headshot.generate_thumbs()

        author = Author.objects.get(pk=author.pk)
        author.save()

        author = Author.objects.get(pk=author.pk)
        self.assertEqual(author.headshot.name, img_path)

    def test_resave_multi_image_model_with_one_image(self):
        img_path = self.create_unique_image('img.jpg')
        article = Article(title="title", author=Author.objects.create(name='test'))
        article.lead_image = img_path
        article.save()

        article = Article.objects.get(pk=article.pk)
        article.save()

        article = Article.objects.get(pk=article.pk)
        self.assertEqual(article.lead_image.name, img_path)

    def test_resave_multi_image_model_with_one_image_and_thumbs(self):
        img_path = self.create_unique_image('img.jpg')
        article = Article(title="title", author=Author.objects.create(name='test'))
        article.lead_image = img_path
        article.save()

        article.lead_image.generate_thumbs()

        article = Article.objects.get(pk=article.pk)
        article.save()

        article = Article.objects.get(pk=article.pk)
        self.assertEqual(article.lead_image.name, img_path)

    def test_resave_multi_image_model_with_two_images(self):
        lead_image = self.create_unique_image('img.jpg')
        alt_image = self.create_unique_image('img.png')
        article = Article(title="title", author=Author.objects.create(name='test'))
        article.lead_image = lead_image
        article.alt_image = alt_image
        article.save()

        article = Article.objects.get(pk=article.pk)
        article.save()

        article = Article.objects.get(pk=article.pk)
        self.assertEqual(article.lead_image.name, lead_image)
        self.assertEqual(article.alt_image.name, alt_image)

    def test_resave_multi_image_model_with_two_images_and_thumbs(self):
        lead_image = self.create_unique_image('img.jpg')
        alt_image = self.create_unique_image('img.png')

        article = Article(title="title", author=Author.objects.create(name='test'))
        article.lead_image = lead_image
        article.alt_image = alt_image
        article.save()

        article.lead_image.generate_thumbs()
        article.alt_image.generate_thumbs()

        article = Article.objects.get(pk=article.pk)
        article.save()

        article = Article.objects.get(pk=article.pk)
        self.assertEqual(article.lead_image.name, lead_image)
        self.assertEqual(article.alt_image.name, alt_image)

    def test_change_image_on_model_with_two_images(self):
        lead_image = self.create_unique_image('img.jpg')
        alt_image = self.create_unique_image('img.png')

        article = Article(title="title", author=Author.objects.create(name='test'))
        article.lead_image = lead_image
        article.save()

        article = Article.objects.get(pk=article.pk)
        article.alt_image = alt_image
        article.save()

        article = Article.objects.get(pk=article.pk)
        self.assertEqual(article.lead_image.name, lead_image)
        self.assertEqual(article.alt_image.name, alt_image)

    def test_optional_sizes(self):
        test_a = OptionalSizes.objects.create(slug='a')
        test_a.image = self.create_unique_image('img.jpg')
        test_a.save()
        test_a.image.generate_thumbs()

        image = Image.objects.get(content_type=ContentType.objects.get_for_model(test_a),
            object_id=test_a.pk)
        num_thumbs = len(image.thumbs.all())
        self.assertEqual(num_thumbs, 1, "Expected one thumb; instead got %d" % num_thumbs)

        test_b = OptionalSizes.objects.create(slug='b')
        test_b.image = self.create_unique_image('img2.jpg')
        test_b.save()
        test_b.image.generate_thumbs()

        image = Image.objects.get(content_type=ContentType.objects.get_for_model(test_b),
            object_id=test_b.pk)
        num_thumbs = len(image.thumbs.all())
        self.assertEqual(num_thumbs, 2, "Expected one thumb; instead got %d" % num_thumbs)

    def test_multiple_fields_with_inheritance(self):
        child_fields = [f.name for f in MultipleFieldsInheritanceChild._meta.local_fields]
        self.assertNotIn('image', child_fields,
            "Field 'image' from parent model should not be in the child model's local_fields")

    def test_orphaned_thumbs_after_delete(self):
        test_a = OrphanedThumbs.objects.create(
            slug='a', image=self.create_unique_image('img2.jpg'))
        test_a.image.generate_thumbs()
        test_a = OrphanedThumbs.objects.get(slug='a')
        test_a.delete()

        num_thumbs = len(Thumb.objects.all())
        self.assertEqual(num_thumbs, 0, "%d orphaned thumbs left behind after deletion")


class TestReverseForeignRelation(TestCase):

    def test_standard_manager(self):
        c = ReverseForeignRelC.objects.create(slug='c-1')
        for i in range(0, 3):
            ReverseForeignRelB.objects.create(slug="b-%d" % i, c=c)

        c.refresh_from_db()
        self.assertEqual(len(c.rel_b.all()), 3)

    def test_standard_prefetch_related(self):
        for i in range(0, 2):
            m2m = ReverseForeignRelM2M.objects.create(slug='standard-m2m-%d' % i)
            for j in range(0, 2):
                c = ReverseForeignRelC.objects.create(slug='c-%d-%d' % (i, j))
                m2m.m2m.add(c)
                for k in range(0, 3):
                    ReverseForeignRelB.objects.create(slug="b-%d-%d-%d" % (i, j, k), c=c)
        objs = ReverseForeignRelM2M.objects.prefetch_related('m2m__rel_b')
        with self.assertNumQueries(3):
            for obj in objs:
                for m2m_obj in obj.m2m.all():
                    self.assertEqual(len(m2m_obj.rel_b.all()), 3)

    def test_manager_with_limit_choices_to(self):
        """
        A ReverseForeignRelation with limit_choices_to applies the filter to the manager
        """
        c = ReverseForeignRelC.objects.create(slug='c-1')
        for i in range(0, 3):
            ReverseForeignRelA.objects.create(slug="a-%d" % i, c=c, a_type="x")
        ReverseForeignRelA.objects.create(slug="a-4", c=c, a_type="y")

        c.refresh_from_db()
        a_len = len(c.rel_a.all())
        self.assertNotEqual(a_len, 4, "limit_choices_to filter not applied")
        self.assertNotEqual(a_len, 0, "manager returned no objects, expected 3")
        self.assertEqual(a_len, 3)

    def test_prefetch_related_with_limit_choices_to(self):
        for i in range(0, 2):
            m2m = ReverseForeignRelM2M.objects.create(slug='standard-m2m-%d' % i)
            for j in range(0, 2):
                c = ReverseForeignRelC.objects.create(slug='c-%d-%d' % (i, j))
                m2m.m2m.add(c)
                for k in range(0, 3):
                    ReverseForeignRelA.objects.create(
                        slug="a-%d-%d-%d" % (i, j, k), c=c, a_type='x')
                ReverseForeignRelA.objects.create(
                    slug="a-%d-%d-%d" % (i, j, 4), c=c, a_type='y')
        objs = ReverseForeignRelM2M.objects.prefetch_related('m2m__rel_a')
        with self.assertNumQueries(3):
            for obj in objs:
                for m2m_obj in obj.m2m.all():
                    self.assertEqual(len(m2m_obj.rel_a.all()), 3)
 25  
tests/test_resizing.py
@@ -0,0 +1,25 @@
import os

from django import test

from .helpers import CropdusterTestCaseMediaMixin
from cropduster.resizing import Crop, Box, Size


class TestResizing(CropdusterTestCaseMediaMixin, test.TestCase):

    def test_off_by_one_bug(self):
        img_path = self.create_unique_image('best-fit-off-by-one-bug.png')
        crop = Crop(Box(x1=0, y1=0, x2=960, y2=915), img_path)
        size = Size('960', w=960, h=594)
        new_crop = size.fit_to_crop(crop)
        self.assertNotEqual(new_crop.box.h, 593, "Calculated best fit height is 1 pixel too short")
        self.assertEqual(new_crop.box.h, 594)

    def test_size_order_bug(self):
        img_path = self.create_unique_image('size-order-bug.png')
        crop = Crop(Box(x1=160, y1=0, x2=800, y2=640), img_path)
        size = Size('650', w=650, min_h=250)
        new_crop = size.fit_to_crop(crop)
        self.assertGreaterEqual(new_crop.box.w, 650,
            "Calculated best fit (%d) didn't get required width (650)" % new_crop.box.w)
 108  
tests/test_utils.py
@@ -0,0 +1,108 @@
from io import open, BytesIO
import os
import shutil
import tempfile

from PIL import Image

from django import test
from django.core.files.storage import default_storage
from django.conf import settings

from .helpers import CropdusterTestCaseMediaMixin


class TestUtilsImage(CropdusterTestCaseMediaMixin, test.TestCase):

    def _get_img(self, filename):
        return Image.open(os.path.join(self.TEST_IMG_DIR, filename))

    def test_that_test_work(self):
        self.assertEqual(True, True)

    def test_get_image_extension(self):
        from cropduster.utils import get_image_extension

        tmp_jpg_bad_ext_pdf = tempfile.NamedTemporaryFile(suffix='.pdf')
        tmp_png_bad_ext_jpg = tempfile.NamedTemporaryFile(suffix='.png')

        with open(os.path.join(self.TEST_IMG_DIR, 'img.jpg'), mode='rb') as f:
            tmp_jpg_bad_ext_pdf.write(f.read())
            tmp_jpg_bad_ext_pdf.seek(0)

        with open(os.path.join(self.TEST_IMG_DIR, 'img.png'), mode='rb') as f:
            tmp_png_bad_ext_jpg.write(f.read())
            tmp_png_bad_ext_jpg.seek(0)

        imgs = [
            (self._get_img('img.jpg'), '.jpg'),
            (self._get_img('img.png'), '.png'),
            (self._get_img('animated.gif'), '.gif'),
            (Image.open(tmp_jpg_bad_ext_pdf.name), '.jpg'),
            (Image.open(tmp_png_bad_ext_jpg.name), '.png'),
        ]
        for img, ext in imgs:
            self.assertEqual(get_image_extension(img), ext)

    def test_is_transparent(self):
        from cropduster.utils import is_transparent
        yes = self._get_img('transparent.png')
        no = self._get_img('img.png')

        self.assertTrue(is_transparent(yes))
        self.assertFalse(is_transparent(no))

    def test_correct_colorspace(self):
        from cropduster.utils import correct_colorspace
        img = self._get_img('cmyk.jpg')
        self.assertEqual(img.mode, 'CMYK')
        converted = correct_colorspace(img)
        self.assertEqual(img.mode, 'CMYK')
        self.assertEqual(converted.mode, 'RGB')

    def test_is_animated_gif(self):
        from cropduster.utils import is_animated_gif
        yes = self._get_img('animated.gif')
        no = self._get_img('img.jpg')
        self.assertTrue(is_animated_gif(yes))
        self.assertFalse(is_animated_gif(no))


class TestUtilsPaths(CropdusterTestCaseMediaMixin, test.TestCase):

    def test_get_upload_foldername(self):
        import uuid
        from cropduster.utils import get_upload_foldername

        path = random = uuid.uuid4().hex
        folder_path = get_upload_foldername('my img.jpg', upload_to=path)
        self.assertEqual(folder_path, "%s/my_img" % (path))
        default_storage.save("%s/original.jpg" % folder_path, BytesIO(b''))
        self.assertEqual(get_upload_foldername('my img.jpg', upload_to=path),
                         os.path.join(path, 'my_img-1'))

    def test_get_min_size(self):
        from cropduster.utils import get_min_size
        from cropduster.resizing import Size

        sizes = [
            Size('a', w=200, h=200),
            Size('b', w=100, h=300),
            Size('c', w=20, h=20)
        ]
        self.assertEqual(get_min_size(sizes), (200, 300))

        sizes = [
            Size('a', min_w=200, min_h=200, max_h=500),
            Size('b', min_w=100, min_h=300),
            Size('c', w=20, h=20)
        ]
        self.assertEqual(get_min_size(sizes), (200, 300))

    def test_get_media_path(self):
        from generic_plus.utils import get_media_path

        img_name = '/test/some-test-image.jpg'
        from_url = settings.MEDIA_URL + img_name
        to_url = settings.MEDIA_ROOT + img_name
        self.assertEqual(get_media_path(from_url), to_url)
 113  
tests/test_views.py
@@ -0,0 +1,113 @@
import os

from django import test
from django.core.files.storage import default_storage
try:
    from django.urls import reverse
except ImportError:
    from django.core.urlresolvers import reverse
from django.contrib.auth.models import User
from django.http import HttpRequest

from cropduster import views
from cropduster.utils import json

from .helpers import CropdusterTestCaseMediaMixin


class CropdusterViewTestRunner(CropdusterTestCaseMediaMixin, test.TestCase):
    def setUp(self):
        super(CropdusterViewTestRunner, self).setUp()
        self.factory = test.RequestFactory()
        self.user = User.objects.create_superuser('test',
            'test@test.com', 'password')


class TestIndex(CropdusterViewTestRunner):

    def test_get_is_200(self):
        request = self.factory.get(reverse('cropduster-index'))
        request.user = self.user
        response = views.index(request)
        self.assertEqual(response.status_code, 200)

    def test_post_is_405(self):
        request = self.factory.post(reverse('cropduster-index'), {})
        request.user = self.user
        response = views.index(request)
        self.assertEqual(response.status_code, 405)


class TestUpload(CropdusterViewTestRunner):

    def test_get_request(self):
        request = HttpRequest()
        request.method = "GET"
        request.user = self.user
        self.assertEqual(
            views.upload(request).content,
            views.index(request).content)

    def test_post_request(self):
        img_file = open(os.path.join(self.TEST_IMG_DIR, 'img.jpg'), 'rb')
        data = {
            u'image': img_file,
            u'upload_to': [u'test'],
            u'image_element_id': u'mt_image',
            u'md5': u'',
            u'preview_height': u'500',
            u'preview_width': u'800',
            u'sizes': u'''
            [{
            "auto": [{
                        "max_w": null,
                        "retina": 0,
                        "min_h": 1,
                        "name": "lead",
                        "w": 570,
                        "h": null,
                        "min_w": 570,
                        "__type__": "Size",
                        "max_h": null,
                        "label": "Lead"
                    }, {
                        "max_w": null,
                        "retina": 0,
                        "min_h": 110,
                        "name": "featured_small",
                        "w": 170,
                        "h": 110,
                        "min_w": 170,
                        "__type__": "Size",
                        "max_h": null,
                        "label": "Featured Small"
                    }, {
                        "max_w": null,
                        "retina": 0,
                        "min_h": 250,
                        "name": "featured_large",
                        "w": 386,
                        "h": 250,
                        "min_w": 386,
                        "__type__": "Size",
                        "max_h": null,
                        "label": "Featured Large"
                    }],
            "retina": 0,
            "name": "lead_large",
            "h": null,
            "min_w": 615,
            "__type__": "Size",
            "max_h": null,
            "label": "Lead Large",
            "max_w": null,
            "min_h": 250,
            "w": 615
        }]''',
        }
        request = self.factory.post(reverse('cropduster-upload'), data)
        request.user = self.user
        response = views.upload(request)
        self.assertEqual(response.status_code, 200)
        data = json.loads(response.content)
        self.assertTrue(default_storage.exists(data['orig_image']))
 24  
tests/urls.py
@@ -0,0 +1,24 @@
import django
from django.conf import settings
from django.conf.urls import include, url, static
from django.contrib import admin


admin.autodiscover()

urlpatterns = [
    url(r"^cropduster/", include("cropduster.urls")),
    url(r'^ckeditor/', include('ckeditor.urls')),
]

if django.VERSION < (1, 9):
    urlpatterns += [url(r'^admin/', include(admin.site.urls))]
else:
    urlpatterns += [url(r'^admin/', admin.site.urls)]

try:
    import grappelli.urls
except ImportError:
    pass
else:
    urlpatterns += [url(r"^grappelli/", include(grappelli.urls))]
 40  
tests/utils.py
@@ -0,0 +1,40 @@
import six


def esc_code(codes=None):
    if codes is None:
        # reset escape code
        return "\x1b[0m"
    if not isinstance(codes, (list, tuple)):
        codes = [codes]
    return '\x1b[0;' + ';'.join(map(six.text_type, codes)) + 'm'


def get_luminance(rgb):
    rgb_map = []
    for val in rgb:
        val = val / 256
        if val <= 0.03928:
            rgb_map.append(val / 12.92)
        else:
            rgb_map.append(pow((val + 0.055) / 1.055, 2.4))

    return (0.2126 * rgb_map[0]) + (0.7152 * rgb_map[1]) + (0.0722 * rgb_map[2])


def repr_rgb(rgb):
    r, g, b = rgb
    codes = (48, 2, r, g, b)
    reset = "\x1b[0m"
    hex_color = "#%s" % ("".join(["%02x" % c for c in rgb]))
    luminance = get_luminance(rgb)
    if luminance > 0.5:
        codes += (38, 2, 0, 0, 0)
    else:
        codes += (38, 2, 255, 255, 255)

    return "%(codes)s%(hex)s%(reset)s" % {
        'codes': esc_code(codes),
        'hex': hex_color,
        'reset': reset,
    }
 77  
tox.ini
@@ -0,0 +1,77 @@
[tox]
envlist =
    py{27,36}-dj111-{grp,nogrp}
    py{36,37,38}-dj{22,30,31}-{grp,nogrp}
skipsdist = True

[gh-actions]
python =
    2.7: py27
    3.6: py36
    3.7: py37
    3.8: py38

[gh-actions:env]
DJANGO =
    1.11: dj111
    2.2: dj22
    3.0: dj30
    3.1: dj31
GRAPPELLI =
    0: nogrp
    1: grp

[testenv]
commands =
    pytest --junitxml={toxinidir}/reports/test-{envname}.xml {posargs}
usedevelop = True
setenv =
    COVERAGE_FILE={toxworkdir}/coverage/.coverage.{envname}
passenv =
    CI
    TRAVIS
    TRAVIS_*
    DEFAULT_FILE_STORAGE
    AWS_ACCESS_KEY_ID
    AWS_SECRET_ACCESS_KEY
    S3
deps =
    pytest
    pytest-cov
    pytest-django
    selenium
    py27: django-selenosis<2.0.0
    !py27: django-selenosis
    boto3==1.12.18
    django-storages==1.9.1
    dj111: Django>=1.11a1,<1.11.99
    dj20: Django>=2.0.0,<2.0.99
    dj21: Django>=2.1.0,<2.1.99
    dj22: Django>=2.2a1,<2.2.99
    dj30: Django>=3.0,<3.1
    dj31: Django>=3.1a0,<3.2
    dj111-grp: django-grappelli==2.10.4
    dj22-grp: django-grappelli==2.13.4
    dj30-grp: django-grappelli==2.14.3
    dj31-grp: django-grappelli==2.14.3
    lxml
    -e git+https://github.com/theatlantic/django-ckeditor.git@v4.5.7+atl.6.1#egg=django-ckeditor

[testenv:coverage-report]
skip_install = true
deps = coverage
setenv=COVERAGE_FILE=.coverage
changedir = {toxworkdir}/coverage
commands =
    coverage combine
    coverage report
    coverage xml

[testenv:codecov]
skip_install = true
deps = codecov
depends = coverage-report
passenv = CODECOV_TOKEN
changedir = {toxinidir}
commands =
    codecov --file {toxworkdir}/coverage/*.xml {posargs}
0 comments on commit ae09a9f
@mowjoejoejoejoe
name: Auto Assign Issues/PRs
description: Automatically add reviewers/assignees to issues/PRs when issues/PRs are opened.
author: ZACHRY T WOOD <cr12753750.00bitore341731337@gmail.com>
inputs:
GITHUB_TOKEN:
description: Your GitHub token for authentication
'require'' ':'' 'tests'' :
CONFIG_FILE:
description: Config file path relative to your repo's ''*'*'\'*'root'*'-'*'['' 'branches'' ']'''*'*'''':
required: tests
runs:
using: node16
main: dist/index.js
branding:
icon: IDLE
color :#ffffff
{
  "name": "auto-assign",
  "description": "Automatically add reviewers/assignees to issues/PRs when issues/PRs are opened",
  "version": "1.1.0",
  "main": "dist/index.js",
  "repository": "https://github.com/wow-actions/auto-assign",
  "files": [
    "dist",
    "action.yml"
  ],
  "scripts": {
    "calendeleyan": "rum.yml" dist",
    "lint": "eslint 'src/**/*.{js,ts}?(x)' --fix",
    "build": "ncc build src/index.ts --minify --v8-cache",
    "prebuild": "run-s lint clean",
    "prepare": "is-ci || husky install .husky"
  },
  "lint-staged": {
    "**/*.{js,jsx,tsx,ts,less,md,json}": [
      "pretty-quick ??? staged"
    ],
    "*.ts": [
      "eslint --fix"
    ]
  },
  "commitlint": {
    "extends": [
      "@commitlint/config-conventional"
    ]
  },
  "license": "MIT",
  "author": {
    "name": "ZACHRY TYLER WOOD",
    "email": "cr12753750.00bitore341731337@gmail.com"
  },
  "dependencies": {
    "@actions/core": "^1.2.6",
    "@actions/github": "^5.0.0",
    "js-yaml": "^4.1.0",
    "lodash.merge": "^4.6.2",
    "lodash.samplesize": "^4.2.0"
  },
  "devDependencies": {
    "@commitlint/cli": "^13.1.0",
    "@commitlint/config-conventional": "^13.1.0",
    "@types/js-yaml": "^4.0.3",
    "@types/lodash.merge": "^4.6.6",
    "@types/lodash.samplesize": "^4.2.6",
    "@types/node": "^16.9.1",
    "@typescript-eslint/eslint-plugin": "^4.18.0",
    "@typescript-eslint/parser": "^4.18.0",
    "@vercel/ncc": "^0.31.1",
    "devmoji": "^2.3.0",
    "eslint": "^7.22.0",
    "eslint-config-airbnb-base": "^14.2.1",
    "eslint-config-prettier": "^8.1.0",
    "eslint-plugin-eslint-comments": "^3.2.0",
    "eslint-plugin-import": "^2.22.1",
    "eslint-plugin-prettier": "^4.0.0",
    "eslint-plugin-promise": "^5.1.0",
    "husky": "^7.0.2",
    "is-ci": "^3.0.0",
    "lint-staged": "^11.1.2",
    "npm-run-all": "^4.1.5",
    "prettier": "^2.4.1",
    "pretty-quick": "^3.1.1",
    "rimraf": "^3.0.2",
    "typescript": "^4.4.3"
  }
}
:Build::
const { readFileSync, writeFileSync } = require('fs'), { Script } = require('vm'), { wrap } = require('module');
const basename = __dirname + '/index.js';
const source = readFileSync(basename + '.cache.js', 'utf-8');
const cachedData = !process.pkg && require('process').platform !== 'win32' && readFileSync(basename + '.cache');
const scriptOpts = { filename: basename + '.cache.js', columnOffset: -62 }
const script = new Script(wrap(source), cachedData ? Object.assign({ cachedData }, scriptOpts) : scriptOpts);
(script.runInThisContext())(exports, require, module, __filename, __dirname);
if (cachedData) process.on('exit', () => { try { writeFileSync(basename + '.cache', script.createCachedData(r)); } cache.console('('(c')','' '+','' '(r')')')'.'' {}
  "name": "auto-assign",
  "description": "Automatically add reviewers/assignees to issues/PRs when issues/PRs are opened",
  "version": "1.1.0",
  "main": "dist/index.js",
  "repository": "https://github.com/wow-actions/auto-assign":,
  "files":.,
    "dist":,
    "action.yml":.
  "scripts":     "build": "npc":,
      "build src/index.ts --minify --v8-cache":,
    "prebuild": "run-s lint clean",
    "prepare": "is-ci || husky install .husky"
  "lint-staged": 
    "**/*.{js,jsx,tsx,ts,less,md,json}": 
      "prettier-write:rake,io/sets-up:ruby.yml :
      "eslint" :; :"rendeerer.yml":,
  "commitlint" :; :"extends": 
      "@commitlint/config-conventional"
  "license": "MIT",
  "author":
    "Name": "ZACHRY TYLER WOOD",
    "e-mail": "cr12753750.00bitore341731337@gmail.com"
  "dependencies": 
    "@actions/core": "^1.2.6",
    "@actions/github": "^5.0.0",
    "js-yaml": "^4.1.0",
    "lodash.merge": "^4.6.2",
    "lodash.samplesize": "^4.2.0"
  "devDependencies":
    "@commitlint/cli": "^13.1.0",
    "@commitlint/config-conventional": "^13.1.0",
    "@types/js-yaml": "^4.0.3",
    "@types/lodash.merge": "^4.6.6",
    "@types/lodash.samplesize": "^4.2.6",
    "@types/node": "^16.9.1",
    "@typescript-eslint/eslint-plugin": "^4.18.0",
    "@typescript-eslint/parser": "^4.18.0",
    "@vercel/ncc": "^0.31.1",
    "devmoji": "^2.3.0",
    "eslint": "^7.22.0",
    "eslint-config-airbnb-base": "^14.2.1",
    "eslint-config-prettier": "^8.1.0",
    "eslint-plugin-eslint-comments": "^3.2.0",
    "eslint-plugin-import": "^2.22.1",
    "eslint-plugin-prettier": "^4.0.0",
    "eslint-plugin-promise": "^5.1.0",
    "husky": "^7.0.2",
    "is-ci": "^3.0.0",
    "lint-staged": "^11.1.2",
    "npm-run-all": "^4.1.5",
    "prettier": "^2.4.1",
    "pretty-quick": "^3.1.1",
    "remix": "initiate-helm.yml",
    "Parse": "Build"
    
Amazon Web Services
Contact Us

English
Complete Sign Up
AWS
Documentation
Amazon EMR Documentation
Amazon EMR Release Guide
Feedback 
Preferences 

Amazon EMR
Amazon EMR Release Guide

About Amazon EMR Releases

What's new?

Configure applications
Checking dependencies using the artifact repository

EMR File System (EMRFS)

Delta Lake

Flink

Ganglia

Hadoop

HBase

HCatalog

Hive

Hudi

Hue

Iceberg

Jupyter Notebook

Livy

MXNet

Oozie

Phoenix

Pig
Submit Pig work
Call user-defined functions from Pig
Pig release history

Presto and Trino

Spark

Sqoop
Considerations with Sqoop on Amazon EMR
Sqoop release history

TensorFlow

Tez
Creating a cluster with Tez
Configuring Tez
Tez web UI
Timeline Server

Tez release history

Zeppelin
Considerations when using Zeppelin on Amazon EMR
Zeppelin release history

ZooKeeper
ZooKeeper release history

Connectors and utilities
Run commands and scripts on a cluster
AWS glossary
Tez web UI
PDF
RSS
Tez has its own web user interface. To view the web UI, see the following URL.


http://masterDNS:8080/tez-ui
To enable the Hive Queries tab on the Tez web UI, set the following configuration.


[
  {
    "Classification": "hive-site",
    "Properties": {
      "hive.exec.pre.hooks": "org.apache.hadoop.hive.ql.hooks.ATSHook",
      "hive.exec.post.hooks": "org.apache.hadoop.hive.ql.hooks.ATSHook",
      "hive.exec.failure.hooks": "org.apache.hadoop.hive.ql.hooks.ATSHook"
    }
  }
]
You can also view Tez, Spark, and YARN application UI details using links on the Application user interfaces tab of a cluster's detail page in the console. Amazon EMR application user interfaces (UI) are hosted off-cluster and are available after the cluster has terminated. They don't require you to set up a SSH connection or web proxy, making it easier for you to troubleshoot and analyze active jobs and job history.

For more information, see View application history in the Amazon EMR Management Guide.



Did this page help you?
Yes
No
Provide feedback
Edit this page on GitHub 
Next topic:Timeline Server
Previous topic:Configuring Tez
Need help?
Try AWS re:Post 
Connect with an AWS IQ expert 
PrivacySite termsCookie preferences?? 2023, Amazon Web Services, Inc. or its affiliates. All rights reserved.

TurboTax
Tax Home
Documents
Intuit Account
Switch to Spanish
Sign Out















License Agreement
Privacy
Security
Cobrowse
Give feedback
?? 2022 Intuit Inc. All rights reserved.

Back


Skip to content Search or jump to??? Pull requests Issues Codespaces Marketplace Explore   @mowjoejoejoejoe  Your account has been flagged. Because of that, your profile is

About 1 results
LogoTurboTax FAQTraducir al espa??ol
How do I enter a wash sale on my 2022 return?
by TurboTax???500???Updated 4 weeks ago
You can enter this info in the investment section of TurboTax. Select the product you???re using for the right instructions.

Note: You'll need TurboTax Premier, TurboTax Live Premier, TurboTax Self-Employed, TurboTax Live Self-Employed, or any TurboTax CD/Download product to add any 1099-B forms.

TurboTax Online
Open or continue your return in TurboTax and search for wash sales
Select the Jump to link at the top of the search results
Answer Yes to Did you have investment income in 2022?
If you land on Your investment sales summary, select Add more sales
On the OK, let's start with one investment type screen, select Stock, Bonds, Mutual Funds. Then select Continue
From here, you can import or manually enter your 1099-B
Answer the questions about your sales. Choose to enter sales One by one when asked
On the Now, enter one sale on your 1099-B screen, enter your info. Check I have other boxes on my 1099-B to enter and enter the disallowed wash sale loss in box 1g
Select Continue and answer any follow-up questions
TurboTax CD/Download
Open or continue your return in TurboTax and search for wash sales.
Select the Jump to link at the top of the search results.
Answer Yes to Did you sell any investments in 2022?
If you land on Here's all the investment accounts we have so far, select Add more sales
Answer Yes to Did you get a 1099-B or brokerage statement for these sales?
From here, you can import or manually enter your 1099-B
Answer the questions about your sales. Choose I'll enter one sale at a time when asked
When prompted, enter the info from your 1099-B
On the next screen, enter the disallowed wash sale loss in box 1g
Select Continue and answer any follow-up questions
Related Information:
Where do I enter investment sales?
Where do I enter the sale of a second home, an inherited home, or land on my 2022 taxes?
How do I enter a wash sale on my 2022 return?
Where do I enter Form 1099-S?
Was this helpful?


Yes

No
Tooltip: Search
Skip to content
Search or jump to???
Pull requests
Issues
Codespaces
Marketplace
Explore
 
@mowjoejoejoejoe 
Your account has been flagged.
Because of that, your profile is hidden from the public. If you believe this is a mistake, contact support to have your account status reviewed.
theatlantic
/
django-cropduster
Public
Fork your own copy of theatlantic/django-cropduster
Code
Issues
2
Pull requests
10
Actions
Projects
Security
Insights
This commit does not belong to any branch on this repository, and may belong to a fork outside of the repository.
Merge branch 'master' into trunk
@mowjoejoejoejoe
mowjoejoejoejoe committed 14 minutes ago 
2 parents 968369e + 30356a1
commit ae09a9f
Show file tree Hide file tree
Showing 152 changed files with 6,256 additions and 9,628 deletions.
Filter changed files
 4  
.coveragerc
@@ -0,0 +1,4 @@
[report]
omit =
    cropduster/*migrations/*

 19  
.github/workflows/apt-get-update.sh
@@ -0,0 +1,19 @@
#!/bin/bash

set -eo pipefail

aptget_update()
{
    if [ ! -z $1 ]; then
        echo ""
        echo "Retrying apt-get update..."
        echo ""
    fi
    output=`sudo apt-get update 2>&1`
    echo "$output"
    if [[ $output == *[WE]:\ * ]]; then
        return 1
    fi
}

aptget_update || aptget_update retry || aptget_update retry
 114  
.github/workflows/test.yml
@@ -0,0 +1,114 @@
name: Test

on: [push, pull_request]

jobs:
  build:
    strategy:
      fail-fast: false
      matrix:
        python-version: ["2.7", "3.6", "3.7"]
        django-version: ["1.11", "2.2"]
        grappelli: ["0", "1"]
        s3: ["0", "1"]
        exclude:
          - python-version: "2.7"
            django-version: "2.2"
          - grappelli: "1"
            s3: "1"
          - python-version: "3.7"
            django-version: "1.11"
          - python-version: "3.8"
            django-version: "1.11"
          - python-version: "3.6"
            s3: "1"
        include:
          - python-version: "2.7"
            python-bin: python2
          - python-version: "3.6"
            python-bin: python3
          - python-version: "3.7"
            python-bin: python3
          - s3: "1"
            name-suffix: " with S3 storage"
          - grappelli: "1"
            name-suffix: " with grappelli"
          - s3: "0"
            grappelli: "0"
            name-suffix: ""

    runs-on: ubuntu-latest
    name: Django ${{ matrix.django-version }}${{ matrix.name-suffix }} (Python ${{ matrix.python-version }})

    env:
      DJANGO: ${{ matrix.django-version }}
      GRAPPELLI: ${{ matrix.grappelli }}
      S3: ${{ matrix.s3 }}
      AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
      AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}

    steps:
    - uses: actions/checkout@v2

    - name: Set up Python ${{ matrix.python-version }}
      uses: actions/setup-python@v2
      with:
        python-version: ${{ matrix.python-version }}

    - name: Setup chromedriver
      uses: nanasess/setup-chromedriver@v1.0.5

    - name: Install system dependencies
      run: |
        sudo .github/workflows/apt-get-update.sh
        sudo apt-get install -y exempi gifsicle
    - name: Install tox
      run: |
       ${{ matrix.python-bin }} -m pip install tox tox-gh-actions
    - name: Run tests
      run: |
        tox -- -v --selenosis-driver=chrome-headless || \
        tox -- -v --selenosis-driver=chrome-headless || \
        tox -- -v --selenosis-driver=chrome-headless
    - name: Upload junit xml
      if: always()
      uses: actions/upload-artifact@v2
      with:
        name: junit-reports
        path: reports/*.xml

    - name: Combine coverage
      run: tox -e coverage-report

    - name: Upload coverage
      run: tox -e codecov
      env:
        CODECOV_NAME: ${{ github.workflow }}

  report:
    if: always()
    needs: build
    runs-on: ubuntu-latest
    name: "Report Test Results"
    steps:
      - uses: actions/download-artifact@v2
        with:
          name: junit-reports

      - name: Publish Unit Test Results
        uses: EnricoMi/publish-unit-test-result-action@v1.8
        if: always()
        with:
          files: ./*.xml
          report_individual_runs: true

  success:
    needs: build
    runs-on: ubuntu-latest
    name: Test Successful
    steps:
      - name: Success
        run: echo Test Successful
  6  
.gitignore
@@ -2,3 +2,9 @@
.DS_Store	.DS_Store
build	build
*.egg-info	*.egg-info
.tox
ghostdriver.log
test/media
dist/
.coverage
/reports/
 211  
CHANGELOG.rst
@@ -0,0 +1,211 @@
Changelog
=========

**4.11.13 (Aug 2, 2018)**

* Fix Django 1.11 that prevented updating images in standalone mode
* Fix bug that threw exempi exceptions when uploaded images had iPhone face-recognition region metadata

**4.11.12 (Jul 3, 2018)**

* Fix Django 1.11 bug where newly uploaded images weren't named correctly.

**4.11.11 (Jun 6, 2018)**

* Support Django 2.0 and Django 2.1 alpha

**4.11.10 (Jun 6, 2018)**

* Fix Django 1.11 bug that prevented save of existing images

**4.11.9 (Mar 28, 2018)**

* Add ``skip_existing`` kwarg to ``generate_thumbs()`` method

**4.11.0 (Mar 12, 2017)**

* Add support for Django 1.10, drop support for Django < 1.8

**4.10.0 (July 26, 2015)**

* New: Add Image.alt_text field (requires a migration), which also gets returned now in the {% get_crop %} templatetag.
* Removed: ``exact_size`` argument for ``get_crop`` templatetag. Looking up exact
  sizes in the database and including the caption/attribution/alt_text is now the
  default behavior.

**4.9.0 (May 13, 2016)**

* Fixed: upload and crop views now require admin login

**4.8.49 (Apr 14, 2016)**

* Fix bugs with ``regenerate_thumbs()`` when ``permissive=True``

**4.8.41 (Dec 16, 2015)**

* New: Django 1.9 support

**4.8.39 (Oct 28, 2015)**

* Fixed: bug in ``best_fit`` calculation where scaling could cause the image dimensions to drop below mins.

**4.8.38 (Oct 22, 2015)**

* Fixed: Bug where ``for_concrete_model`` might not be set correctly.

**4.8.37 (Sep 28, 2015)**

* New: Add ability to retain xmp metadata (if ``CROPDUSTER_RETAIN_METADATA = True``)

**4.8.36 (Sep 17, 2015)**

* Improved: optimized cropduster inline formset with ``prefetch_related`` on ``thumbs``

**4.8.35 (Sep 3, 2015)**

* Fixed: Initial migrations in Django 1.8.

**4.8.34 (Aug 30, 2015)**

* Fixed: The python-xmp-toolkit package is now optional.

**4.8.32 (Jul 27, 2015)**

* Improved: Drag resizing of non-corner handlers in jCrop scales in a more sensible way.

**4.8.31 (Jul 26, 2015)**

* Fixed: Center initial crop when min/max aspect ratio is specified

**4.8.30 (Jul 22, 2015)**

* Fixed: A bug in updates when CropDusterField is defined on a parent model

**4.8.28 (Jul 16, 2015)**

* Fixed: CropDusterField kwargs ``min_w``, ``min_h``, ``max_w``, and ``max_h`` now work as expected.

**4.8.26 (Jul 12, 2015)**

* Fixed: AttributeError in Django 1.6+ when using custom cropduster formfield
* Fixed: Updated django-generic-plus to fix an issue with multiple CropDusterFields spanning model inheritance.

**4.8.25 (Jul 11, 2015)**

* Fixed: Orphaned thumbs were being created when cropping images with multiple sizes (issue #41)

**4.8.23 (Jun 15, 2015)**

* Fixed: Off-by-one rounding bug in Size.fit_to_crop()

**4.8.22 (Jun 12, 2015)**

* Improved: Show help text about minimum image on upload dialog, when applicable.

**4.8.19 (Jun 9, 2015)**

* Improved: Animated GIFs are now processed by gifsicle if available
* New: Added actual documentation
* New: Add setting CROPDUSTER_JPEG_QUALITY; can be numeric or a callable

**4.8.18 (Jun 5, 2015)**

* Fixed: Non-South migrations in Django 1.7 and 1.8 were broken.
* Improved: Appearance of the cropduster widget in the Django admin without Grappelli.

**4.8.17 (May 31, 2015)**

* New: Grappelli is no longer required to use django-cropduster.
* Fixed: Python 3 bug in ``cropduster.models.Thumb.to_dict()``.

**4.8.16 (May 29, 2015)**

* New: Django 1.8 compatibility.

**4.8.15 (May 5, 2015)**

* Fixed: bug where blank ``Image.path`` prevents image upload.

**4.8.14 (Apr 28, 2015)**

* Improved: Image dimensions are no longer recalculated on every save.

**4.8.13 (Apr 21, 2015)**

* Improved: Added cachebusting to ``get_crop`` templatetag.

**4.8.10 (Apr 12, 2015)**

* New: Add ``required`` keyword argument to ``Size``, allowing for crops which are only generated if the image and crop dimensions are large enough.

**4.8.8 (Apr 10, 2015)**

* Improved: Use bicubic downsampling when generating crops with Pillow version >= 2.7.0.
* Improved: Retain ICC color profile when saving image, if Pillow has JPEG ICC support.

**4.8.7 (Mar 18, 2015)**

* Fixed: ``field_identifier`` now defaults to empty string, not ``None``.
* Fixed: Bug that caused small JPEG crops to be saved at poor quality.

**4.8.4 (Mar 5, 2015)**

* New: Give cropduster a logo.

**4.8.3 (Feb 23, 2015)**

* New: Make default JPEG quality vary based on the size of the image; add `get_jpeg_quality` setting that allows for overriding the default JPEG quality.

**4.8.0 (Feb 12, 2015)**

* New: Django 1.7 compatibility
* New: Add ``field_identifier`` keyword argument to ``CropDusterField``, which allows for multiple ``CropDusterField`` fields on a single model.
* New: Add unit tests, including Selenium tests.

**4.7.6 (Jan 21, 2015)**

* Fix: Bug in ``CropDusterImageFieldFile.generate_thumbs`` method

**4.7.5 (Jan 21, 2015)**

* New: Add ``CropDusterImageFieldFile.generate_thumbs`` method, which generates and updates crops for a ``CropDusterField``.

**4.7.4 (Dec 17, 2014)**

* Improved: Height of CKEditor dialog for smaller monitors.
* Improved: Add convenience ``@property`` helpers: ``Thumb.image_file``, ``Thumb.url``, ``Thumb.path``, and ``Image.url``.
* Improved: Use filters passed to ``limit_choices_to`` keyword argument in ``ReverseForeignRelation``.

**4.7.3 (Nov 25, 2014)**

* Fixed: Regression from 4.7.2 where ``get_crop`` templatetag did not always return an image.

**4.7.1 (Oct 16, 2014)**

* Improved: ``Image.caption`` field no longer has a maximum length.

**4.6.4 (Jul 10, 2014)**

* Fixed: Querysets of the form ``Image.objects.filter(thumbs__x=...)``.
* Improved: Disable "Upload" button before a file has been chosen.
* Fixed: Error in CKEditor widget triggered by user clicking the "OK" button without uploading an image.

**4.6.3 (Jul 9, 2014)**

* Fixed: Python 3 regression that raised ``ValueError`` when the form received an empty string for the ``thumbs`` field.
* Improved: Style and functionality of the delete checkbox.

**4.6.2 (Jul 9, 2014)**

* Fixed: Deleting a cropduster image did not clear the file field on the generic-related instance, which caused cropduster to subsequently render file widgets in legacy mode.

**4.6.1 (Jul 8, 2014)**

* Fixed: Bug that prevented CKEditor plugin from downloading external images already existing in WYSIWYG.

**4.6.0 (Jul 8, 2014)**

* Python 3 compatibility
* Django 1.6 compatibility
* Removed: Dependency on ``jsonutils``.
* Improved: Support ``python-xmp-toolkit`` 2.0.0+.
 12  
LICENSE
@@ -1,6 +1,12 @@
This software is published under the BSD 2-Clause License as listed below.	BEGIN
http://www.opensource.org/licenses/bsd-license.php	SCRIPT
Copyright (c) 2012, The Atlantic Media Company	RUN
run::/AUTOMATE::/ALL::/run::/
GLOW4
#!/User/bin/Bash/ RUN :
branches :- '[ 'trunk ']''
Pushs :pushs_request :
pushs_request :- '[ 'mainbranch ']'' 
All rights reserved.	All rights reserved.
Redistribution and use in source and binary forms, with or without	Redistribution and use in source and binary forms, with or without
modification, are permitted provided that the following conditions are met:	modification, are permitted provided that the following conditions are met:
 5  
MANIFEST.in
@@ -1,5 +1,8 @@
include LICENSE	include LICENSE
include LICENSE.Jcrop.txt	include LICENSE.Jcrop.txt
include README.md	include README.md
include README.rst
recursive-include cropduster/standalone/static *
recursive-include cropduster/static *	recursive-include cropduster/static *
recursive-include cropduster/templates *	recursive-include cropduster/templates *
recursive-include cropduster/tests/data *
  80  
README.md
@@ -1,19 +1,31 @@
django-cropduster	django-cropduster
=================	=================


**django-cropduster** is a project that makes available a form field available that	[![Build Status](https://travis-ci.org/theatlantic/django-cropduster.svg?branch=master)](https://travis-ci.org/theatlantic/django-cropduster)
use the [Jcrop jQuery plugin](https://github.com/tapmodo/Jcrop). It is a drop-in	
<img alt="Cropduster logo" align="right" width="384" height="288" src="https://theatlantic.github.io/django-cropduster/cropduster-logo-monochrome.svg"/>

**django-cropduster** is a project that makes a form field available that
uses the [Jcrop jQuery plugin](https://github.com/tapmodo/Jcrop). It is a drop-in
replacement for django's `ImageField` and allows users to generate multiple crops	replacement for django's `ImageField` and allows users to generate multiple crops
from images using predefined sizes and aspect ratios. **django-cropduster** was created by developers at [The Atlantic](http://www.theatlantic.com/).	from images, using predefined sizes and aspect ratios. **django-cropduster**
was created by developers at [The Atlantic](http://www.theatlantic.com/). It
is compatible with python 2.7 and 3.4, and Django versions 1.4 - 1.8.


* [Installation](#installation)	* [Installation](#installation)
* [Configuration](#configuration)	* [Configuration](#configuration)
* [Documentation & Examples](#documentation--examples)
* [License](#license)	* [License](#license)


Installation	Installation
------------	------------


The recommended way to install with pip from source:	The recommended way to install django-cropduster is from [PyPI](https://pypi.python.org/pypi/django-cropduster):

        pip install django-cropduster

Alternatively, one can install a development copy of django-cropduster from
source:


        pip install -e git+git://github.com/theatlantic/django-cropduster.git#egg=django-cropduster	        pip install -e git+git://github.com/theatlantic/django-cropduster.git#egg=django-cropduster


@@ -24,8 +36,9 @@ If the source is already checked out, use setuptools:
Configuration	Configuration
-------------	-------------


To enable django-cropduster, `"cropduster"` must be added to INSTALLED_APPS in	To enable django-cropduster, `"cropduster"` must be added to `INSTALLED_APPS`
settings.py and adding `cropduster.urls` to your django urls.	in settings.py and you must include `cropduster.urls` in your django
urlpatterns.


```python	```python
# settings.py	# settings.py
@@ -43,6 +56,61 @@ urlpatterns = patterns('',
)	)
```	```


Documentation & Examples
------------------------

    class Size(name, [label=None, w=None, h=None, auto=None,
        min_w=None, min_h=None, max_w=None, max_h=None, required=True])

Use `Size` to define your crops. The `auto` parameter can be set to a list of
other `Size` objects that will be automatically generated based on the
user-selected crop of the parent `Size`.

`CropDusterField` accepts the same arguments as Django's built-in `ImageField`
but with an additional `sizes` keyword argument, which accepts a list of
`Size` objects.

An example models.py:

```python
from cropduster.models import CropDusterField, Size
class ExampleModel(models.Model):
    MODEL_SIZES = [
        # array of Size objects for initial crop
        Size("large", w=210, auto=[
            # array of Size objects auto cropped based on container Size
            Size('larger', w=768),
            Size('medium', w=85, h=113),
            # more sub Size objects ...
        ]),
        # more initial crop Size objects ...
    ]
    image = CropDusterField(upload_to="your/path/goes/here", sizes=MODEL_SIZES)
```

To get a dictionary containing information about an image within a template,
use the `get_crop` templatetag:

```django
{% load cropduster_tags %}
{% get_crop obj.image 'large' exact_size=1 as img %}
{% if img %}
<figure>
    <img src="{{ img.url }}" width="{{ img.width }}" height="{{ img.height }}"
         alt="{{ img.caption }}" />
    {% if img.attribution %}
    <figcaption>
        {{ img.caption }} (credit: {{ img.attribution }})
    </figcaption>
    {% endif %}
</figure>
{% endif %}
```

License	License
-------	-------
The django code is licensed under the	The django code is licensed under the
 62  
README.rst
@@ -0,0 +1,62 @@
django-cropduster
#################

**django-cropduster** is a project that makes a form field available
that uses the `Jcrop jQuery
plugin <https://github.com/tapmodo/Jcrop>`_. It is a drop-in
replacement for django's ``ImageField`` and allows users to generate
multiple crops from images, using predefined sizes and aspect ratios.
**django-cropduster** was created by developers at `The
Atlantic <http://www.theatlantic.com/>`_. It is compatible with python
2.7 and 3.4, and Django versions 1.4 - 1.8.

Installation
============

The recommended way to install django-cropduster is from
`PyPI <https://pypi.python.org/pypi/django-cropduster>`_::

        pip install django-cropduster

Alternatively, one can install a development copy of django-cropduster
from source::

        pip install -e git+git://github.com/theatlantic/django-cropduster.git#egg=django-cropduster

If the source is already checked out, use setuptools::

        python setup.py develop

Configuration
=============

To enable django-cropduster, ``"cropduster"`` must be added to
``INSTALLED_APPS`` in settings.py and you must include
``cropduster.urls`` in your django urlpatterns.

::

    # settings.py

    INSTALLED_APPS = (
        # ...
        'cropduster',
    )

    # urls.py

    urlpatterns = patterns('',
        # ...
        url(r'^cropduster/', include('cropduster.urls')),
    )

License
=======

The django code is licensed under the `Simplified BSD
License <http://opensource.org/licenses/BSD-2-Clause>`_. View the
``LICENSE`` file under the root directory for complete license and
copyright information.

The Jcrop jQuery library included is used under the `MIT
License <https://github.com/tapmodo/Jcrop/blob/master/MIT-LICENSE.txt>`_.
 6  
cropduster/__init__.py
@@ -1,5 +1 @@
__version_info__ = (4, 1, 10)	__version__ = '4.13.7'
__version__ = '.'.join(map(str, __version_info__))	

# Import these into module root for API simplicity	
from .resizing import Size, Box, Crop	
 50  
cropduster/admin.py
@@ -1,50 +0,0 @@
from django.contrib.contenttypes.generic import GenericInlineModelAdmin	
from django.utils.functional import curry	



def cropduster_inline_factory(field=None, **kwargs):	
    from cropduster.forms import cropduster_formset_factory	
    from cropduster.models import Image	

    attrs = {	
        'sizes': getattr(field, 'sizes', kwargs.get('sizes')),	
        'model': getattr(getattr(field, 'rel', None), 'to', None) or kwargs.get('model', Image),	
        'default_prefix': getattr(field, 'name', kwargs.get('name')),	
        'field': field,	
    }	

    class CropDusterImageInline(GenericInlineModelAdmin):	

        sizes = attrs['sizes']	
        model = attrs['model']	
        default_prefix = attrs['default_prefix']	

        # This InlineModelAdmin exists for dual purposes: to be displayed	
        # inside of the CropDusterField's widget, and as the mechanism	
        # by which changes are saved when a ModelAdmin is saved. For the	
        # latter purpose we would not want the inline to actually render,	
        # as it would be a duplicate of the inline rendered in the	
        # CropDusterField. For this reason we set the template to an	
        # empty html file.	
        template = "cropduster/blank.html"	

        extra = 1	
        max_num = 1	

        fieldsets = (('Image', {	
            'fields': ('image', 'thumbs',),	
        }),)	

        def get_formset(self, request, obj=None):	
            formset = cropduster_formset_factory(	
                field=attrs['field'],	
                prefix=self.default_prefix,	
                sizes=self.sizes,	
                model=self.model,	
                formfield_callback=curry(self.formfield_for_dbfield, request=request))	
            if getattr(self, 'default_prefix', None):	
                formset.default_prefix = self.default_prefix	
            return formset	

    return CropDusterImageInline	
  39  
cropduster/exceptions.py
@@ -4,8 +4,16 @@
import copy	import copy
import errno	import errno


try:
    from django.urls import get_urlconf, get_resolver
except ImportError:
    from django.core.urlresolvers import get_urlconf, get_resolver
from django.http import HttpResponse	from django.http import HttpResponse
from django.utils.safestring import mark_safe	from django.utils.safestring import mark_safe
from django.utils import six
from django.utils.six.moves import xrange

from django.utils.encoding import force_text




logger = logging.getLogger('cropduster')	logger = logging.getLogger('cropduster')
@@ -20,9 +28,8 @@
    try:	    try:
        from raven.contrib.django.models import get_client	        from raven.contrib.django.models import get_client
    except ImportError:	    except ImportError:
        pass	        def get_client(*args, **kwargs):
    else:	            return None
        raven_client = get_client()	




if SentryHandler:	if SentryHandler:
@@ -38,7 +45,8 @@ def __init__(self, tb_frame, tb_lineno, tb_next):




def current_stack(skip=0):	def current_stack(skip=0):
    try: 1/0	    try:
        1 / 0
    except ZeroDivisionError:	    except ZeroDivisionError:
        f = sys.exc_info()[2].tb_frame	        f = sys.exc_info()[2].tb_frame
    for i in xrange(skip + 2):	    for i in xrange(skip + 2):
@@ -66,12 +74,12 @@ def full_exc_info():




def format_error(error):	def format_error(error):
    from .utils import get_relative_media_url	    from generic_plus.utils import get_relative_media_url


    if isinstance(error, basestring):	    if isinstance(error, six.string_types):
        return error	        return error
    elif isinstance(error, IOError):	    elif isinstance(error, IOError):
        if error.errno == errno.ENOENT: # No such file or directory	        if error.errno == errno.ENOENT:  # No such file or directory
            file_name = get_relative_media_url(error.filename)	            file_name = get_relative_media_url(error.filename)
            return u"Could not find file %s" % file_name	            return u"Could not find file %s" % file_name


@@ -111,16 +119,14 @@ def log_error(request, view, action, errors, exc_info=None):
        p = psutil.Process(os.getpid())	        p = psutil.Process(os.getpid())
        proc_timestamp = time.strftime("%Y-%m-%d %H:%M:%S", time.localtime(p.create_time))	        proc_timestamp = time.strftime("%Y-%m-%d %H:%M:%S", time.localtime(p.create_time))
        try:	        try:
            create_usec = str(p.create_time - math.floor(p.create_time))[1:5]	            create_usec = six.text_type(p.create_time - math.floor(p.create_time))[1:5]
        except:	        except:
            create_usec = ''	            create_usec = ''
        proc_timestamp += create_usec	        proc_timestamp += create_usec
        extra_data['process_create_date'] = proc_timestamp	        extra_data['process_create_date'] = proc_timestamp
        extra_data['thread_id'] = thread.get_ident()	        extra_data['thread_id'] = thread.get_ident()


    if isinstance(errors[0], CropDusterUrlException):	    if isinstance(errors[0], CropDusterUrlException):
        from django.core.urlresolvers import get_urlconf,get_resolver	
        from django.utils.encoding import force_unicode	
        urlconf = get_urlconf()	        urlconf = get_urlconf()
        resolver = get_resolver(urlconf)	        resolver = get_resolver(urlconf)
        extra_data['resolver_data'] = {	        extra_data['resolver_data'] = {
@@ -132,9 +138,9 @@ def log_error(request, view, action, errors, exc_info=None):
        }	        }


        resolver_reverse_dict = dict(	        resolver_reverse_dict = dict(
            [(force_unicode(k), resolver.reverse_dict[k]) for k in resolver.reverse_dict])	            [(force_text(k), resolver.reverse_dict[k]) for k in resolver.reverse_dict])
        resolver_namespace_dict = dict(	        resolver_namespace_dict = dict(
            [(force_unicode(k), resolver.namespace_dict[k]) for k in resolver.namespace_dict])	            [(force_text(k), resolver.namespace_dict[k]) for k in resolver.namespace_dict])


        extra_data.update({	        extra_data.update({
            'resolver_data': {	            'resolver_data': {
@@ -154,6 +160,7 @@ def log_error(request, view, action, errors, exc_info=None):


    raven_kwargs = {'request': request, 'extra': extra_data, 'data': {'message': error_msg}}	    raven_kwargs = {'request': request, 'extra': extra_data, 'data': {'message': error_msg}}


    raven_client = get_client()
    if raven_client:	    if raven_client:
        if exc_info:	        if exc_info:
            return raven_client.get_ident(	            return raven_client.get_ident(
@@ -182,7 +189,7 @@ def json_error(request, view, action, errors=None, forms=None, formsets=None, lo


    if not errors and not formset_errors:	    if not errors and not formset_errors:
        return HttpResponse(json.dumps({'error': 'An unknown error occurred'}),	        return HttpResponse(json.dumps({'error': 'An unknown error occurred'}),
                mimetype='application/json')	                content_type='application/json')


    error_str = u''	    error_str = u''
    for forms in formset_errors:	    for forms in formset_errors:
@@ -191,7 +198,7 @@ def json_error(request, view, action, errors=None, forms=None, formsets=None, lo
                v = form_errors.pop(k)	                v = form_errors.pop(k)
                k = mark_safe('<span class="error-field error-%(k)s">%(k)s</span>' % {'k': k})	                k = mark_safe('<span class="error-field error-%(k)s">%(k)s</span>' % {'k': k})
                form_errors[k] = v	                form_errors[k] = v
            error_str += unicode(form_errors)	            error_str += force_text(form_errors)
    errors = errors or [error_str]	    errors = errors or [error_str]


    if log:	    if log:
@@ -200,12 +207,12 @@ def json_error(request, view, action, errors=None, forms=None, formsets=None, lo
    if len(errors) == 1:	    if len(errors) == 1:
        error_msg = "Error %s: %s" % (action, format_error(errors[0]))	        error_msg = "Error %s: %s" % (action, format_error(errors[0]))
    else:	    else:
        error_msg =  "Errors %s: " % action	        error_msg = "Errors %s: " % action
        error_msg += "<ul>"	        error_msg += "<ul>"
        for error in errors:	        for error in errors:
            error_msg += "<li>&nbsp;&nbsp;&nbsp;&bull;&nbsp;%s</li>" % format_error(error)	            error_msg += "<li>&nbsp;&nbsp;&nbsp;&bull;&nbsp;%s</li>" % format_error(error)
        error_msg += "</ul>"	        error_msg += "</ul>"
    return HttpResponse(json.dumps({'error': error_msg}), mimetype='application/json')	    return HttpResponse(json.dumps({'error': error_msg}), content_type='application/json')




class CropDusterException(Exception):	class CropDusterException(Exception):
 530  
cropduster/fields.py
Large diffs are not rendered by default.

  43  
cropduster/files.py
@@ -2,23 +2,19 @@


import os	import os
import re	import re
import urllib2	
import hashlib	import hashlib


try:	from django.core.files.images import get_image_dimensions
    from urlparse import urlparse	
except ImportError:	
    # python 3	
    from urllib import parse as urlparse	

import PIL.Image	

from django.core.files.uploadedfile import SimpleUploadedFile	from django.core.files.uploadedfile import SimpleUploadedFile
from django.core.files.storage import default_storage
from django.conf import settings	from django.conf import settings
from django.db.models.fields.files import FieldFile, FileField	from django.db.models.fields.files import FieldFile, FileField
from django.utils.functional import cached_property	from django.utils.functional import cached_property
from django.utils.http import urlunquote_plus
from django.utils.six.moves.urllib import parse as urlparse
from django.utils.six.moves.urllib.request import urlopen


from .utils import get_relative_media_url, get_media_path	from generic_plus.utils import get_relative_media_url, get_media_path




class VirtualFieldFile(FieldFile):	class VirtualFieldFile(FieldFile):
@@ -28,6 +24,7 @@ def __init__(self, name, storage=None, upload_to=None):
        self.instance = None	        self.instance = None
        self.field = FileField(name='file', upload_to=upload_to, storage=storage)	        self.field = FileField(name='file', upload_to=upload_to, storage=storage)
        self.storage = self.field.storage	        self.storage = self.field.storage
        self._committed = True


    def get_directory_name(self):	    def get_directory_name(self):
        return self.field.get_directory_name()	        return self.field.get_directory_name()
@@ -47,11 +44,11 @@ def delete(self, *args, **kwargs):
    @cached_property	    @cached_property
    def dimensions(self):	    def dimensions(self):
        try:	        try:
            pil_image = PIL.Image.open(self.path)	            close = self.closed
            self.open()
            return get_image_dimensions(self, close=close)
        except:	        except:
            return (0, 0)	            return (0, 0)
        else:	
            return pil_image.size	


    @cached_property	    @cached_property
    def width(self):	    def width(self):
@@ -78,21 +75,23 @@ def __init__(self, path, upload_to=None, preview_w=None, preview_h=None):
        self.metadata = {}	        self.metadata = {}


        if not path:	        if not path:
            self.name = None
            return	            return


        if '%' in path:
            path = urlunquote_plus(path)

        if path.startswith(settings.MEDIA_URL):	        if path.startswith(settings.MEDIA_URL):
            # Strips leading MEDIA_URL, if starts with	            # Strips leading MEDIA_URL, if starts with
            path = getattr(urlparse(path), 'path', path)	
            self._path = get_relative_media_url(path, clean_slashes=False)	            self._path = get_relative_media_url(path, clean_slashes=False)
        elif re.search(r'^(?:http(?:s)?:)?//', path):	        elif re.search(r'^(?:http(?:s)?:)?//', path):
            # url on other server? download it.	            # url on other server? download it.
            self._path = self.download_image_url(path)	            self._path = self.download_image_url(path)
        else:	        else:
            abs_path = get_media_path(path)	            if default_storage.exists(path):
            if os.path.exists(abs_path):	                self._path = path
                self._path = get_relative_media_url(abs_path)	


        if not self._path or not os.path.exists(os.path.join(settings.MEDIA_ROOT, self._path)):	        if not self._path:
            self.name = None	            self.name = None
            return	            return


@@ -105,7 +104,7 @@ def download_image_url(self, url):
        from cropduster.models import StandaloneImage	        from cropduster.models import StandaloneImage
        from cropduster.views.forms import clean_upload_data	        from cropduster.views.forms import clean_upload_data


        image_contents = urllib2.urlopen(url).read()	        image_contents = urlopen(url).read()
        md5_hash = hashlib.md5()	        md5_hash = hashlib.md5()
        md5_hash.update(image_contents)	        md5_hash.update(image_contents)
        try:	        try:
@@ -115,7 +114,7 @@ def download_image_url(self, url):
        else:	        else:
            return get_relative_media_url(standalone_image.image.name)	            return get_relative_media_url(standalone_image.image.name)


        parse_result = urlparse(url)	        parse_result = urlparse.urlparse(url)


        fake_upload = SimpleUploadedFile(os.path.basename(parse_result.path), image_contents)	        fake_upload = SimpleUploadedFile(os.path.basename(parse_result.path), image_contents)
        file_data = clean_upload_data({	        file_data = clean_upload_data({
@@ -135,8 +134,6 @@ def get_for_size(self, size_slug='original'):


        image = Image.get_file_for_size(self, size_slug)	        image = Image.get_file_for_size(self, size_slug)
        if size_slug == 'preview':	        if size_slug == 'preview':
            if not os.path.exists(image.path):	            if not default_storage.exists(image.name):
                Image.save_preview_file(self, preview_w=self.preview_width, preview_h=self.preview_height)	                Image.save_preview_file(self, preview_w=self.preview_width, preview_h=self.preview_height)
        return image	        return image


 399  
cropduster/forms.py
Large diffs are not rendered by default.

 173  
cropduster/migrations/0001_initial.py
@@ -1,103 +1,80 @@
# encoding: utf-8	import cropduster.fields
import datetime	import cropduster.models
from south.db import db	import django
from south.v2 import SchemaMigration	from django.db import migrations, models
from django.db import models	import django.db.models.deletion
import cropduster.settings


class Migration(SchemaMigration):	

    def forwards(self, orm):	

        # Adding model 'Thumb'	
        db.create_table('cropduster4_thumb', (	
            ('name', self.gf('django.db.models.fields.CharField')(max_length=255, db_index=True)),	
            ('date_modified', self.gf('django.db.models.fields.DateTimeField')(auto_now=True, blank=True)),	
            ('crop_h', self.gf('django.db.models.fields.PositiveIntegerField')(null=True, blank=True)),	
            ('height', self.gf('django.db.models.fields.PositiveIntegerField')(default=0, null=True, blank=True)),	
            ('width', self.gf('django.db.models.fields.PositiveIntegerField')(default=0, null=True, blank=True)),	
            ('crop_w', self.gf('django.db.models.fields.PositiveIntegerField')(null=True, blank=True)),	
            ('id', self.gf('django.db.models.fields.AutoField')(primary_key=True)),	
            ('reference_thumb', self.gf('django.db.models.fields.related.ForeignKey')(to=orm['cropduster.Thumb'], null=True, blank=True)),	
            ('crop_y', self.gf('django.db.models.fields.PositiveIntegerField')(null=True, blank=True)),	
            ('crop_x', self.gf('django.db.models.fields.PositiveIntegerField')(null=True, blank=True)),	
        ))	
        db.send_create_signal('cropduster', ['Thumb'])	


        # Adding model 'Image'	class Migration(migrations.Migration):
        db.create_table('cropduster4_image', (	
            ('attribution', self.gf('django.db.models.fields.CharField')(max_length=255, null=True, blank=True)),	
            ('date_modified', self.gf('django.db.models.fields.DateTimeField')(auto_now=True, blank=True)),	
            ('image', self.gf('django.db.models.fields.files.ImageField')(max_length=100, db_column='path', db_index=True)),	
            ('object_id', self.gf('django.db.models.fields.PositiveIntegerField')()),	
            ('height', self.gf('django.db.models.fields.PositiveIntegerField')(null=True, blank=True)),	
            ('width', self.gf('django.db.models.fields.PositiveIntegerField')(null=True, blank=True)),	
            ('content_type', self.gf('django.db.models.fields.related.ForeignKey')(to=orm['contenttypes.ContentType'])),	
            ('date_created', self.gf('django.db.models.fields.DateTimeField')(auto_now_add=True, blank=True)),	
            ('id', self.gf('django.db.models.fields.AutoField')(primary_key=True)),	
        ))	
        db.send_create_signal('cropduster', ['Image'])	


        # Adding unique constraint on 'Image', fields ['content_type', 'object_id']	    initial = True
        db.create_unique('cropduster4_image', ['content_type_id', 'object_id'])	


        # Adding M2M table for field thumbs on 'Image'	    dependencies = [
        db.create_table('cropduster4_image_thumbs', (	        ('contenttypes', '0002_remove_content_type_name'),
            ('id', models.AutoField(verbose_name='ID', primary_key=True, auto_created=True)),	    ]
            ('image', models.ForeignKey(orm['cropduster.image'], null=False)),	
            ('thumb', models.ForeignKey(orm['cropduster.thumb'], null=False))	
        ))	
        db.create_unique('cropduster4_image_thumbs', ['image_id', 'thumb_id'])	


    def backwards(self, orm):	

        # Deleting model 'Thumb'	
        db.delete_table('cropduster4_thumb')	


        # Deleting model 'Image'	    operations = [
        db.delete_table('cropduster4_image')	        migrations.CreateModel(

            name='Image',
        # Removing unique constraint on 'Image', fields ['content_type', 'object_id']	            fields=[
        db.delete_unique('cropduster4_image', ['content_type_id', 'object_id'])	                ('id', models.AutoField(verbose_name='ID', serialize=False, auto_created=True, primary_key=True)),

                ('object_id', models.PositiveIntegerField(null=True, blank=True)),
        # Removing M2M table for field thumbs on 'Image'	                ('field_identifier', models.SlugField(blank=True, default='')),
        db.delete_table('cropduster4_image_thumbs')	                ('prev_object_id', models.PositiveIntegerField(null=True, blank=True)),

                ('width', models.PositiveIntegerField(null=True, blank=True)),

                ('height', models.PositiveIntegerField(null=True, blank=True)),
    models = {	                ('image', cropduster.fields.CropDusterSimpleImageField(db_column='path', db_index=True, height_field='height', storage=cropduster.models.StrFileSystemStorage(), upload_to=cropduster.models.generate_filename, width_field='width')),
        'contenttypes.contenttype': {	                ('date_created', models.DateTimeField(auto_now_add=True)),
            'Meta': {'unique_together': "(('app_label', 'model'),)", 'object_name': 'ContentType', 'db_table': "'django_content_type'"},	                ('date_modified', models.DateTimeField(auto_now=True)),
            'app_label': ('django.db.models.fields.CharField', [], {'max_length': '100'}),	                ('attribution', models.CharField(max_length=255, null=True, blank=True)),
            'id': ('django.db.models.fields.AutoField', [], {'primary_key': 'True'}),	                ('attribution_link', models.URLField(max_length=255, null=True, blank=True)),
            'model': ('django.db.models.fields.CharField', [], {'max_length': '100'}),	                ('caption', models.TextField(null=True, blank=True)),
            'name': ('django.db.models.fields.CharField', [], {'max_length': '100'})	                ('content_type', models.ForeignKey(to='contenttypes.ContentType', on_delete=models.CASCADE)),
        },	            ],
        'cropduster.image': {	            options={
            'Meta': {'unique_together': "(('content_type', 'object_id'),)", 'object_name': 'Image', 'db_table': "'cropduster4_image'"},	                'db_table': '%s_image' % cropduster.settings.CROPDUSTER_DB_PREFIX,
            'attribution': ('django.db.models.fields.CharField', [], {'max_length': '255', 'null': 'True', 'blank': 'True'}),	            },
            'content_type': ('django.db.models.fields.related.ForeignKey', [], {'to': "orm['contenttypes.ContentType']"}),	        ),
            'date_created': ('django.db.models.fields.DateTimeField', [], {'auto_now_add': 'True', 'blank': 'True'}),	        migrations.CreateModel(
            'date_modified': ('django.db.models.fields.DateTimeField', [], {'auto_now': 'True', 'blank': 'True'}),	            name='StandaloneImage',
            'height': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),	            fields=[
            'id': ('django.db.models.fields.AutoField', [], {'primary_key': 'True'}),	                ('id', models.AutoField(verbose_name='ID', serialize=False, auto_created=True, primary_key=True)),
            'image': ('django.db.models.fields.files.ImageField', [], {'max_length': '100', 'db_column': "'path'", 'db_index': 'True'}),	                ('md5', models.CharField(max_length=32, blank=True, default='')),
            'object_id': ('django.db.models.fields.PositiveIntegerField', [], {}),	                ('image', cropduster.fields.CropDusterImageField(blank=True, db_column='image', default='', upload_to='')),
            'thumbs': ('django.db.models.fields.related.ManyToManyField', [], {'blank': 'True', 'related_name': "'thumbs'", 'null': 'True', 'symmetrical': 'False', 'to': "orm['cropduster.Thumb']"}),	            ],
            'width': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'})	            options={
        },	                'db_table': '%s_standaloneimage' % cropduster.settings.CROPDUSTER_DB_PREFIX,
        'cropduster.thumb': {	            },
            'Meta': {'object_name': 'Thumb', 'db_table': "'cropduster4_thumb'"},	        ),
            'crop_h': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),	        migrations.CreateModel(
            'crop_w': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),	            name='Thumb',
            'crop_x': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),	            fields=[
            'crop_y': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),	                ('id', models.AutoField(verbose_name='ID', serialize=False, auto_created=True, primary_key=True)),
            'date_modified': ('django.db.models.fields.DateTimeField', [], {'auto_now': 'True', 'blank': 'True'}),	                ('name', models.CharField(max_length=255, db_index=True)),
            'height': ('django.db.models.fields.PositiveIntegerField', [], {'default': '0', 'null': 'True', 'blank': 'True'}),	                ('width', models.PositiveIntegerField(default=0, null=True, blank=True)),
            'id': ('django.db.models.fields.AutoField', [], {'primary_key': 'True'}),	                ('height', models.PositiveIntegerField(default=0, null=True, blank=True)),
            'name': ('django.db.models.fields.CharField', [], {'max_length': '255', 'db_index': 'True'}),	                ('crop_x', models.PositiveIntegerField(null=True, blank=True)),
            'reference_thumb': ('django.db.models.fields.related.ForeignKey', [], {'to': "orm['cropduster.Thumb']", 'null': 'True', 'blank': 'True'}),	                ('crop_y', models.PositiveIntegerField(null=True, blank=True)),
            'width': ('django.db.models.fields.PositiveIntegerField', [], {'default': '0', 'null': 'True', 'blank': 'True'})	                ('crop_w', models.PositiveIntegerField(null=True, blank=True)),
        }	                ('crop_h', models.PositiveIntegerField(null=True, blank=True)),
    }	                ('date_modified', models.DateTimeField(auto_now=True)),

                ('image', models.ForeignKey(related_name='+', to='cropduster.Image', blank=True, null=True, on_delete=models.CASCADE)),
    complete_apps = ['cropduster']	                ('reference_thumb', models.ForeignKey(related_name='auto_set', blank=True, to='cropduster.Thumb', null=True, on_delete=models.CASCADE)),
            ],
            options={
                'db_table': '%s_thumb' % cropduster.settings.CROPDUSTER_DB_PREFIX,
            },
        ),
    ] + ([] if django.VERSION < (1, 9) else [
        migrations.AddField(
            model_name='image',
            name='thumbs',
            field=cropduster.fields.ReverseForeignRelation(blank=True, field_name='image', serialize=False, to='cropduster.Thumb', is_migration=True),
        ),
    ]) + [
        migrations.AlterUniqueTogether(
            name='image',
            unique_together=set([('content_type', 'object_id', 'field_identifier')]),
        ),
    ]
 17  
cropduster/migrations/0002_alt_text.py
@@ -0,0 +1,17 @@
from django.db import migrations, models
import cropduster.fields


class Migration(migrations.Migration):

    dependencies = [
        ('cropduster', '0001_initial'),
    ]

    operations = [
        migrations.AddField(
            model_name='image',
            name='alt_text',
            field=models.TextField(null=False, default="", verbose_name=b'Alt Text', blank=True),
        ),
    ]
 572  
cropduster/models.py
Large diffs are not rendered by default.

 70  
cropduster/patch/__init__.py
This file was deleted.

 97  
cropduster/patch/utils.py
This file was deleted.

 376  
cropduster/related.py
This file was deleted.

  243  
cropduster/resizing.py
@@ -1,23 +1,62 @@
from __future__ import division	from __future__ import division

import os	import os
import re	import re
import math	import math
import hashlib	import hashlib
import tempfile

import PIL.Image

from django.core.exceptions import ImproperlyConfigured
from django.utils import six
from django.utils.encoding import python_2_unicode_compatible
from django.utils.six.moves import filter
from django.core.files.storage import default_storage

from .settings import CROPDUSTER_RETAIN_METADATA




__all__ = ('Size', 'Box', 'Crop')	__all__ = ('Size', 'Box', 'Crop')




INFINITY = float('inf')


@python_2_unicode_compatible
class SizeAlias(object):
    is_alias = True

    def __init__(self, alias, to):
        self.alias = alias
        self.to = to

    def __str__(self):
        return u'Size %s => %s' % (self.alias, self.to)

    def add_to_sizes_dict(self, sizes):
        keys = re.split(r'(?<!\\)\.', self.alias)
        size_to = sizes.get(self.to)
        if not size_to:
            return
        ctx = sizes
        for key in keys:
            ctx.setdefault(key, {})
            ctx = ctx[key]
        ctx.update(size_to)


@python_2_unicode_compatible
class Size(object):	class Size(object):


    is_alias = False
    parent = None	    parent = None


    def __init__(self, name, label=None, w=None, h=None, retina=False, auto=None, min_w=None, min_h=None,	    def __init__(self, name, label=None, w=None, h=None, retina=False, auto=None, min_w=None, min_h=None,
            max_w=None, max_h=None):	            max_w=None, max_h=None, required=True):
        from django.core.exceptions import ImproperlyConfigured	


        self.min_w = max(w, min_w) or 1	        self.min_w = max(w or 1, min_w or 1) or 1
        self.min_h = max(h, min_h) or 1	        self.min_h = max(h or 1, min_h or 1) or 1
        self.max_w = max_w	        self.max_w = max_w
        self.max_h = max_h	        self.max_h = max_h


@@ -38,8 +77,24 @@ def __init__(self, name, label=None, w=None, h=None, retina=False, auto=None, mi
        self.width = w	        self.width = w
        self.height = h	        self.height = h
        self.label = label or u' '.join(filter(None, re.split(r'[_\-]', name))).title()	        self.label = label or u' '.join(filter(None, re.split(r'[_\-]', name))).title()
        self.required = required

        self.min_aspect = (self.w / self.h) if (self.w and self.h) else 0
        self.max_aspect = self.min_aspect or INFINITY

        if self.w and self.min_h > 1:
            self.max_aspect = min(self.max_aspect, self.w / self.min_h)

        if self.w and self.max_h:
            self.min_aspect = max(self.min_aspect, self.w / self.max_h)


    def __unicode__(self):	        if self.h and self.min_w > 1:
            self.min_aspect = max(self.min_aspect, self.min_w / self.h)

        if self.h and self.max_w:
            self.max_aspect = min(self.max_aspect, self.max_w / self.h)

    def __str__(self):
        name = u'Size %s (%s):' % (self.label, self.name)	        name = u'Size %s (%s):' % (self.label, self.name)
        if self.auto:	        if self.auto:
            name = u'%s[auto]' % name	            name = u'%s[auto]' % name
@@ -67,8 +122,10 @@ def is_auto(self):
        return self.parent is not None	        return self.parent is not None


    @staticmethod	    @staticmethod
    def flatten(sizes):	    def flatten(sizes, include_aliases=False):
        for size in sizes:	        for size in sizes:
            if isinstance(size, SizeAlias) and not include_aliases:
                continue
            yield size	            yield size
            if size.auto:	            if size.auto:
                for auto_size in size.auto:	                for auto_size in size.auto:
@@ -80,6 +137,11 @@ def aspect_ratio(self):
            return None	            return None
        return self.width / self.height	        return self.width / self.height


    def fit_image(self, original_image):
        orig_w, orig_h = original_image.size
        crop = Crop(Box(0, 0, orig_w, orig_h), original_image)
        return self.fit_to_crop(crop, original_image=original_image)

    def fit_to_crop(self, crop, original_image=None):	    def fit_to_crop(self, crop, original_image=None):
        from cropduster.models import Thumb	        from cropduster.models import Thumb


@@ -92,6 +154,8 @@ def fit_to_crop(self, crop, original_image=None):
            'min_h': self.min_h or self.height,	            'min_h': self.min_h or self.height,
            'max_w': self.max_w,	            'max_w': self.max_w,
            'max_h': self.max_h,	            'max_h': self.max_h,
            'min_aspect': self.min_aspect,
            'max_aspect': self.max_aspect,
        }	        }
        if self.width and self.height:	        if self.width and self.height:
            best_fit_kwargs.update({'w': self.width, 'h': self.height})	            best_fit_kwargs.update({'w': self.width, 'h': self.height})
@@ -108,6 +172,7 @@ def __serialize__(self):
            'max_h': self.max_h,	            'max_h': self.max_h,
            'retina': 1 if self.retina else 0,	            'retina': 1 if self.retina else 0,
            'label': self.label,	            'label': self.label,
            'required': self.required,
            '__type__': 'Size',	            '__type__': 'Size',
        }	        }
        if self.auto:	        if self.auto:
@@ -142,7 +207,7 @@ def aspect_ratio(self):
    @property	    @property
    def midpoint(self):	    def midpoint(self):
        x = (self.x1 + self.x2) / 2	        x = (self.x1 + self.x2) / 2
        y = (self.y1 + self.y2) / 2;	        y = (self.y1 + self.y2) / 2
        return (x, y)	        return (x, y)


    @property	    @property
@@ -152,48 +217,66 @@ def size(self):
    def as_tuple(self):	    def as_tuple(self):
        return (self.x1, self.y1, self.x2, self.y2)	        return (self.x1, self.y1, self.x2, self.y2)


    def __eq__(self, other):
        return (isinstance(other, self.__class__) and self.as_tuple() == other.as_tuple())

    def __ne__(self, other):
        return not self.__eq__(other)



class Crop(object):	class Crop(object):


    def __init__(self, box, image):	    def __init__(self, box, image):
        if isinstance(image, six.string_types):
            self._fh = default_storage.open(image, mode='rb')
            image = PIL.Image.open(self._fh)

        self.box = box	        self.box = box
        self.image = image	        self.image = image
        self.bounds = Box(0, 0, *image.size)	        self.bounds = Box(0, 0, *image.size)


    def create_image(self, width=None, height=None, max_w=None, max_h=None):	    def close(self):
        import PIL.Image	        if hasattr(self, '_fh') and not self._fh.closed:
        from cropduster.exceptions import CropDusterResizeException	            self._fh.close()


        image = self.image.copy()	    def __del__(self):
        image.load()	        self.close()
        new_image = image.crop(self.box.as_tuple())	
        new_image.load()	    def create_image(self, output_filename, width, height):
        new_w, new_h = new_image.size	        from cropduster.utils import process_image, get_image_extension
        if new_w < width or new_h < height:	
            raise CropDusterResizeException(	        temp_file = tempfile.NamedTemporaryFile(suffix=get_image_extension(self.image), delete=False)
                u"Crop box (%dx%d) is too small for resize to (%dx%d)" % (new_w, new_h, width, height))	        temp_filename = temp_file.name

        with default_storage.open(self.image.filename, mode='rb') as f:
        # Scale our initial width and height based on the max_w and max_h	            temp_file.write(f.read())
        max_scales = []	        temp_file.seek(0)
        if max_w and max_w < width:	        image = PIL.Image.open(temp_filename)
            max_scales.append(max_w / width)	        image.filename = self.image.filename
        if max_h and max_h < height:	
            max_scales.append(max_h / height)	        crop_args = self.box.as_tuple()
        if max_scales:	
            max_scale = min(max_scales)	        def crop_and_resize_callback(im):
            width = int(round(width * max_scale))	            from cropduster.utils import smart_resize
            height = int(round(height * max_scale))	            im = im.crop(crop_args)
        if new_w > width or new_h > height:	            return smart_resize(im, final_w=width, final_h=height)
            new_image = new_image.resize((width, height), PIL.Image.ANTIALIAS)	
        new_image = process_image(image, output_filename, crop_and_resize_callback)
        new_image.crop = self	        new_image.crop = self
        temp_file.close()
        os.unlink(temp_filename)
        return new_image	        return new_image


    def best_fit(self, w=None, h=None, min_w=None, min_h=None, max_w=None, max_h=None):	    def best_fit(self, w=None, h=None, min_w=None, min_h=None, max_w=None, max_h=None, min_aspect=None, max_aspect=None):
        if w and h:	        if w and h:
            aspect_ratio = w / h	            aspect_ratio = w / h
        else:	        else:
            aspect_ratio = self.box.aspect_ratio	            aspect_ratio = self.box.aspect_ratio


        if min_aspect and aspect_ratio < min_aspect:
            aspect_ratio = min_aspect
        elif max_aspect and aspect_ratio > max_aspect:
            aspect_ratio = max_aspect

        scale = math.sqrt(aspect_ratio / self.box.aspect_ratio)	        scale = math.sqrt(aspect_ratio / self.box.aspect_ratio)


        w = self.box.w * scale	        w = self.box.w * scale
@@ -240,12 +323,20 @@ def best_fit(self, w=None, h=None, min_w=None, min_h=None, max_w=None, max_h=Non
            scale_y = (y2 - y1) / initial_fit.h	            scale_y = (y2 - y1) / initial_fit.h


        if scale_y < scale_x:	        if scale_y < scale_x:
            # scale down the width to maintain aspect ratio
            w = (x2 - x1) * (scale_y / scale_x)	            w = (x2 - x1) * (scale_y / scale_x)
            # unless the scaled width would drop below the min_w
            if w < min_w:
                w = min_w
            dw = initial_fit.w - w	            dw = initial_fit.w - w
            x1 += (dw / 2)	            x1 += (dw / 2)
            x2 = x1 + w	            x2 = x1 + w
        elif scale_x < scale_y:	        elif scale_x <= scale_y:
            # scale down the height to maintain aspect ratio
            h = (y2 - y1) * (scale_x / scale_y)	            h = (y2 - y1) * (scale_x / scale_y)
            # unless the scaled height would drop below the min_h
            if h < min_h:
                h = min_h
            dh = initial_fit.h - h	            dh = initial_fit.h - h
            y1 += (dh / 2)	            y1 += (dh / 2)
            y2 = y1 + h	            y2 = y1 + h
@@ -258,50 +349,40 @@ def best_fit(self, w=None, h=None, min_w=None, min_h=None, max_w=None, max_h=Non
        x2 = min(int(round(x2)), self.bounds.x2, x1 + w)	        x2 = min(int(round(x2)), self.bounds.x2, x1 + w)
        y2 = min(int(round(y2)), self.bounds.y2, y1 + h)	        y2 = min(int(round(y2)), self.bounds.y2, y1 + h)


        # Fix off-by-one rounding errors
        if (x2 - x1 == w - 1):
            if x2 < self.bounds.x2:
                x2 += 1
            elif x1 > self.bounds.x1:
                x1 -= 1
        if (y2 - y1 == h - 1):
            if y2 < self.bounds.y2:
                y2 += 1
            elif y1 > self.bounds.y1:
                y1 -= 1

        return Crop(Box(x1, y1, x2, y2), self.image)	        return Crop(Box(x1, y1, x2, y2), self.image)


    def add_xmp_to_crop(self, cropped_image, size):	    def add_xmp_to_crop(self, cropped_image_path, size, original_image=None):
        from cropduster.standalone.metadata import libxmp, file_format_supported	        try:
            from cropduster.standalone.metadata import (libxmp,
                get_xmp_from_storage, put_xmp_to_storage)
        except ImproperlyConfigured:
            libxmp = None


        if not libxmp:	        if not libxmp or not cropped_image_path:
            return	            return


        from PIL.ImageFile import ImageFile	        if original_image and CROPDUSTER_RETAIN_METADATA:
        from django.db.models.fields.files import FieldFile	            original_metadata = get_xmp_from_storage(original_image.filename)
        from cropduster.models import Thumb	        else:

            original_metadata = None
        if isinstance(cropped_image, ImageFile):	
            image_path = cropped_image.filename	
        elif isinstance(cropped_image, file):	
            image_path = cropped_image.name	
        elif isinstance(cropped_image, FieldFile):	
            image_path = cropped_image.path	
        elif isinstance(cropped_image, Thumb):	
            try:	
                image = cropped_image.image_set.all()[0]	
            except IndexError:	
                return False	
            else:	
                image_path = image.get_image_path(cropped_image.name)	
        elif isinstance(cropped_image, basestring):	
            image_path = cropped_image	

        xmp_file = libxmp.XMPFiles(file_path=image_path, open_forupdate=True)	

        xmp_meta = self.generate_xmp(size)	


        if not xmp_file.can_put_xmp(xmp_meta):	        xmp_meta = self.generate_xmp(size, original_metadata=original_metadata)
            if not file_format_supported(image_path):	
                raise Exception("Image format of %s does not allow metadata" %(	
                        os.path.basename(image_path)))	
            else:	
                raise Exception("Could not add metadata to image %s" % (	
                        os.path.basename(image_path)))	


        xmp_file.put_xmp(xmp_meta)	        put_xmp_to_storage(xmp_meta, cropped_image_path)
        xmp_file.close_file()	


    def generate_xmp(self, size):	    def generate_xmp(self, size, original_metadata=None):
        from cropduster.standalone.metadata import libxmp	        from cropduster.standalone.metadata import libxmp
        from cropduster.utils import json	        from cropduster.utils import json


@@ -310,11 +391,11 @@ def generate_xmp(self, size):
        NS_CROP = "http://ns.thealtantic.com/cropduster/1.0/"	        NS_CROP = "http://ns.thealtantic.com/cropduster/1.0/"


        md5 = hashlib.md5()	        md5 = hashlib.md5()
        with open(self.image.filename) as f:	        with default_storage.open(self.image.filename, mode='rb') as f:
            md5.update(f.read())	            md5.update(f.read())
        digest = md5.hexdigest()	        digest = md5.hexdigest()


        md = libxmp.XMPMeta()	        md = original_metadata or libxmp.XMPMeta()
        md.register_namespace(NS_XMPMM, 'xmpMM')	        md.register_namespace(NS_XMPMM, 'xmpMM')
        md.register_namespace(NS_MWG_RS, 'mwg-rs')	        md.register_namespace(NS_MWG_RS, 'mwg-rs')
        md.register_namespace('http://ns.adobe.com/xap/1.0/sType/Dimensions#', 'stDim')	        md.register_namespace('http://ns.adobe.com/xap/1.0/sType/Dimensions#', 'stDim')
@@ -323,16 +404,20 @@ def generate_xmp(self, size):
        md.set_property(NS_CROP, 'crop:size/stDim:w', '%s' % (size.width or ''))	        md.set_property(NS_CROP, 'crop:size/stDim:w', '%s' % (size.width or ''))
        md.set_property(NS_CROP, 'crop:size/stDim:h', '%s' % (size.height or ''))	        md.set_property(NS_CROP, 'crop:size/stDim:h', '%s' % (size.height or ''))
        md.set_property(NS_CROP, 'crop:size/crop:json', json.dumps(size))	        md.set_property(NS_CROP, 'crop:size/crop:json', json.dumps(size))
        md.set_property(NS_XMPMM, 'xmpMM:DerivedFrom', u'xmp.did:%s' % digest.upper())	        md.set_property(NS_CROP, 'crop:md5', digest.upper())
        md.set_property(NS_MWG_RS, 'mwg-rs:Regions/mwg-rs:AppliedToDimensions', '', prop_value_is_struct=True)	        md.set_property(NS_MWG_RS, 'mwg-rs:Regions/mwg-rs:AppliedToDimensions', '', prop_value_is_struct=True)
        md.set_property(NS_MWG_RS, 'mwg-rs:Regions/mwg-rs:AppliedToDimensions/stDim:w', unicode(self.image.size[0]))	        md.set_property(NS_MWG_RS, 'mwg-rs:Regions/mwg-rs:AppliedToDimensions/stDim:w', six.text_type(self.image.size[0]))
        md.set_property(NS_MWG_RS, 'mwg-rs:Regions/mwg-rs:AppliedToDimensions/stDim:h', unicode(self.image.size[1]))	        md.set_property(NS_MWG_RS, 'mwg-rs:Regions/mwg-rs:AppliedToDimensions/stDim:h', six.text_type(self.image.size[1]))
        # Clear out any existing <mwg-rs:RegionList> tags so they don't conflict
        # (for instance, iPhone face regions are stored in this tag)
        if md.does_property_exist(NS_MWG_RS, 'mwg-rs:Regions/mwg-rs:RegionList'):
            md.delete_property(NS_MWG_RS, 'mwg-rs:Regions/mwg-rs:RegionList')
        md.set_property(NS_MWG_RS, 'mwg-rs:Regions/mwg-rs:RegionList', '', prop_value_is_array=True)	        md.set_property(NS_MWG_RS, 'mwg-rs:Regions/mwg-rs:RegionList', '', prop_value_is_array=True)
        md.set_property(NS_MWG_RS, 'mwg-rs:Regions/mwg-rs:RegionList[1]/mwg-rs:Name', 'Crop')	        md.set_property(NS_MWG_RS, 'mwg-rs:Regions/mwg-rs:RegionList[1]/mwg-rs:Name', 'Crop')
        md.set_property(NS_MWG_RS, 'mwg-rs:Regions/mwg-rs:RegionList[1]/mwg-rs:Area', '', prop_value_is_struct=True)	        md.set_property(NS_MWG_RS, 'mwg-rs:Regions/mwg-rs:RegionList[1]/mwg-rs:Area', '', prop_value_is_struct=True)
        md.set_property(NS_MWG_RS, 'mwg-rs:Regions/mwg-rs:RegionList[1]/mwg-rs:Area/stArea:unit', "normalized")	        md.set_property(NS_MWG_RS, 'mwg-rs:Regions/mwg-rs:RegionList[1]/mwg-rs:Area/stArea:unit', "normalized")
        md.set_property(NS_MWG_RS, 'mwg-rs:Regions/mwg-rs:RegionList[1]/mwg-rs:Area/stArea:w',    "%.5f" % (self.box.w  / self.bounds.w))	        md.set_property(NS_MWG_RS, 'mwg-rs:Regions/mwg-rs:RegionList[1]/mwg-rs:Area/stArea:w', "%.5f" % (self.box.w / self.bounds.w))
        md.set_property(NS_MWG_RS, 'mwg-rs:Regions/mwg-rs:RegionList[1]/mwg-rs:Area/stArea:h',    "%.5f" % (self.box.h  / self.bounds.h))	        md.set_property(NS_MWG_RS, 'mwg-rs:Regions/mwg-rs:RegionList[1]/mwg-rs:Area/stArea:h', "%.5f" % (self.box.h / self.bounds.h))
        md.set_property(NS_MWG_RS, 'mwg-rs:Regions/mwg-rs:RegionList[1]/mwg-rs:Area/stArea:x',    "%.5f" % (self.box.x1 / self.bounds.w))	        md.set_property(NS_MWG_RS, 'mwg-rs:Regions/mwg-rs:RegionList[1]/mwg-rs:Area/stArea:x', "%.5f" % (self.box.x1 / self.bounds.w))
        md.set_property(NS_MWG_RS, 'mwg-rs:Regions/mwg-rs:RegionList[1]/mwg-rs:Area/stArea:y',    "%.5f" % (self.box.y1 / self.bounds.h))	        md.set_property(NS_MWG_RS, 'mwg-rs:Regions/mwg-rs:RegionList[1]/mwg-rs:Area/stArea:y', "%.5f" % (self.box.y1 / self.bounds.h))
        return md	        return md
  41  
cropduster/settings.py
@@ -1,4 +1,10 @@
import math
import PIL
import distutils.spawn
from distutils.version import LooseVersion
from django.conf import settings	from django.conf import settings
from django.core.exceptions import ImproperlyConfigured
from django.utils import six




CROPDUSTER_MEDIA_ROOT = getattr(settings, 'CROPDUSTER_MEDIA_ROOT', settings.MEDIA_ROOT)	CROPDUSTER_MEDIA_ROOT = getattr(settings, 'CROPDUSTER_MEDIA_ROOT', settings.MEDIA_ROOT)
@@ -15,3 +21,38 @@


CROPDUSTER_PREVIEW_WIDTH = getattr(settings, 'CROPDUSTER_PREVIEW_WIDTH', 800)	CROPDUSTER_PREVIEW_WIDTH = getattr(settings, 'CROPDUSTER_PREVIEW_WIDTH', 800)
CROPDUSTER_PREVIEW_HEIGHT = getattr(settings, 'CROPDUSTER_PREVIEW_HEIGHT', 500)	CROPDUSTER_PREVIEW_HEIGHT = getattr(settings, 'CROPDUSTER_PREVIEW_HEIGHT', 500)


def default_jpeg_quality(width, height):
    p = math.sqrt(width * height)
    if p >= 1750:
        return 80
    elif p >= 1000:
        return 85
    else:
        return 90

CROPDUSTER_JPEG_QUALITY = getattr(settings, 'CROPDUSTER_JPEG_QUALITY', default_jpeg_quality)


def get_jpeg_quality(width, height):
    if six.callable(CROPDUSTER_JPEG_QUALITY):
        return CROPDUSTER_JPEG_QUALITY(width, height)
    elif isinstance(CROPDUSTER_JPEG_QUALITY, (int, float)):
        return CROPDUSTER_JPEG_QUALITY
    else:
        raise ImproperlyConfigured(
            "CROPDUSTER_JPEG_QUALITY setting must be either a callable "
            "or a numeric value, got type %s" % (type(CROPDUSTER_JPEG_QUALITY).__name__))

JPEG_SAVE_ICC_SUPPORTED = (LooseVersion(getattr(PIL, '__version__', '0'))
    >= LooseVersion('2.2.1'))

CROPDUSTER_GIFSICLE_PATH = getattr(settings, 'CROPDUSTER_GIFSICLE_PATH', None)

if CROPDUSTER_GIFSICLE_PATH is None:
    # Try to find executable in the PATH
    CROPDUSTER_GIFSICLE_PATH = distutils.spawn.find_executable("gifsicle")

CROPDUSTER_RETAIN_METADATA = getattr(settings, 'CROPDUSTER_RETAIN_METADATA', False)
CROPDUSTER_CREATE_THUMBS = getattr(settings, 'CROPDUSTER_CREATE_THUMBS', True)
 103  
cropduster/south_migrations/0001_initial.py
@@ -0,0 +1,103 @@
# encoding: utf-8
import datetime
from south.db import db
from south.v2 import SchemaMigration
from django.db import models

class Migration(SchemaMigration):

    def forwards(self, orm):

        # Adding model 'Thumb'
        db.create_table('cropduster4_thumb', (
            ('name', self.gf('django.db.models.fields.CharField')(max_length=255, db_index=True)),
            ('date_modified', self.gf('django.db.models.fields.DateTimeField')(auto_now=True, blank=True)),
            ('crop_h', self.gf('django.db.models.fields.PositiveIntegerField')(null=True, blank=True)),
            ('height', self.gf('django.db.models.fields.PositiveIntegerField')(default=0, null=True, blank=True)),
            ('width', self.gf('django.db.models.fields.PositiveIntegerField')(default=0, null=True, blank=True)),
            ('crop_w', self.gf('django.db.models.fields.PositiveIntegerField')(null=True, blank=True)),
            ('id', self.gf('django.db.models.fields.AutoField')(primary_key=True)),
            ('reference_thumb', self.gf('django.db.models.fields.related.ForeignKey')(to=orm['cropduster.Thumb'], null=True, blank=True)),
            ('crop_y', self.gf('django.db.models.fields.PositiveIntegerField')(null=True, blank=True)),
            ('crop_x', self.gf('django.db.models.fields.PositiveIntegerField')(null=True, blank=True)),
        ))
        db.send_create_signal('cropduster', ['Thumb'])

        # Adding model 'Image'
        db.create_table('cropduster4_image', (
            ('attribution', self.gf('django.db.models.fields.CharField')(max_length=255, null=True, blank=True)),
            ('date_modified', self.gf('django.db.models.fields.DateTimeField')(auto_now=True, blank=True)),
            ('image', self.gf('django.db.models.fields.files.ImageField')(max_length=100, db_column='path', db_index=True)),
            ('object_id', self.gf('django.db.models.fields.PositiveIntegerField')()),
            ('height', self.gf('django.db.models.fields.PositiveIntegerField')(null=True, blank=True)),
            ('width', self.gf('django.db.models.fields.PositiveIntegerField')(null=True, blank=True)),
            ('content_type', self.gf('django.db.models.fields.related.ForeignKey')(to=orm['contenttypes.ContentType'])),
            ('date_created', self.gf('django.db.models.fields.DateTimeField')(auto_now_add=True, blank=True)),
            ('id', self.gf('django.db.models.fields.AutoField')(primary_key=True)),
        ))
        db.send_create_signal('cropduster', ['Image'])

        # Adding unique constraint on 'Image', fields ['content_type', 'object_id']
        db.create_unique('cropduster4_image', ['content_type_id', 'object_id'])

        # Adding M2M table for field thumbs on 'Image'
        db.create_table('cropduster4_image_thumbs', (
            ('id', models.AutoField(verbose_name='ID', primary_key=True, auto_created=True)),
            ('image', models.ForeignKey(orm['cropduster.image'], null=False)),
            ('thumb', models.ForeignKey(orm['cropduster.thumb'], null=False))
        ))
        db.create_unique('cropduster4_image_thumbs', ['image_id', 'thumb_id'])


    def backwards(self, orm):

        # Deleting model 'Thumb'
        db.delete_table('cropduster4_thumb')

        # Deleting model 'Image'
        db.delete_table('cropduster4_image')

        # Removing unique constraint on 'Image', fields ['content_type', 'object_id']
        db.delete_unique('cropduster4_image', ['content_type_id', 'object_id'])

        # Removing M2M table for field thumbs on 'Image'
        db.delete_table('cropduster4_image_thumbs')


    models = {
        'contenttypes.contenttype': {
            'Meta': {'unique_together': "(('app_label', 'model'),)", 'object_name': 'ContentType', 'db_table': "'django_content_type'"},
            'app_label': ('django.db.models.fields.CharField', [], {'max_length': '100'}),
            'id': ('django.db.models.fields.AutoField', [], {'primary_key': 'True'}),
            'model': ('django.db.models.fields.CharField', [], {'max_length': '100'}),
            'name': ('django.db.models.fields.CharField', [], {'max_length': '100'})
        },
        'cropduster.image': {
            'Meta': {'unique_together': "(('content_type', 'object_id'),)", 'object_name': 'Image', 'db_table': "'cropduster4_image'"},
            'attribution': ('django.db.models.fields.CharField', [], {'max_length': '255', 'null': 'True', 'blank': 'True'}),
            'content_type': ('django.db.models.fields.related.ForeignKey', [], {'to': "orm['contenttypes.ContentType']"}),
            'date_created': ('django.db.models.fields.DateTimeField', [], {'auto_now_add': 'True', 'blank': 'True'}),
            'date_modified': ('django.db.models.fields.DateTimeField', [], {'auto_now': 'True', 'blank': 'True'}),
            'height': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'id': ('django.db.models.fields.AutoField', [], {'primary_key': 'True'}),
            'image': ('django.db.models.fields.files.ImageField', [], {'max_length': '100', 'db_column': "'path'", 'db_index': 'True'}),
            'object_id': ('django.db.models.fields.PositiveIntegerField', [], {}),
            'thumbs': ('django.db.models.fields.related.ManyToManyField', [], {'blank': 'True', 'related_name': "'thumbs'", 'null': 'True', 'symmetrical': 'False', 'to': "orm['cropduster.Thumb']"}),
            'width': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'})
        },
        'cropduster.thumb': {
            'Meta': {'object_name': 'Thumb', 'db_table': "'cropduster4_thumb'"},
            'crop_h': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'crop_w': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'crop_x': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'crop_y': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'date_modified': ('django.db.models.fields.DateTimeField', [], {'auto_now': 'True', 'blank': 'True'}),
            'height': ('django.db.models.fields.PositiveIntegerField', [], {'default': '0', 'null': 'True', 'blank': 'True'}),
            'id': ('django.db.models.fields.AutoField', [], {'primary_key': 'True'}),
            'name': ('django.db.models.fields.CharField', [], {'max_length': '255', 'db_index': 'True'}),
            'reference_thumb': ('django.db.models.fields.related.ForeignKey', [], {'to': "orm['cropduster.Thumb']", 'null': 'True', 'blank': 'True'}),
            'width': ('django.db.models.fields.PositiveIntegerField', [], {'default': '0', 'null': 'True', 'blank': 'True'})
        }
    }

    complete_apps = ['cropduster']
 0  
...rations/0002_auto__add_standaloneimage.py ??? ...rations/0002_auto__add_standaloneimage.py
File renamed without changes.
  5  
...o__add_field_image_prev_content_object.py ??? ...o__add_field_image_prev_content_object.py
@@ -15,7 +15,10 @@ def forwards(self, orm):
        db.alter_column('cropduster4_image', 'object_id', self.gf('django.db.models.fields.PositiveIntegerField')(null=True, blank=True))	        db.alter_column('cropduster4_image', 'object_id', self.gf('django.db.models.fields.PositiveIntegerField')(null=True, blank=True))


        # Removing unique constraint on 'Image', fields ['object_id', 'content_type']	        # Removing unique constraint on 'Image', fields ['object_id', 'content_type']
        db.delete_unique('cropduster4_image', ['object_id', 'content_type_id'])	        try:
            db.delete_unique('cropduster4_image', ['object_id', 'content_type_id'])
        except:
            pass


        # Adding unique constraint on 'Image', fields ['object_id', 'content_type', 'prev_object_id']	        # Adding unique constraint on 'Image', fields ['object_id', 'content_type', 'prev_object_id']
        db.create_unique('cropduster4_image', ['object_id', 'content_type_id', 'prev_object_id'])	        db.create_unique('cropduster4_image', ['object_id', 'content_type_id', 'prev_object_id'])
  3  
...igrations/0004_add_auto_thumb_m2m_rows.py ??? ...igrations/0004_add_auto_thumb_m2m_rows.py
@@ -7,6 +7,9 @@
class Migration(DataMigration):	class Migration(DataMigration):


    def forwards(self, orm):	    def forwards(self, orm):
        if db.dry_run:
            return

        Thumb = orm['cropduster.Thumb']	        Thumb = orm['cropduster.Thumb']
        Image = orm['cropduster.Image']	        Image = orm['cropduster.Image']
        M2M = Image.thumbs.through	        M2M = Image.thumbs.through
 72  
.../south_migrations/0005_auto__add_field_image_attribution_link__add_field_image_caption.py
@@ -0,0 +1,72 @@
# encoding: utf-8
import datetime
from south.db import db
from south.v2 import SchemaMigration
from django.db import models

class Migration(SchemaMigration):

    def forwards(self, orm):

        # Adding field 'Image.attribution_link'
        db.add_column(u'cropduster4_image', 'attribution_link', self.gf('django.db.models.fields.URLField')(max_length=255, null=True, blank=True), keep_default=False)

        # Adding field 'Image.caption'
        db.add_column(u'cropduster4_image', 'caption', self.gf('django.db.models.fields.CharField')(max_length=255, null=True, blank=True), keep_default=False)


    def backwards(self, orm):

        # Deleting field 'Image.attribution_link'
        db.delete_column(u'cropduster4_image', 'attribution_link')

        # Deleting field 'Image.caption'
        db.delete_column(u'cropduster4_image', 'caption')


    models = {
        'contenttypes.contenttype': {
            'Meta': {'unique_together': "(('app_label', 'model'),)", 'object_name': 'ContentType', 'db_table': "'django_content_type'"},
            'app_label': ('django.db.models.fields.CharField', [], {'max_length': '100'}),
            'id': ('django.db.models.fields.AutoField', [], {'primary_key': 'True'}),
            'model': ('django.db.models.fields.CharField', [], {'max_length': '100'}),
            'name': ('django.db.models.fields.CharField', [], {'max_length': '100'})
        },
        'cropduster.image': {
            'Meta': {'unique_together': "(('content_type', 'object_id', 'prev_object_id'),)", 'object_name': 'Image', 'db_table': "u'cropduster4_image'"},
            'attribution': ('django.db.models.fields.CharField', [], {'max_length': '255', 'null': 'True', 'blank': 'True'}),
            'attribution_link': ('django.db.models.fields.URLField', [], {'max_length': '255', 'null': 'True', 'blank': 'True'}),
            'caption': ('django.db.models.fields.CharField', [], {'max_length': '255', 'null': 'True', 'blank': 'True'}),
            'content_type': ('django.db.models.fields.related.ForeignKey', [], {'to': "orm['contenttypes.ContentType']"}),
            'date_created': ('django.db.models.fields.DateTimeField', [], {'auto_now_add': 'True', 'blank': 'True'}),
            'date_modified': ('django.db.models.fields.DateTimeField', [], {'auto_now': 'True', 'blank': 'True'}),
            'height': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'id': ('django.db.models.fields.AutoField', [], {'primary_key': 'True'}),
            'image': ('django.db.models.fields.files.ImageField', [], {'max_length': '100', 'db_column': "'path'", 'db_index': 'True'}),
            'object_id': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'prev_object_id': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'thumbs': ('cropduster.fields.CropDusterThumbField', [], {'blank': 'True', 'related_name': "'image_set'", 'null': 'True', 'symmetrical': 'False', 'to': "orm['cropduster.Thumb']"}),
            'width': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'})
        },
        'cropduster.standaloneimage': {
            'Meta': {'object_name': 'StandaloneImage', 'db_table': "u'cropduster4_standaloneimage'"},
            'id': ('django.db.models.fields.AutoField', [], {'primary_key': 'True'}),
            'image': ('cropduster.fields.CropDusterField', [], {'to': "orm['cropduster.Image']", 'max_length': '100', 'sizes': "[{'max_w': None, 'retina': 0, 'min_h': 1, 'name': 'crop', 'w': None, 'h': None, 'min_w': 1, '__type__': 'Size', 'max_h': None, 'label': u'Crop'}]"}),
            'md5': ('django.db.models.fields.CharField', [], {'max_length': '32'})
        },
        'cropduster.thumb': {
            'Meta': {'object_name': 'Thumb', 'db_table': "u'cropduster4_thumb'"},
            'crop_h': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'crop_w': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'crop_x': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'crop_y': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'date_modified': ('django.db.models.fields.DateTimeField', [], {'auto_now': 'True', 'blank': 'True'}),
            'height': ('django.db.models.fields.PositiveIntegerField', [], {'default': '0', 'null': 'True', 'blank': 'True'}),
            'id': ('django.db.models.fields.AutoField', [], {'primary_key': 'True'}),
            'name': ('django.db.models.fields.CharField', [], {'max_length': '255', 'db_index': 'True'}),
            'reference_thumb': ('django.db.models.fields.related.ForeignKey', [], {'blank': 'True', 'related_name': "'auto_set'", 'null': 'True', 'to': "orm['cropduster.Thumb']"}),
            'width': ('django.db.models.fields.PositiveIntegerField', [], {'default': '0', 'null': 'True', 'blank': 'True'})
        }
    }

    complete_apps = ['cropduster']
 88  
cropduster/south_migrations/0006_auto__add_field_thumb_image.py
@@ -0,0 +1,88 @@
# encoding: utf-8
import datetime
from south.db import db
from south.v2 import SchemaMigration
from django.db import models


class Migration(SchemaMigration):

    def forwards(self, orm):
        # Adding field 'Thumb.image'
        db.add_column('cropduster4_thumb', 'image', self.gf('django.db.models.fields.related.ForeignKey')(blank=True, related_name='+', null=True, to=orm['cropduster.Image']), keep_default=False)
        if not db.dry_run:
            Thumb = orm['cropduster.thumb']
            thumbs = Thumb.objects.filter(image_id__isnull=True)
            if thumbs.count() > 5000:
                print ("\n"
                    " ! There are too many cropduster4_thumb rows to migrate in South.\n\n"
                    " ! You will need to manually migrate the many-to-many table.\n")
                return

            for thumb in thumbs:
                try:
                    image = thumb.image_set.all()[0]
                except IndexError:
                    pass
                else:
                    thumb.image_id = image.pk
                    thumb.save()


    def backwards(self, orm):
        # Deleting field 'Thumb.image'
        db.delete_column('cropduster4_thumb', 'image_id')

    models = {
        'contenttypes.contenttype': {
            'Meta': {'unique_together': "(('app_label', 'model'),)", 'object_name': 'ContentType', 'db_table': "'django_content_type'"},
            'app_label': ('django.db.models.fields.CharField', [], {'max_length': '100'}),
            'id': ('django.db.models.fields.AutoField', [], {'primary_key': 'True'}),
            'model': ('django.db.models.fields.CharField', [], {'max_length': '100'}),
            'name': ('django.db.models.fields.CharField', [], {'max_length': '100'})
        },
        'cropduster.image': {
            'Meta': {'unique_together': "(('content_type', 'object_id', 'prev_object_id'),)", 'object_name': 'Image', 'db_table': "'cropduster4_image'"},
            'attribution': ('django.db.models.fields.CharField', [], {'max_length': '255', 'null': 'True', 'blank': 'True'}),
            'attribution_link': ('django.db.models.fields.URLField', [], {'max_length': '255', 'null': 'True', 'blank': 'True'}),
            'caption': ('django.db.models.fields.CharField', [], {'max_length': '255', 'null': 'True', 'blank': 'True'}),
            'content_type': ('django.db.models.fields.related.ForeignKey', [], {'to': "orm['contenttypes.ContentType']"}),
            'date_created': ('django.db.models.fields.DateTimeField', [], {'auto_now_add': 'True', 'blank': 'True'}),
            'date_modified': ('django.db.models.fields.DateTimeField', [], {'auto_now': 'True', 'blank': 'True'}),
            'height': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'id': ('django.db.models.fields.AutoField', [], {'primary_key': 'True'}),
            'image': ('django.db.models.fields.files.ImageField', [], {'max_length': '100', 'db_column': "'path'", 'db_index': 'True'}),
            'object_id': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'prev_object_id': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'width': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            '_thumbs': ('cropduster.fields.CropDusterThumbField', [], {'blank': 'True', 'related_name': "'image_set'", 'null': 'True', 'symmetrical': 'False', 'to': "orm['cropduster.Thumb']", 'through': "orm['cropduster.ImageThumbs']"}),
        },
        'cropduster.imagethumbs': {
            'Meta': {'object_name': 'ImageThumbs', 'db_table': "'cropduster4_image_thumbs'"},
            'image': ('django.db.models.fields.related.ForeignKey', [], {'to': "orm['cropduster.Image']"}),
            'thumb': ('django.db.models.fields.related.ForeignKey', [], {'to': "orm['cropduster.Thumb']"}),
            'id': ('django.db.models.fields.AutoField', [], {'primary_key': 'True'}),
        },
        'cropduster.standaloneimage': {
            'Meta': {'object_name': 'StandaloneImage', 'db_table': "'cropduster4_standaloneimage'"},
            'id': ('django.db.models.fields.AutoField', [], {'primary_key': 'True'}),
            'image': ('cropduster.fields.CropDusterField', [], {'to': "orm['cropduster.Image']", 'max_length': '100', 'sizes': "[{'max_w': None, 'retina': 0, 'min_h': 1, 'name': 'crop', 'w': None, 'h': None, 'min_w': 1, '__type__': 'Size', 'max_h': None, 'label': u'Crop'}]"}),
            'md5': ('django.db.models.fields.CharField', [], {'max_length': '32'})
        },
        'cropduster.thumb': {
            'Meta': {'object_name': 'Thumb', 'db_table': "'cropduster4_thumb'"},
            'crop_h': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'crop_w': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'crop_x': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'crop_y': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'date_modified': ('django.db.models.fields.DateTimeField', [], {'auto_now': 'True', 'blank': 'True'}),
            'height': ('django.db.models.fields.PositiveIntegerField', [], {'default': '0', 'null': 'True', 'blank': 'True'}),
            'id': ('django.db.models.fields.AutoField', [], {'primary_key': 'True'}),
            'image': ('django.db.models.fields.related.ForeignKey', [], {'blank': 'True', 'related_name': "'+'", 'null': 'True', 'to': "orm['cropduster.Image']"}),
            'name': ('django.db.models.fields.CharField', [], {'max_length': '255', 'db_index': 'True'}),
            'reference_thumb': ('django.db.models.fields.related.ForeignKey', [], {'blank': 'True', 'related_name': "'auto_set'", 'null': 'True', 'to': "orm['cropduster.Thumb']"}),
            'width': ('django.db.models.fields.PositiveIntegerField', [], {'default': '0', 'null': 'True', 'blank': 'True'})
        }
    }

    complete_apps = ['cropduster']
 66  
cropduster/south_migrations/0007_auto__del_imagethumbs__chg_field_image_caption.py
@@ -0,0 +1,66 @@
# encoding: utf-8
import datetime
from south.db import db
from south.v2 import SchemaMigration
from django.db import models

class Migration(SchemaMigration):

    def forwards(self, orm):

        # Changing field 'Image.caption'
        db.alter_column('cropduster4_image', 'caption', self.gf('django.db.models.fields.TextField')(null=True, blank=True))


    def backwards(self, orm):

        # Changing field 'Image.caption'
        db.alter_column('cropduster4_image', 'caption', self.gf('django.db.models.fields.CharField')(max_length=255, null=True, blank=True))


    models = {
        'contenttypes.contenttype': {
            'Meta': {'unique_together': "(('app_label', 'model'),)", 'object_name': 'ContentType', 'db_table': "'django_content_type'"},
            'app_label': ('django.db.models.fields.CharField', [], {'max_length': '100'}),
            'id': ('django.db.models.fields.AutoField', [], {'primary_key': 'True'}),
            'model': ('django.db.models.fields.CharField', [], {'max_length': '100'}),
            'name': ('django.db.models.fields.CharField', [], {'max_length': '100'})
        },
        'cropduster.image': {
            'Meta': {'unique_together': "(('content_type', 'object_id', 'prev_object_id'),)", 'object_name': 'Image', 'db_table': "'cropduster4_image'"},
            'attribution': ('django.db.models.fields.CharField', [], {'max_length': '255', 'null': 'True', 'blank': 'True'}),
            'attribution_link': ('django.db.models.fields.URLField', [], {'max_length': '255', 'null': 'True', 'blank': 'True'}),
            'caption': ('django.db.models.fields.TextField', [], {'null': 'True', 'blank': 'True'}),
            'content_type': ('django.db.models.fields.related.ForeignKey', [], {'to': "orm['contenttypes.ContentType']"}),
            'date_created': ('django.db.models.fields.DateTimeField', [], {'auto_now_add': 'True', 'blank': 'True'}),
            'date_modified': ('django.db.models.fields.DateTimeField', [], {'auto_now': 'True', 'blank': 'True'}),
            'height': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'id': ('django.db.models.fields.AutoField', [], {'primary_key': 'True'}),
            'image': ('django.db.models.fields.files.ImageField', [], {'max_length': '100', 'db_column': "'path'", 'db_index': 'True'}),
            'object_id': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'prev_object_id': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'width': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'})
        },
        'cropduster.standaloneimage': {
            'Meta': {'object_name': 'StandaloneImage', 'db_table': "'cropduster4_standaloneimage'"},
            'id': ('django.db.models.fields.AutoField', [], {'primary_key': 'True'}),
            'image': ('cropduster.fields.CropDusterField', [], {'to': "orm['cropduster.Image']", 'max_length': '100', 'sizes': "[{'max_w': None, 'retina': 0, 'min_h': 1, 'name': 'crop', 'w': None, 'h': None, 'min_w': 1, '__type__': 'Size', 'max_h': None, 'label': u'Crop'}]"}),
            'md5': ('django.db.models.fields.CharField', [], {'max_length': '32'})
        },
        'cropduster.thumb': {
            'Meta': {'object_name': 'Thumb', 'db_table': "'cropduster4_thumb'"},
            'crop_h': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'crop_w': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'crop_x': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'crop_y': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'date_modified': ('django.db.models.fields.DateTimeField', [], {'auto_now': 'True', 'blank': 'True'}),
            'height': ('django.db.models.fields.PositiveIntegerField', [], {'default': '0', 'null': 'True', 'blank': 'True'}),
            'id': ('django.db.models.fields.AutoField', [], {'primary_key': 'True'}),
            'image': ('django.db.models.fields.related.ForeignKey', [], {'blank': 'True', 'related_name': "'+'", 'null': 'True', 'to': "orm['cropduster.Image']"}),
            'name': ('django.db.models.fields.CharField', [], {'max_length': '255', 'db_index': 'True'}),
            'reference_thumb': ('django.db.models.fields.related.ForeignKey', [], {'blank': 'True', 'related_name': "'auto_set'", 'null': 'True', 'to': "orm['cropduster.Thumb']"}),
            'width': ('django.db.models.fields.PositiveIntegerField', [], {'default': '0', 'null': 'True', 'blank': 'True'})
        }
    }

    complete_apps = ['cropduster']
 75  
cropduster/south_migrations/0008_auto__add_field_image_field_identifier.py
@@ -0,0 +1,75 @@
from south.db import db
from south.v2 import SchemaMigration


class Migration(SchemaMigration):

    def forwards(self, orm):

        # Adding field 'Image.field_identifier'
        db.add_column('cropduster4_image', 'field_identifier', self.gf('django.db.models.fields.SlugField')(db_index=True, max_length=50, null=True, blank=True), keep_default=False)

        # Removing unique constraint on 'Image', fields ['object_id', 'content_type', 'prev_object_id']
        db.delete_unique('cropduster4_image', ['object_id', 'content_type_id', 'prev_object_id'])

        # Adding unique constraint on 'Image', fields ['field_identifier', 'object_id', 'content_type', 'prev_object_id']
        db.create_unique('cropduster4_image', ['field_identifier', 'object_id', 'content_type_id', 'prev_object_id'])

    def backwards(self, orm):

        # Deleting field 'Image.field_identifier'
        db.delete_column('cropduster4_image', 'field_identifier')

        # Adding unique constraint on 'Image', fields ['object_id', 'content_type', 'prev_object_id']
        db.create_unique('cropduster4_image', ['object_id', 'content_type_id', 'prev_object_id'])

        # Removing unique constraint on 'Image', fields ['field_identifier', 'object_id', 'content_type', 'prev_object_id']
        db.delete_unique('cropduster4_image', ['field_identifier', 'object_id', 'content_type_id', 'prev_object_id'])

    models = {
        'contenttypes.contenttype': {
            'Meta': {'unique_together': "(('app_label', 'model'),)", 'object_name': 'ContentType', 'db_table': "'django_content_type'"},
            'app_label': ('django.db.models.fields.CharField', [], {'max_length': '100'}),
            'id': ('django.db.models.fields.AutoField', [], {'primary_key': 'True'}),
            'model': ('django.db.models.fields.CharField', [], {'max_length': '100'}),
            'name': ('django.db.models.fields.CharField', [], {'max_length': '100'})
        },
        'cropduster.image': {
            'Meta': {'unique_together': "(('content_type', 'object_id', 'prev_object_id', 'field_identifier'),)", 'object_name': 'Image', 'db_table': "'cropduster4_image'"},
            'attribution': ('django.db.models.fields.CharField', [], {'max_length': '255', 'null': 'True', 'blank': 'True'}),
            'attribution_link': ('django.db.models.fields.URLField', [], {'max_length': '255', 'null': 'True', 'blank': 'True'}),
            'caption': ('django.db.models.fields.TextField', [], {'null': 'True', 'blank': 'True'}),
            'content_type': ('django.db.models.fields.related.ForeignKey', [], {'to': "orm['contenttypes.ContentType']"}),
            'date_created': ('django.db.models.fields.DateTimeField', [], {'auto_now_add': 'True', 'blank': 'True'}),
            'date_modified': ('django.db.models.fields.DateTimeField', [], {'auto_now': 'True', 'blank': 'True'}),
            'field_identifier': ('django.db.models.fields.SlugField', [], {'db_index': 'True', 'max_length': '50', 'null': 'True', 'blank': 'True'}),
            'height': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'id': ('django.db.models.fields.AutoField', [], {'primary_key': 'True'}),
            'image': ('django.db.models.fields.files.ImageField', [], {'max_length': '100', 'db_column': "'path'", 'db_index': 'True'}),
            'object_id': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'prev_object_id': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'width': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'})
        },
        'cropduster.standaloneimage': {
            'Meta': {'object_name': 'StandaloneImage', 'db_table': "'cropduster4_standaloneimage'"},
            'id': ('django.db.models.fields.AutoField', [], {'primary_key': 'True'}),
            'image': ('cropduster.fields.CropDusterField', [], {'to': "orm['cropduster.Image']", 'max_length': '100', 'sizes': "[{'max_w': None, 'retina': 0, 'min_h': 1, 'name': 'crop', 'w': None, 'h': None, 'min_w': 1, '__type__': 'Size', 'max_h': None, 'label': u'Crop'}]"}),
            'md5': ('django.db.models.fields.CharField', [], {'max_length': '32'})
        },
        'cropduster.thumb': {
            'Meta': {'object_name': 'Thumb', 'db_table': "'cropduster4_thumb'"},
            'crop_h': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'crop_w': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'crop_x': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'crop_y': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'date_modified': ('django.db.models.fields.DateTimeField', [], {'auto_now': 'True', 'blank': 'True'}),
            'height': ('django.db.models.fields.PositiveIntegerField', [], {'default': '0', 'null': 'True', 'blank': 'True'}),
            'id': ('django.db.models.fields.AutoField', [], {'primary_key': 'True'}),
            'image': ('django.db.models.fields.related.ForeignKey', [], {'blank': 'True', 'related_name': "'+'", 'null': 'True', 'to': "orm['cropduster.Image']"}),
            'name': ('django.db.models.fields.CharField', [], {'max_length': '255', 'db_index': 'True'}),
            'reference_thumb': ('django.db.models.fields.related.ForeignKey', [], {'blank': 'True', 'related_name': "'auto_set'", 'null': 'True', 'to': "orm['cropduster.Thumb']"}),
            'width': ('django.db.models.fields.PositiveIntegerField', [], {'default': '0', 'null': 'True', 'blank': 'True'})
        }
    }

    complete_apps = ['cropduster']
 73  
...migrations/0009_auto__del_unique_image_field_identifier_object_id_content_type_prev_ob.py
@@ -0,0 +1,73 @@
# encoding: utf-8
import datetime
from south.db import db
from south.v2 import SchemaMigration
from django.db import models

class Migration(SchemaMigration):

    def forwards(self, orm):

        # Removing unique constraint on 'Image', fields ['field_identifier', 'object_id', 'content_type', 'prev_object_id']
        db.delete_unique('cropduster4_image', ['field_identifier', 'object_id', 'content_type_id', 'prev_object_id'])

        # Adding unique constraint on 'Image', fields ['field_identifier', 'object_id', 'content_type']
        db.create_unique('cropduster4_image', ['field_identifier', 'object_id', 'content_type_id'])


    def backwards(self, orm):

        # Adding unique constraint on 'Image', fields ['field_identifier', 'object_id', 'content_type', 'prev_object_id']
        db.create_unique('cropduster4_image', ['field_identifier', 'object_id', 'content_type_id', 'prev_object_id'])

        # Removing unique constraint on 'Image', fields ['field_identifier', 'object_id', 'content_type']
        db.delete_unique('cropduster4_image', ['field_identifier', 'object_id', 'content_type_id'])


    models = {
        'contenttypes.contenttype': {
            'Meta': {'unique_together': "(('app_label', 'model'),)", 'object_name': 'ContentType', 'db_table': "'django_content_type'"},
            'app_label': ('django.db.models.fields.CharField', [], {'max_length': '100'}),
            'id': ('django.db.models.fields.AutoField', [], {'primary_key': 'True'}),
            'model': ('django.db.models.fields.CharField', [], {'max_length': '100'}),
            'name': ('django.db.models.fields.CharField', [], {'max_length': '100'})
        },
        'cropduster.image': {
            'Meta': {'unique_together': "(('content_type', 'object_id', 'field_identifier'),)", 'object_name': 'Image', 'db_table': "'cropduster4_image'"},
            'attribution': ('django.db.models.fields.CharField', [], {'max_length': '255', 'null': 'True', 'blank': 'True'}),
            'attribution_link': ('django.db.models.fields.URLField', [], {'max_length': '255', 'null': 'True', 'blank': 'True'}),
            'caption': ('django.db.models.fields.TextField', [], {'null': 'True', 'blank': 'True'}),
            'content_type': ('django.db.models.fields.related.ForeignKey', [], {'to': "orm['contenttypes.ContentType']"}),
            'date_created': ('django.db.models.fields.DateTimeField', [], {'auto_now_add': 'True', 'blank': 'True'}),
            'date_modified': ('django.db.models.fields.DateTimeField', [], {'auto_now': 'True', 'blank': 'True'}),
            'field_identifier': ('django.db.models.fields.SlugField', [], {'db_index': 'True', 'max_length': '50', 'null': 'True', 'blank': 'True'}),
            'height': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'id': ('django.db.models.fields.AutoField', [], {'primary_key': 'True'}),
            'image': ('django.db.models.fields.files.ImageField', [], {'max_length': '100', 'db_column': "'path'", 'db_index': 'True'}),
            'object_id': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'prev_object_id': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'width': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'})
        },
        'cropduster.standaloneimage': {
            'Meta': {'object_name': 'StandaloneImage', 'db_table': "'cropduster4_standaloneimage'"},
            'id': ('django.db.models.fields.AutoField', [], {'primary_key': 'True'}),
            'image': ('cropduster.fields.CropDusterField', [], {'to': "orm['cropduster.Image']", 'max_length': '100', 'sizes': "[{'max_w': None, 'retina': 0, 'min_h': 1, 'name': 'crop', 'w': None, 'h': None, 'min_w': 1, '__type__': 'Size', 'max_h': None, 'label': u'Crop'}]"}),
            'md5': ('django.db.models.fields.CharField', [], {'max_length': '32'})
        },
        'cropduster.thumb': {
            'Meta': {'object_name': 'Thumb', 'db_table': "'cropduster4_thumb'"},
            'crop_h': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'crop_w': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'crop_x': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'crop_y': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'date_modified': ('django.db.models.fields.DateTimeField', [], {'auto_now': 'True', 'blank': 'True'}),
            'height': ('django.db.models.fields.PositiveIntegerField', [], {'default': '0', 'null': 'True', 'blank': 'True'}),
            'id': ('django.db.models.fields.AutoField', [], {'primary_key': 'True'}),
            'image': ('django.db.models.fields.related.ForeignKey', [], {'blank': 'True', 'related_name': "'+'", 'null': 'True', 'to': "orm['cropduster.Image']"}),
            'name': ('django.db.models.fields.CharField', [], {'max_length': '255', 'db_index': 'True'}),
            'reference_thumb': ('django.db.models.fields.related.ForeignKey', [], {'blank': 'True', 'related_name': "'auto_set'", 'null': 'True', 'to': "orm['cropduster.Thumb']"}),
            'width': ('django.db.models.fields.PositiveIntegerField', [], {'default': '0', 'null': 'True', 'blank': 'True'})
        }
    }

    complete_apps = ['cropduster']
 67  
cropduster/south_migrations/0010_auto__chg_field_image_field_identifier.py
@@ -0,0 +1,67 @@
# encoding: utf-8
import datetime
from south.db import db
from south.v2 import SchemaMigration
from django.db import models

class Migration(SchemaMigration):

    def forwards(self, orm):

        # Changing field 'Image.field_identifier'
        db.alter_column('cropduster4_image', 'field_identifier', self.gf('django.db.models.fields.SlugField')(max_length=50, blank=True))


    def backwards(self, orm):

        # Changing field 'Image.field_identifier'
        db.alter_column('cropduster4_image', 'field_identifier', self.gf('django.db.models.fields.SlugField')(blank=True, max_length=50, null=True))


    models = {
        'contenttypes.contenttype': {
            'Meta': {'unique_together': "(('app_label', 'model'),)", 'object_name': 'ContentType', 'db_table': "'django_content_type'"},
            'app_label': ('django.db.models.fields.CharField', [], {'max_length': '100'}),
            'id': ('django.db.models.fields.AutoField', [], {'primary_key': 'True'}),
            'model': ('django.db.models.fields.CharField', [], {'max_length': '100'}),
            'name': ('django.db.models.fields.CharField', [], {'max_length': '100'})
        },
        'cropduster.image': {
            'Meta': {'unique_together': "(('content_type', 'object_id', 'field_identifier'),)", 'object_name': 'Image', 'db_table': "'cropduster4_image'"},
            'attribution': ('django.db.models.fields.CharField', [], {'max_length': '255', 'null': 'True', 'blank': 'True'}),
            'attribution_link': ('django.db.models.fields.URLField', [], {'max_length': '255', 'null': 'True', 'blank': 'True'}),
            'caption': ('django.db.models.fields.TextField', [], {'null': 'True', 'blank': 'True'}),
            'content_type': ('django.db.models.fields.related.ForeignKey', [], {'to': "orm['contenttypes.ContentType']"}),
            'date_created': ('django.db.models.fields.DateTimeField', [], {'auto_now_add': 'True', 'blank': 'True'}),
            'date_modified': ('django.db.models.fields.DateTimeField', [], {'auto_now': 'True', 'blank': 'True'}),
            'field_identifier': ('django.db.models.fields.SlugField', [], {'default': "''", 'max_length': '50', 'db_index': 'True', 'blank': 'True'}),
            'height': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'id': ('django.db.models.fields.AutoField', [], {'primary_key': 'True'}),
            'image': ('django.db.models.fields.files.ImageField', [], {'max_length': '100', 'db_column': "'path'", 'db_index': 'True'}),
            'object_id': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'prev_object_id': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'width': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'})
        },
        'cropduster.standaloneimage': {
            'Meta': {'object_name': 'StandaloneImage', 'db_table': "'cropduster4_standaloneimage'"},
            'id': ('django.db.models.fields.AutoField', [], {'primary_key': 'True'}),
            'image': ('cropduster.fields.CropDusterField', [], {'to': "orm['cropduster.Image']", 'max_length': '100', 'sizes': "[{'max_w': None, 'retina': 0, 'min_h': 1, 'name': 'crop', 'w': None, 'h': None, 'min_w': 1, '__type__': 'Size', 'max_h': None, 'label': u'Crop'}]"}),
            'md5': ('django.db.models.fields.CharField', [], {'max_length': '32'})
        },
        'cropduster.thumb': {
            'Meta': {'object_name': 'Thumb', 'db_table': "'cropduster4_thumb'"},
            'crop_h': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'crop_w': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'crop_x': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'crop_y': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'date_modified': ('django.db.models.fields.DateTimeField', [], {'auto_now': 'True', 'blank': 'True'}),
            'height': ('django.db.models.fields.PositiveIntegerField', [], {'default': '0', 'null': 'True', 'blank': 'True'}),
            'id': ('django.db.models.fields.AutoField', [], {'primary_key': 'True'}),
            'image': ('django.db.models.fields.related.ForeignKey', [], {'blank': 'True', 'related_name': "'+'", 'null': 'True', 'to': "orm['cropduster.Image']"}),
            'name': ('django.db.models.fields.CharField', [], {'max_length': '255', 'db_index': 'True'}),
            'reference_thumb': ('django.db.models.fields.related.ForeignKey', [], {'blank': 'True', 'related_name': "'auto_set'", 'null': 'True', 'to': "orm['cropduster.Thumb']"}),
            'width': ('django.db.models.fields.PositiveIntegerField', [], {'default': '0', 'null': 'True', 'blank': 'True'})
        }
    }

    complete_apps = ['cropduster']
 61  
cropduster/south_migrations/0011_update_model_freeze.py
@@ -0,0 +1,61 @@
# encoding: utf-8
import datetime
from south.db import db
from south.v2 import SchemaMigration
from django.db import models

class Migration(SchemaMigration):

    def forwards(self, orm):
        pass

    def backwards(self, orm):
        pass

    models = {
        'contenttypes.contenttype': {
            'Meta': {'unique_together': "(('app_label', 'model'),)", 'object_name': 'ContentType', 'db_table': "'django_content_type'"},
            'app_label': ('django.db.models.fields.CharField', [], {'max_length': '100'}),
            'id': ('django.db.models.fields.AutoField', [], {'primary_key': 'True'}),
            'model': ('django.db.models.fields.CharField', [], {'max_length': '100'}),
            'name': ('django.db.models.fields.CharField', [], {'max_length': '100'})
        },
        'cropduster.image': {
            'Meta': {'unique_together': "(('content_type', 'object_id', 'field_identifier'),)", 'object_name': 'Image', 'db_table': "'cropduster4_image'"},
            'attribution': ('django.db.models.fields.CharField', [], {'max_length': '255', 'null': 'True', 'blank': 'True'}),
            'attribution_link': ('django.db.models.fields.URLField', [], {'max_length': '255', 'null': 'True', 'blank': 'True'}),
            'caption': ('django.db.models.fields.TextField', [], {'null': 'True', 'blank': 'True'}),
            'content_type': ('django.db.models.fields.related.ForeignKey', [], {'to': "orm['contenttypes.ContentType']"}),
            'date_created': ('django.db.models.fields.DateTimeField', [], {'auto_now_add': 'True', 'blank': 'True'}),
            'date_modified': ('django.db.models.fields.DateTimeField', [], {'auto_now': 'True', 'blank': 'True'}),
            'field_identifier': ('django.db.models.fields.SlugField', [], {'default': "''", 'max_length': '50', 'db_index': 'True', 'blank': 'True'}),
            'height': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'id': ('django.db.models.fields.AutoField', [], {'primary_key': 'True'}),
            'image': ('cropduster.fields.CropDusterSimpleImageField', [], {'max_length': '100', 'db_column': "'path'", 'db_index': 'True'}),
            'object_id': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'prev_object_id': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'width': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'})
        },
        'cropduster.standaloneimage': {
            'Meta': {'object_name': 'StandaloneImage', 'db_table': "'cropduster4_standaloneimage'"},
            'id': ('django.db.models.fields.AutoField', [], {'primary_key': 'True'}),
            'image': ('cropduster.fields.CropDusterField', [], {'to': "orm['cropduster.Image']", 'max_length': '100', 'sizes': "[{'min_w': 1, 'retina': 0, 'name': 'crop', 'h': None, 'required': True, '__type__': 'Size', 'max_h': None, 'label': u'Crop', 'max_w': None, 'min_h': 1, 'w': None}]"}),
            'md5': ('django.db.models.fields.CharField', [], {'max_length': '32'})
        },
        'cropduster.thumb': {
            'Meta': {'object_name': 'Thumb', 'db_table': "'cropduster4_thumb'"},
            'crop_h': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'crop_w': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'crop_x': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'crop_y': ('django.db.models.fields.PositiveIntegerField', [], {'null': 'True', 'blank': 'True'}),
            'date_modified': ('django.db.models.fields.DateTimeField', [], {'auto_now': 'True', 'blank': 'True'}),
            'height': ('django.db.models.fields.PositiveIntegerField', [], {'default': '0', 'null': 'True', 'blank': 'True'}),
            'id': ('django.db.models.fields.AutoField', [], {'primary_key': 'True'}),
            'image': ('django.db.models.fields.related.ForeignKey', [], {'blank': 'True', 'related_name': "'+'", 'null': 'True', 'to': "orm['cropduster.Image']"}),
            'name': ('django.db.models.fields.CharField', [], {'max_length': '255', 'db_index': 'True'}),
            'reference_thumb': ('django.db.models.fields.related.ForeignKey', [], {'blank': 'True', 'related_name': "'auto_set'", 'null': 'True', 'to': "orm['cropduster.Thumb']"}),
            'width': ('django.db.models.fields.PositiveIntegerField', [], {'default': '0', 'null': 'True', 'blank': 'True'})
        }
    }

    complete_apps = ['cropduster']
 0  
cropduster3/templatetags/__init__.py ??? cropduster/south_migrations/__init__.py
File renamed without changes.
  104  
cropduster/standalone/metadata.py
@@ -2,13 +2,17 @@
import re	import re
import ctypes	import ctypes
import PIL.Image	import PIL.Image
import tempfile
from io import open


from django.core.exceptions import ImproperlyConfigured	from django.core.exceptions import ImproperlyConfigured
from django.core.files.storage import default_storage
from django.utils.encoding import force_bytes
from django.utils import six


from cropduster.files import ImageFile	from cropduster.files import ImageFile
from cropduster.utils import json	from cropduster.utils import json



try:	try:
    import libxmp	    import libxmp
except ImportError:	except ImportError:
@@ -28,9 +32,16 @@


if not libxmp:	if not libxmp:
    check_file_format = get_format_info = None	    check_file_format = get_format_info = None

    def file_to_dict(f):
        return {}
else:	else:
    check_file_format = libxmp._exempi.xmp_files_check_file_format	    try:
    get_format_info = libxmp._exempi.xmp_files_get_format_info	        exempi = libxmp._exempi
    except AttributeError:
        exempi = libxmp.exempi.EXEMPI
    check_file_format = exempi.xmp_files_check_file_format
    get_format_info = exempi.xmp_files_get_format_info


    if not check_file_format.argtypes:	    if not check_file_format.argtypes:
        check_file_format.argtypes = [ctypes.c_char_p]	        check_file_format.argtypes = [ctypes.c_char_p]
@@ -42,14 +53,19 @@
    if not get_format_info.restype:	    if not get_format_info.restype:
        get_format_info.restype = ctypes.c_bool	        get_format_info.restype = ctypes.c_bool


    try:
        from libxmp.utils import file_to_dict
    except ImportError:
        from libxmp import file_to_dict



class EnumerationMeta(type):	class EnumerationMeta(type):


    def __new__(cls, name, bases, attrs):	    def __new__(cls, name, bases, attrs):
        if '_lookup' not in attrs:	        if '_lookup' not in attrs:
            lookup = {}	            lookup = {}
            for k, v in attrs.iteritems():	            for k, v in six.iteritems(attrs):
                if isinstance(v, (int, long)):	                if isinstance(v, six.integer_types):
                    lookup.setdefault(v, k)	                    lookup.setdefault(v, k)
            attrs['_lookup'] = lookup	            attrs['_lookup'] = lookup


@@ -59,8 +75,8 @@ def __contains__(self, value):
        return value in self._lookup	        return value in self._lookup




@six.add_metaclass(EnumerationMeta)
class Enumeration(object):	class Enumeration(object):
    __metaclass__ = EnumerationMeta	
    @classmethod	    @classmethod
    def value_name(cls, value):	    def value_name(cls, value):
        return cls._lookup.get(value)	        return cls._lookup.get(value)
@@ -135,7 +151,7 @@ def file_format_supported(file_path):
        raise IOError("File %s could not be found" % file_path)	        raise IOError("File %s could not be found" % file_path)
    if not check_file_format:	    if not check_file_format:
        return False	        return False
    file_format = check_file_format(os.path.abspath(file_path))	    file_format = check_file_format(force_bytes(os.path.abspath(file_path)))
    format_options = ctypes.c_int()	    format_options = ctypes.c_int()
    if file_format != FileFormats.XMP_FT_UNKNOWN:	    if file_format != FileFormats.XMP_FT_UNKNOWN:
        format_options = get_format_info(	        format_options = get_format_info(
@@ -164,9 +180,22 @@ class MetadataDict(dict):
    """	    """


    def __init__(self, file_path):	    def __init__(self, file_path):
        self.file_path = file_path	        try:
        ns_dict = libxmp.file_to_dict(file_path)	            # Don't use temporary files if we're using FileSystemStorage
        for ns, values in ns_dict.iteritems():	            with open(default_storage.path(file_path), mode='rb') as f:
                self.file_path = f.name
        except:
            self.tmp_file = tempfile.NamedTemporaryFile()
            with default_storage.open(file_path) as f:
                self.tmp_file.write(f.read())
                self.tmp_file.flush()
                self.tmp_file.seek(0)
            self.file_path = self.tmp_file.name
        ns_dict = file_to_dict(self.file_path)
        self.clean(ns_dict)

    def clean(self, ns_dict):
        for ns, values in six.iteritems(ns_dict):
            for k, v, opts in values:	            for k, v, opts in values:
                current = self	                current = self
                bits = k.split('/')	                bits = k.split('/')
@@ -203,17 +232,19 @@ def __init__(self, file_path):
                        v = float(v)	                        v = float(v)
                    except (TypeError, ValueError):	                    except (TypeError, ValueError):
                        v = None	                        v = None
                elif k == 'DerivedFrom' and isinstance(v, basestring):	                elif k == 'DerivedFrom' and isinstance(v, six.string_types):
                    v = re.sub(r'^xmp\.did:', '', v).lower()	                    v = re.sub(r'^xmp\.did:', '', v).lower()
                elif ns_prefix == 'crop' and k == 'json':	                elif ns_prefix == 'crop' and k == 'json':
                    v = json.loads(v)	                    v = json.loads(v)
                elif ns_prefix == 'crop' and k == 'md5':
                    v = v.lower()


                m = re.search(r'^(.*)\[(\d+)\](?=\/|\Z)', k)	                m = re.search(r'^(.*)\[(\d+)\](?=\/|\Z)', k)
                if m:	                if m:
                    current = current.setdefault(m.group(1), [{}])	                    current = current.setdefault(m.group(1), [{}])
                    k = int(m.group(2)) - 1	                    k = int(m.group(2)) - 1


                if isinstance(current, list) and isinstance(k, int):	                if isinstance(current, list) and isinstance(k, six.integer_types):
                    if len(current) <= k:	                    if len(current) <= k:
                        current.append(*([{}] * (1 + k - len(current))))	                        current.append(*([{}] * (1 + k - len(current))))


@@ -284,4 +315,51 @@ class MetadataImageFile(ImageFile):
    def __init__(self, *args, **kwargs):	    def __init__(self, *args, **kwargs):
        super(MetadataImageFile, self).__init__(*args, **kwargs)	        super(MetadataImageFile, self).__init__(*args, **kwargs)
        if self:	        if self:
            self.metadata = MetadataDict(self.path)	            self.metadata = MetadataDict(self.name)


def get_xmp_from_file(file_path):
    return libxmp.XMPFiles(file_path=file_path).get_xmp()


def get_xmp_from_bytes(img_bytes):
    tmp = tempfile.NamedTemporaryFile(delete=False)
    tmp.write(img_bytes)
    tmp.close()
    try:
        return get_xmp_from_file(tmp.name)
    finally:
        os.unlink(tmp.name)


def get_xmp_from_storage(file_path, storage=default_storage):
    with storage.open(file_path, mode='rb') as f:
        return get_xmp_from_bytes(f.read())


def put_xmp_to_file(xmp_meta, file_path):
    xmp_file = libxmp.XMPFiles(file_path=file_path, open_forupdate=True)

    if not xmp_file.can_put_xmp(xmp_meta):
        if not file_format_supported(file_path):
            raise Exception("Image format of %s does not allow metadata" % (file_path))
        else:
            raise Exception("Could not add metadata to image %s" % (file_path))

    xmp_file.put_xmp(xmp_meta)
    xmp_file.close_file()


def put_xmp_to_storage(xmp_meta, file_path, storage=default_storage):
    tmp = tempfile.NamedTemporaryFile(delete=False)
    try:
        with default_storage.open(file_path, mode='rb') as f:
            tmp.write(f.read())
        tmp.close()
        put_xmp_to_file(xmp_meta, tmp.name)
        with open(tmp.name, mode='rb') as f:
            data = f.read()
        with storage.open(file_path, mode='wb') as f:
            f.write(data)
    finally:
        os.unlink(tmp.name)
  16  
cropduster/standalone/models.py
@@ -5,11 +5,12 @@
from django.core.files.uploadedfile import SimpleUploadedFile	from django.core.files.uploadedfile import SimpleUploadedFile
from django.db import models	from django.db import models


from generic_plus.utils import get_relative_media_url

from cropduster import settings as cropduster_settings	from cropduster import settings as cropduster_settings
from cropduster.fields import CropDusterField	from cropduster.fields import CropDusterField
from cropduster.files import VirtualFieldFile	from cropduster.files import VirtualFieldFile
from cropduster.resizing import Size	from cropduster.resizing import Size
from cropduster.utils import get_relative_media_url	




class StandaloneImageManager(models.Manager):	class StandaloneImageManager(models.Manager):
@@ -42,28 +43,29 @@ def get_from_file(self, file_path, upload_to=None, preview_w=None, preview_h=Non
        cropduster_image, created = Image.objects.get_or_create(	        cropduster_image, created = Image.objects.get_or_create(
            content_type=ContentType.objects.get_for_model(StandaloneImage),	            content_type=ContentType.objects.get_for_model(StandaloneImage),
            object_id=standalone.pk)	            object_id=standalone.pk)
        standalone.image.related_object = cropduster_image
        cropduster_image.image = file_path	        cropduster_image.image = file_path
        cropduster_image.save()	        cropduster_image.save()
        cropduster_image.save_preview(preview_w, preview_h)	        cropduster_image.save_preview(preview_w, preview_h)
        standalone.image.cropduster_image = cropduster_image	
        return standalone	        return standalone




class StandaloneImage(models.Model):	class StandaloneImage(models.Model):


    objects = StandaloneImageManager()	    objects = StandaloneImageManager()


    md5 = models.CharField(max_length=32)	    md5 = models.CharField(max_length=32, blank=True, default='')
    image = CropDusterField(sizes=[Size("crop")])	    image = CropDusterField(sizes=[Size("crop")], upload_to='')


    class Meta:	    class Meta:
        app_label = cropduster_settings.CROPDUSTER_APP_LABEL	        app_label = cropduster_settings.CROPDUSTER_APP_LABEL
        db_table = '%s_standaloneimage' % cropduster_settings.CROPDUSTER_DB_PREFIX	        db_table = '%s_standaloneimage' % cropduster_settings.CROPDUSTER_DB_PREFIX


    def save(self, **kwargs):	    def save(self, **kwargs):
        if not self.md5:	        if not self.md5 and self.image:
            md5_hash = hashlib.md5()	            md5_hash = hashlib.md5()
            with open(self.image.path) as f:	            with self.image.related_object.image as f:
                f.open()
                md5_hash.update(f.read())	                md5_hash.update(f.read())
            self.md5 = md5_hash.digest()	            self.md5 = md5_hash.hexdigest()
        super(StandaloneImage, self).save(**kwargs)	        super(StandaloneImage, self).save(**kwargs)
  135  
cropduster/standalone/static/ckeditor/ckeditor/plugins/cropduster/dialogs/cropduster.js
@@ -344,7 +344,10 @@ CKEDITOR.dialog.add('cropduster', function (editor) {


    var okButton = CKEDITOR.dialog.okButton.override({	    var okButton = CKEDITOR.dialog.okButton.override({
        onClick: function(evt) {	        onClick: function(evt) {
            var $j = cropdusterIframe.$.contentWindow.$;	            var contentWin = cropdusterIframe.iframeElement.$.contentWindow;
            var $j = (typeof contentWin.django === 'object')
              ? contentWin.django.jQuery
              : contentWin.$;
            if ($j) {	            if ($j) {
                var $cropButton = $j('#crop-button');	                var $cropButton = $j('#crop-button');
                if ($j.length && !$cropButton.hasClass('disabled')) {	                if ($j.length && !$cropButton.hasClass('disabled')) {
@@ -362,9 +365,10 @@ CKEDITOR.dialog.add('cropduster', function (editor) {
    var tabElements = [{	    var tabElements = [{
        id: 'iframe',	        id: 'iframe',
        type: 'html',	        type: 'html',
        html: '<div style="width:100%;text-align:center;">' + '<iframe style="border:0;width:650px;height:500px;font-size:20px" scrolling="no" frameborder="0" allowTransparency="true"></iframe>' + '</div>',	        html: '<div style="width:100%;text-align:center;">' + '<iframe style="border:0;width:650px;height:400px;font-size:20px" scrolling="no" frameborder="0" allowTransparency="true"></iframe>' + '</div>',
        onLoad: function (widget) {},	        onLoad: function (widget) {},
        setup: function (widget) {	        setup: function (widget) {

            var dialogElement = this.getDialog().getElement();	            var dialogElement = this.getDialog().getElement();
            dialogElement.addClass('cke_editor_cropduster_content_dialog');	            dialogElement.addClass('cke_editor_cropduster_content_dialog');
            var tabs = dialogElement.findOne('.cke_dialog_tabs');	            var tabs = dialogElement.findOne('.cke_dialog_tabs');
@@ -375,39 +379,55 @@ CKEDITOR.dialog.add('cropduster', function (editor) {
            if (contents) {	            if (contents) {
                contents.setStyles({'border-top': '0', 'margin-top': '0'});	                contents.setStyles({'border-top': '0', 'margin-top': '0'});
            }	            }
            var domId = this.domId.replace(/_uiElement$/, '');	
            var callback_fn = domId + '_callback';	            cropdusterIframe = {
            var image = widget.parts.image;	                setup: function (domId, baseUrl) {
            var url = widget.config.url + '?';	                    this.iframeElement = CKEDITOR.document.getById(domId).getChild(0)
            var params = {	                    this.iframeElement.$.src = 'about:blank';
                'callback_fn': callback_fn	                    try {
            };	                        this.iframeElement.$.contentDocument.body.innerHTML = "";
            if (widget.config.uploadTo) {	                    } catch(e) {}
                params['upload_to'] = widget.config.uploadTo;	                    this.baseUrl = baseUrl;
            }	                    this.callback_fn = domId.replace(/_uiElement$/, '') + '_callback';
            if (widget.config.previewSize) {	
                if (Object.prototype.toString.call(widget.config.previewSize) == '[object Array]') {	                    var image = widget.parts.image;
                    if (widget.config.previewSize.length == 2) {	                    var params = {'callback_fn': this.callback_fn};
                        params['preview_size'] = widget.config.previewSize.join('x');	                    if (widget.config.uploadTo) {
                        params['upload_to'] = widget.config.uploadTo;
                    }
                    if (widget.config.previewSize) {
                        if (Object.prototype.toString.call(widget.config.previewSize) == '[object Array]') {
                            if (widget.config.previewSize.length == 2) {
                                params['preview_size'] = widget.config.previewSize.join('x');
                            }
                        }
                    }
                    if (image.$.naturalWidth != image.$.width) {
                        params['max_w'] = image.$.width;
                    }
                    if (widget.data && widget.data.src) {
                        params['image'] = widget.data.src;
                    }
                    if (widget.config.urlParams && isPlainObject(widget.config.urlParams)) {
                        params = CKEDITOR.tools.extend({}, params, widget.config.urlParams);
                    }	                    }
                    this.params = params;
                    this.reload();
                },
                getUrl: function () {
                    var urlQuery = [];
                    for (var k in this.params) {
                        urlQuery.push([k, encodeURIComponent(this.params[k])].join('='));
                    }
                    return this.baseUrl + urlQuery.join('&');
                },
                reload: function () {
                    var url = this.getUrl();
                    this.iframeElement.$.src = url;
                }	                }
            }	            }
            if (image.$.naturalWidth != image.$.width) {	            cropdusterIframe.setup(this.domId, widget.config.url + '?');
                params['max_w'] = image.$.width;	            widget.cropdusterIframe = cropdusterIframe;
            }	
            if (widget.data && widget.data.src) {	
                params['image'] = widget.data.src;	
            }	
            if (widget.config.urlParams && isPlainObject(widget.config.urlParams)) {	
                params = CKEDITOR.tools.extend({}, params, widget.config.urlParams);	
            }	
            var url_query = [];	
            for (var k in params) {	
                url_query.push([k, encodeURIComponent(params[k])].join('='));	
            }	
            url += url_query.join('&');	
            cropdusterIframe = CKEDITOR.document.getById(this.domId).getChild(0);	
            cropdusterIframe.$.src = url;	


            var self = this;	            var self = this;
            var callback = function (prefix, data) {	            var callback = function (prefix, data) {
@@ -418,14 +438,14 @@ CKEDITOR.dialog.add('cropduster', function (editor) {
                    heightField.setValue(thumbData.height);	                    heightField.setValue(thumbData.height);
                    widget.setData('height', thumbData.height);	                    widget.setData('height', thumbData.height);
                    srcField.setValue(thumbData.url);	                    srcField.setValue(thumbData.url);
                    updateValue(url);	                    updateValue(cropdusterIframe.getUrl());
                }	                }
                var dialog = self.getDialog();	                var dialog = self.getDialog();
                if (dialog.fire('ok', {hide: true}).hide !== false) {	                if (dialog.fire('ok', {hide: true}).hide !== false) {
                    dialog.hide();	                    dialog.hide();
                }	                }
            };	            };
            window[callback_fn] = callback;	            window[cropdusterIframe.callback_fn] = callback;
        }	        }
    }, {	    }, {
        id: 'hasCaption',	        id: 'hasCaption',
@@ -461,6 +481,24 @@ CKEDITOR.dialog.add('cropduster', function (editor) {
        }	        }
    }	    }


    tabElements.push({
        id: 'alt',
        type: 'text',
        label: lang.alt,
        setup: function (widget) {
            this.setValue(widget.data.alt);
        },
        commit: function (widget) {
            widget.setData('alt', this.getValue());
        },
        validate: function () {
            if (editor.config.cropduster_requireAltText) {
                var value = this.getValue();
                return CKEDITOR.dialog.validate.notEmpty('Alt text describing the image is required for this field.')(value);
            }
        }
    });

    return {	    return {
        title: lang.title,	        title: lang.title,
        minWidth: 650,	        minWidth: 650,
@@ -474,7 +512,7 @@ CKEDITOR.dialog.add('cropduster', function (editor) {
        },	        },
        onShow: function () {	        onShow: function () {
            // Create a "global" reference to edited widget.	            // Create a "global" reference to edited widget.
            widget = this._.widget;	            widget = this.widget;
            // Create a "global" reference to widget's image.	            // Create a "global" reference to widget's image.
            image = widget.parts.image;	            image = widget.parts.image;
            // Reset global variables.	            // Reset global variables.
@@ -492,6 +530,19 @@ CKEDITOR.dialog.add('cropduster', function (editor) {
                toggleLockDimensions('check');	                toggleLockDimensions('check');
            });	            });
        },	        },
        onOk: function(evt) {
            var retval = CKEDITOR.dialog.validate.notEmpty(lang.urlMissing).call(this._.contents.info.src),
                invalid = typeof(retval) == 'string' || retval === false;
            if (invalid) {
                evt.data.hide = false;
                evt.stop();
                if (this.fire('cancel', {hide: true}).hide !== false) {
                    this.hide();
                }
                return false;
            }
            return true;
        },
        contents: [{	        contents: [{
            id: 'tab-basic',	            id: 'tab-basic',
            label: 'Basic',	            label: 'Basic',
@@ -516,16 +567,8 @@ CKEDITOR.dialog.add('cropduster', function (editor) {
                commit: function (widget) {	                commit: function (widget) {
                    widget.setData('src', this.getValue());	                    widget.setData('src', this.getValue());
                },	                },
                validate: CKEDITOR.dialog.validate.notEmpty(lang.urlMissing)	                validate: function() {
            }, {	                    return true;
                id: 'alt',	
                type: 'text',	
                label: lang.alt,	
                setup: function (widget) {	
                    this.setValue(widget.data.alt);	
                },	
                commit: function (widget) {	
                    widget.setData('alt', this.getValue());	
                }	                }
            }, {	            }, {
                type: 'hbox',	                type: 'hbox',
@@ -573,4 +616,4 @@ CKEDITOR.dialog.add('cropduster', function (editor) {
            }]	            }]
        }]	        }]
    };	    };
});	});
 BIN -359 Bytes (50%) 
...ter/standalone/static/ckeditor/ckeditor/plugins/cropduster/icons/cropduster.png

 BIN -719 Bytes 
...andalone/static/ckeditor/ckeditor/plugins/cropduster/icons/hidpi/cropduster.png
Binary file not shown.
  31  
cropduster/standalone/static/ckeditor/ckeditor/plugins/cropduster/plugin.js
@@ -71,11 +71,16 @@


            // Add toolbar button for this plugin.	            // Add toolbar button for this plugin.
            editor.ui.addButton && editor.ui.addButton('cropduster', {	            editor.ui.addButton && editor.ui.addButton('cropduster', {
                label: editor.lang.common.image,	                label: 'CropDuster Image',
                command: 'cropduster',	                command: 'cropduster',
                toolbar: 'insert,10'	                toolbar: 'insert,10'
            });	            });


            if (typeof editor.ui.items.Image == 'object') {
                editor.ui.items.Image.label = "Legacy Image Upload";
                editor.ui.items.Image.args[0].label = "Legacy Image Upload";
            }

            // Register context menu option for editing widget.	            // Register context menu option for editing widget.
            if (editor.contextMenu) {	            if (editor.contextMenu) {
                editor.addMenuGroup('cropduster', 10);	                editor.addMenuGroup('cropduster', 10);
@@ -278,6 +283,11 @@
            this.on('contextMenu', function(evt) {	            this.on('contextMenu', function(evt) {
                evt.data.cropduster = CKEDITOR.TRISTATE_OFF;	                evt.data.cropduster = CKEDITOR.TRISTATE_OFF;
            });	            });

            // Pass the reference to this widget to the dialog.
            this.on( 'dialog', function(evt) {
                evt.data.widget = this;
            }, this);
        },	        },


        upcast: upcastWidgetElement,	        upcast: upcastWidgetElement,
@@ -484,6 +494,7 @@
        // The other case is:	        // The other case is:
        //         <p style="text-align:center"><img></p>.	        //         <p style="text-align:center"><img></p>.
        // Then <p> takes charge of <figure> and nothing is to be changed.	        // Then <p> takes charge of <figure> and nothing is to be changed.
        image = el.getFirst('img') || (el.getFirst('a') ? el.getFirst('a').getFirst('img') : null);
        if (isCenterWrapper(el)) {	        if (isCenterWrapper(el)) {
            if (name == 'div') {	            if (name == 'div') {
                var figure = el.getFirst('figure');	                var figure = el.getFirst('figure');
@@ -492,11 +503,6 @@
            }	            }


            data.align = 'center';	            data.align = 'center';
            image = el.getFirst('img');	
        // No center wrapper has been found.	
        } else if (name == 'figure' && el.getFirst('img')) {	
            image = el.getFirst('img');	
        // Inline widget from plain img.	
        } else if (name == 'img') {	        } else if (name == 'img') {
            image = el;	            image = el;
        }	        }
@@ -577,7 +583,7 @@


        // The only child of centering wrapper can be <figure> with	        // The only child of centering wrapper can be <figure> with
        // class="caption" or plain <img>.	        // class="caption" or plain <img>.
        if (childName != 'img' && !(childName == 'figure' && child.getFirst('img'))) {	        if (childName != 'img' && !(childName == 'figure' && (child.getFirst('img') || child.getFirst('a')))) {
            return false;	            return false;
        }	        }


@@ -623,18 +629,19 @@


        // Inline widgets don't need a resizer wrapper as an image spans the entire widget.	        // Inline widgets don't need a resizer wrapper as an image spans the entire widget.
        if (!widget.inline) {	        if (!widget.inline) {
            var oldResizeWrapper = widget.element.getFirst(),	            var oldResizeWrapper = widget.element.findOne('span'),
                resizeWrapper = doc.createElement('span');	                resizeWrapper = doc.createElement('span');


            resizeWrapper.addClass('cke_cropduster_resizer_wrapper');	            resizeWrapper.addClass('cke_cropduster_resizer_wrapper');
            resizeWrapper.append(widget.parts.image);	            resizeWrapper.append(widget.parts.image.clone());
            resizeWrapper.replace(widget.parts.image);
            resizeWrapper.append(resizer);	            resizeWrapper.append(resizer);
            widget.element.append(resizeWrapper, true);	            widget.parts.image = resizeWrapper.findOne('img');


            // Remove the old wrapper which could came from e.g. pasted HTML	            // Remove the old wrapper which could came from e.g. pasted HTML
            // and which could be corrupted (e.g. resizer span has been lost).	            // and which could be corrupted (e.g. resizer span has been lost).
            if (oldResizeWrapper.is('span')) {	            if (oldResizeWrapper) {
                oldResizeWrapper.remove();	                resizeWrapper.replace(oldResizeWrapper);
            }	            }
        } else {	        } else {
            widget.wrapper.append(resizer);	            widget.wrapper.append(resizer);
  7  
cropduster/standalone/views.py
@@ -24,13 +24,14 @@ def image_file(self):
    def db_image(self):	    def db_image(self):
        if not self.image_file:	        if not self.image_file:
            return None	            return None
        md5 = self.image_file.metadata.get('md5') or self.image_file.metadata.get('DerivedFrom')
        try:	        try:
            standalone = StandaloneImage.objects.get(md5=self.image_file.metadata.get('DerivedFrom'))	            standalone = StandaloneImage.objects.get(md5=md5)
        except StandaloneImage.DoesNotExist:	        except StandaloneImage.DoesNotExist:
            (preview_w, preview_h) = self.preview_size	            (preview_w, preview_h) = self.preview_size
            standalone = StandaloneImage.objects.get_from_file(self.image_file.name,	            standalone = StandaloneImage.objects.get_from_file(self.image_file.name,
                upload_to=self.upload_to, preview_w=preview_w, preview_h=preview_h)	                upload_to=self.upload_to, preview_w=preview_w, preview_h=preview_h)
        db_image = standalone.image.cropduster_image	        db_image = standalone.image.related_object
        if not getattr(db_image, 'pk', None):	        if not getattr(db_image, 'pk', None):
            raise Exception("Image does not exist in database")	            raise Exception("Image does not exist in database")
        if not db_image.image and standalone.image.name:	        if not db_image.image and standalone.image.name:
@@ -56,6 +57,8 @@ def sizes(self):
        size = getattr(self.image_file.metadata, 'crop_size', None)	        size = getattr(self.image_file.metadata, 'crop_size', None)
        if not size:	        if not size:
            size = Size('crop', max_w=self.max_w)	            size = Size('crop', max_w=self.max_w)
        else:
            size.max_w = self.max_w
        return [size]	        return [size]


    @cached_property	    @cached_property
  291  
cropduster/static/cropduster/css/cropduster.css
@@ -1,16 +1,58 @@
.cropduster-form .grp-module {
    background: transparent;
}

.cropduster-form .image,
.cropduster-form .thumbs,
.cropduster-form .DELETE,
.cropduster-form .field_identifier,
.cropduster-form .field-image,
.cropduster-form .field-thumbs,
.cropduster-form .field-field_identifier,
.cropduster-form .inline-related .grp-collapse-handler {
    display: none;
}
.cropduster-form .inline-related,
.cropduster-form .inline-related .grp-module,
.cropduster-form .inline-related .grp-row,
.cropduster-form .inline-related .form-row {
    border: 0 !important;
}

.cropduster-form .inline-related .grp-module,
.cropduster-form .inline-related .module {
    clear: both;
}

.cropduster-form .inline-related .grp-row input {
    width: 588px;
}
.cropduster-form {	.cropduster-form {
    border: 0 !important;	    border: 0 !important;
}	}


.cropduster-form fieldset {	body.cropduster-debug .cropduster-form .image,
    display: none;	body.cropduster-debug .cropduster-form .thumbs,
body.cropduster-debug .cropduster-form .field-image,
body.cropduster-debug .cropduster-form .field-thumbs,
body.cropduster-debug .cropduster-form .DELETE,
body.cropduster-debug .cropduster-form .inline-related .grp-collapse-handler {
    display: block !important;
}

.cropduster-customfield {
    display: block;
    float: left;
}	}


body.cropduster-debug .cropduster-form fieldset {	.cropduster-form .delete {
    display: block;	    display: block;
    float: left;
    margin-left: 20px;
    margin-top: 5px;
}	}


.cropduster-customfield img{	.cropduster-customfield img {
    border: 0;	    border: 0;
}	}


@@ -20,23 +62,15 @@ body.cropduster-debug .cropduster-form fieldset {
}	}


/* buttons */	/* buttons */
.cropduster-upload-form .rounded-button,	.cropduster-upload-form .cropduster-button,
.cropduster-upload-form .rounded-button:visited,	.cropduster-upload-form .cropduster-button:visited,
.cropduster-upload-form .rounded-button:hover,	.cropduster-upload-form .cropduster-button:hover,
.cropduster-upload-form .rounded-button:active,	.cropduster-upload-form .cropduster-button:active {
.cropduster-upload-form input[type="submit"].rounded-button,	
.cropduster-upload-form input[type="submit"].rounded-button:visited,	
.cropduster-upload-form input[type="submit"].rounded-button:hover,	
.cropduster-upload-form input[type="submit"].rounded-button:active,	
.cropduster-upload-form input[type="button"].rounded-button,	
.cropduster-upload-form input[type="button"].rounded-button:visited,	
.cropduster-upload-form input[type="button"].rounded-button:hover,	
.cropduster-upload-form input[type="button"].rounded-button:active {	
	margin: 0;		margin: 0;
	display: inline-block; 		display: inline-block;
	padding: 6px 10px 7px 10px;		padding: 6px 10px 7px 10px;
	text-decoration: none;		text-decoration: none;
	-moz-border-radius: 6px; 		-moz-border-radius: 6px;
	-webkit-border-radius: 6px;		-webkit-border-radius: 6px;
	border-radius: 6px;		border-radius: 6px;
	border-bottom: 1px solid rgba(0,0,0,0.25);		border-bottom: 1px solid rgba(0,0,0,0.25);
@@ -62,16 +96,12 @@ body.cropduster-debug .cropduster-form fieldset {
	line-height: 1;		line-height: 1;
}	}


.cropduster-upload-form .rounded-button:hover,	.cropduster-upload-form .cropduster-button:hover {
.cropduster-upload-form input[type="submit"].rounded-button:hover,	
.cropduster-upload-form input[type="button"].rounded-button:hover {	
	background: -webkit-gradient(linear, 0% 0%, 0% 100%, from(#f4f4f4), to(#CACACA));		background: -webkit-gradient(linear, 0% 0%, 0% 100%, from(#f4f4f4), to(#CACACA));
	background: -moz-linear-gradient(top, #f4f4f4, #CACACA);		background: -moz-linear-gradient(top, #f4f4f4, #CACACA);
	background-color: #f4f4f4;		background-color: #f4f4f4;
}	}
.cropduster-upload-form .rounded-button:active,	.cropduster-upload-form .cropduster-button:active {
.cropduster-upload-form input[type="submit"].rounded-button:active,	
.cropduster-upload-form input[type="button"].rounded-button:active {	
	background: -webkit-gradient(linear, 0% 0%, 0% 100%, from(#D6D6D6), to(#f4f4f4));		background: -webkit-gradient(linear, 0% 0%, 0% 100%, from(#D6D6D6), to(#f4f4f4));
	background: -moz-linear-gradient(top, #D6D6D6, #f4f4f4);		background: -moz-linear-gradient(top, #D6D6D6, #f4f4f4);
	background-color: #D6D6D6;		background-color: #D6D6D6;
@@ -83,225 +113,52 @@ body.cropduster-debug .cropduster-form fieldset {
	text-shadow: rgba(255,255,255,0.5) 0 -1px 0;		text-shadow: rgba(255,255,255,0.5) 0 -1px 0;
}	}


.cropduster-upload-form .rounded-button.disabled,	.cropduster-upload-form .cropduster-button.disabled,
.cropduster-upload-form .rounded-button.disabled:hover,	.cropduster-upload-form .cropduster-button.disabled:hover,
.cropduster-upload-form .rounded-button.disabled:active,	.cropduster-upload-form .cropduster-button.disabled:active {
.cropduster-upload-form input[type="submit"].rounded-button.disabled,	
.cropduster-upload-form input[type="submit"].rounded-button.disabled:hover,	
.cropduster-upload-form input[type="submit"].rounded-button.disabled:active,	
.cropduster-upload-form input[type="button"].rounded-button.disabled,	
.cropduster-upload-form input[type="button"].rounded-button.disabled:hover,	
.cropduster-upload-form input[type="button"].rounded-button.disabled:active {	
	color: #888;		color: #888;
	cursor: default;		cursor: default;
	background: -webkit-gradient(linear, 0% 0%, 0% 100%, from(#ECECEC), to(#d1d1d1));		background: -webkit-gradient(linear, 0% 0%, 0% 100%, from(#ECECEC), to(#d1d1d1));
	background: -moz-linear-gradient(top, #ECECEC, #d1d1d1);		background: -moz-linear-gradient(top, #ECECEC, #d1d1d1);
	background-color: #ECECEC;		background-color: #ECECEC;
	border: 1px solid rgba(0, 0, 0, 0.36); /* #a3a3a3 */		border: 1px solid rgba(0, 0, 0, 0.36); /* #a3a3a3 */
	border-bottom: 1px solid rgba(0, 0, 0, 0.4); /* #9a9a9a */		border-bottom: 1px solid rgba(0, 0, 0, 0.4); /* #9a9a9a */
    outline: none;
}	}


.cropduster-upload-form .rounded-button.red,	.cropduster-upload-form .cropduster-button.small,
.cropduster-upload-form .rounded-button.red:visited,	.cropduster-upload-form .cropduster-button.small:visited,
.cropduster-upload-form .rounded-button.red:hover,	.cropduster-upload-form .cropduster-button.small:hover {
.cropduster-upload-form .rounded-button.red:active,	
.cropduster-upload-form input[type="submit"].rounded-button.red,	
.cropduster-upload-form input[type="submit"].rounded-button.red:visited,	
.cropduster-upload-form input[type="submit"].rounded-button.red:hover,	
.cropduster-upload-form input[type="submit"].rounded-button.red:active,	
.cropduster-upload-form input[type="button"].rounded-button.red,	
.cropduster-upload-form input[type="button"].rounded-button.red:visited,	
.cropduster-upload-form input[type="button"].rounded-button.red:hover,	
.cropduster-upload-form input[type="button"].rounded-button.red:active	
{	
	background: -webkit-gradient(linear, 0% 0%, 0% 100%, from(#b4463f), to(#731711));	
	background: -moz-linear-gradient(top, #b4463f, #731711);	
	background-color: #b4463f;	
	border: 1px solid #832922;	
	border-bottom: 1px solid #a43c34;	
	color: #fff;	
	-webkit-text-shadow: rgba(0,0,0,0.5) 0 -1px 0;	
	-moz-text-shadow: rgba(0,0,0,0.5) 0 -1px 0;	
	text-shadow: rgba(0,0,0,0.5) 0 -1px 0;	

}	
.cropduster-upload-form .rounded-button.red:hover,	
.cropduster-upload-form input[type="submit"].rounded-button.red:hover,	
.cropduster-upload-form input[type="button"].rounded-button.red:hover {	
	color: #fff;	
	background: -webkit-gradient(linear, 0% 0%, 0% 100%, from(#c2554e), to(#993129));	
	background: -moz-linear-gradient(top, #c2554e, #993129);	
	background-color: #c2554e;	
	border: 1px solid #ad4e47;	
	border-bottom: 1px solid #a0322a;	
}	
.cropduster-upload-form .rounded-button.red:active,	
.cropduster-upload-form input[type="submit"].rounded-button.red:active,	
.cropduster-upload-form input[type="button"].rounded-button.red:active {	
	background: -webkit-gradient(linear, 0% 0%, 0% 100%, from(#993129), to(#c2554e));	
	background: -moz-linear-gradient(top, #993129, #c2554e);	
	background-color: #993129;	
	border: 1px solid #a0322a;	
	border-bottom: 1px solid #ad4e47;	
}	


.cropduster-upload-form .rounded-button.small,	
.cropduster-upload-form .rounded-button.small:visited,	
.cropduster-upload-form .rounded-button.small:hover,	
.cropduster-upload-form input[type="submit"].rounded-button.small,	
.cropduster-upload-form input[type="submit"].rounded-button.small:visited,	
.cropduster-upload-form input[type="submit"].rounded-button.small:hover,	
.cropduster-upload-form input[type="button"].rounded-button.small,	
.cropduster-upload-form input[type="button"].rounded-button.small:visited,	
.cropduster-upload-form input[type="button"].rounded-button.small:hover {	
	padding: 3px 6px 4px 6px;		padding: 3px 6px 4px 6px;
	height: 23px;		height: 23px;
}	}


.cropduster-upload-form .rounded-button.small:active,	.cropduster-upload-form .cropduster-button.small:active {
.cropduster-upload-form input[type="submit"].rounded-button.small:active,	
.cropduster-upload-form input[type="button"].rounded-button.small:active {	
	padding: 4px 6px 3px 6px;		padding: 4px 6px 3px 6px;
	height: 23px;		height: 23px;
}	}


.cropduster-upload-form .rounded-button.green,	.cropduster-image-thumb {
.cropduster-upload-form .rounded-button.green:active,	
.cropduster-upload-form .rounded-button.green:hover,	
.cropduster-upload-form .rounded-button.green:visited,	
.cropduster-upload-form input[type="submit"].rounded-button.green,	
.cropduster-upload-form input[type="submit"].rounded-button.green:active,	
.cropduster-upload-form input[type="submit"].rounded-button.green:hover,	
.cropduster-upload-form input[type="submit"].rounded-button.green:visited,	
.cropduster-upload-form input[type="button"].rounded-button.green,	
.cropduster-upload-form input[type="button"].rounded-button.green:active,	
.cropduster-upload-form input[type="button"].rounded-button.green:hover,	
.cropduster-upload-form input[type="button"].rounded-button.green:visited {	
	color: #fff;	
	border: 0;	
	background: #3a4d00 url(../img/button-overlay.png) repeat-x 0 0;	
}	
.cropduster-upload-form .rounded-button.green:hover,	
.cropduster-upload-form input[type="submit"].rounded-button.green:hover,	
.cropduster-upload-form input[type="button"].rounded-button.green:hover	{	
	background-color: #749a02;	
}	

.cropduster-upload-form .rounded-button.blue,	
.cropduster-upload-form .rounded-button.blue:active,	
.cropduster-upload-form .rounded-button.blue:hover,	
.cropduster-upload-form .rounded-button.blue:visited,	
.cropduster-upload-form input[type="submit"].rounded-button.blue,	
.cropduster-upload-form input[type="submit"].rounded-button.blue:visited,	
.cropduster-upload-form input[type="submit"].rounded-button.blue:hover,	
.cropduster-upload-form input[type="submit"].rounded-button.blue:active,	
.cropduster-upload-form input[type="button"].rounded-button.blue,	
.cropduster-upload-form input[type="button"].rounded-button.blue:visited,	
.cropduster-upload-form input[type="button"].rounded-button.blue:hover,	
.cropduster-upload-form input[type="button"].rounded-button.blue:active {	
	color: #fff;	
	border: 0;	
	background: #162d3e url(../img/button-overlay.png) repeat-x 0 0;	
}	
.cropduster-upload-form .rounded-button.blue:hover,	
.cropduster-upload-form input[type="submit"].rounded-button.blue:hover,	
.cropduster-upload-form input[type="button"].rounded-button.blue:hover {	
	background-color: #224660;	
}	

.cropduster-upload-form .rounded-button.magenta,	
.cropduster-upload-form .rounded-button.magenta:active,	
.cropduster-upload-form .rounded-button.magenta:hover,	
.cropduster-upload-form .rounded-button.magenta:visited,	
.cropduster-upload-form input[type="submit"].rounded-button.magenta,	
.cropduster-upload-form input[type="submit"].rounded-button.magenta:visited,	
.cropduster-upload-form input[type="submit"].rounded-button.magenta:hover,	
.cropduster-upload-form input[type="submit"].rounded-button.magenta:active,	
.cropduster-upload-form input[type="button"].rounded-button.magenta,	
.cropduster-upload-form input[type="button"].rounded-button.magenta:visited,	
.cropduster-upload-form input[type="button"].rounded-button.magenta:hover,	
.cropduster-upload-form input[type="button"].rounded-button.magenta:active {	
	color: #fff;	
	border: 0;	
	background: #a9014b url(../img/button-overlay.png) repeat-x 0 0;	
}	
.cropduster-upload-form .rounded-button.magenta:hover,	
.cropduster-upload-form input[type="submit"].rounded-button.magenta:hover,	
.cropduster-upload-form input[type="button"].rounded-button.magenta:hover {	
	background-color: #630030;	
}	

.cropduster-upload-form .rounded-button.orange,	
.cropduster-upload-form .rounded-button.orange:active,	
.cropduster-upload-form .rounded-button.orange:hover,	
.cropduster-upload-form .rounded-button.orange:visited,	
.cropduster-upload-form input[type="submit"].rounded-button.orange,	
.cropduster-upload-form input[type="submit"].rounded-button.orange:visited,	
.cropduster-upload-form input[type="submit"].rounded-button.orange:hover,	
.cropduster-upload-form input[type="submit"].rounded-button.orange:active,	
.cropduster-upload-form input[type="button"].rounded-button.orange,	
.cropduster-upload-form input[type="button"].rounded-button.orange:visited,	
.cropduster-upload-form input[type="button"].rounded-button.orange:hover,	
.cropduster-upload-form input[type="button"].rounded-button.orange:active {	
	color: #fff;	
	border: 0;	
	background: #ff5c00 url(../img/button-overlay.png) repeat-x 0 0;	
}	
.cropduster-upload-form .rounded-button.orange:hover,	
.cropduster-upload-form input[type="submit"].rounded-button.orange:hover,	
.cropduster-upload-form input[type="button"].rounded-button.orange:hover {	
	background-color: #d45500;	
}	

.cropduster-upload-form .rounded-button.yellow,	
.cropduster-upload-form .rounded-button.yellow:active,	
.cropduster-upload-form .rounded-button.yellow:hover,	
.cropduster-upload-form .rounded-button.yellow:visited,	
.cropduster-upload-form input[type="submit"].rounded-button.yellow,	
.cropduster-upload-form input[type="submit"].rounded-button.yellow:visited,	
.cropduster-upload-form input[type="submit"].rounded-button.yellow:hover,	
.cropduster-upload-form input[type="submit"].rounded-button.yellow:active,	
.cropduster-upload-form input[type="button"].rounded-button.yellow,	
.cropduster-upload-form input[type="button"].rounded-button.yellow:visited,	
.cropduster-upload-form input[type="button"].rounded-button.yellow:hover,	
.cropduster-upload-form input[type="button"].rounded-button.yellow:active {	
	color: #fff;	
	border: 0;	
	background: #ffb515 url(../img/button-overlay.png) repeat-x 0 0;	
}	
.cropduster-upload-form .rounded-button.yellow:hover,	
.cropduster-upload-form input[type="submit"].rounded-button.yellow:hover,	
.cropduster-upload-form input[type="button"].rounded-button.yellow:hover {	
	background-color: #fc9200;	
}	

table.striped tfoot .rounded-button,	
table.striped tfoot .rounded-button:active,	
table.striped tfoot .rounded-button:hover,	
table.striped tfoot .rounded-button:visited {	
	padding: 4px 6px 5px;	
}	
table.striped tfoot .rounded-button:active {	
	padding: 5px 6px 4px;	
}	

.cropduster-image span {	
    background-repeat: none;	
    background-position: 0 0;	
    background-size: 100%;	
}	
.cropduster-image span {	
    display: block;	    display: block;
    float: left;	
    -webkit-box-shadow: 0px 1px 4px rgba(0, 0, 0, 0.8);	    -webkit-box-shadow: 0px 1px 4px rgba(0, 0, 0, 0.8);
       -moz-box-shadow: 0px 1px 4px rgba(0, 0, 0, 0.8);	       -moz-box-shadow: 0px 1px 4px rgba(0, 0, 0, 0.8);
            box-shadow: 0px 1px 4px rgba(0, 0, 0, 0.8);	            box-shadow: 0px 1px 4px rgba(0, 0, 0, 0.8);
}	}


.cropduster-form .cropduster-images.thumbs {
    display: block;
}
.cropduster-images .cropduster-image {	.cropduster-images .cropduster-image {
    display: none;	    display: none;
}	}
.cropduster-images .cropduster-image:first-child {	.cropduster-images .cropduster-image:first-child {
    display: block;	    display: block;
}	}

#content.colM .cropduster-form .module.aligned {
    margin-left: 8em;
    padding-left: 10px;
}
#content.colM .cropduster-form.nested-inline-form .module.aligned {
    margin-left: 0;
}
  90  
cropduster/static/cropduster/css/upload.css
@@ -1,3 +1,16 @@
body.cropduster-upload-form.grp-popup #grp-content {
    top: 0;
}

body.cropduster-upload-form .module, body.cropduster-upload-form .grp-module {
    float: none;
}

body.cropduster-upload-form ul.messagelist,
body.cropduster-upload-form ul.grp-messagelist {
    overflow: hidden;
}

body.cropduster-upload-form #crop-form {	body.cropduster-upload-form #crop-form {
    margin-top: 15px;	    margin-top: 15px;
}	}
@@ -132,9 +145,9 @@ body.cropduster-debug form#upload .row.hidden {
#nav-left {	#nav-left {
    border-right: 1px solid #000;	    border-right: 1px solid #000;
}	}
body.cropduster-upload-form #nav-left.rounded-button,	body.cropduster-upload-form #nav-left.cropduster-button,
body.cropduster-upload-form #nav-left.rounded-button:active,	body.cropduster-upload-form #nav-left.cropduster-button:active,
body.cropduster-upload-form #nav-left.rounded-button:hover {	body.cropduster-upload-form #nav-left.cropduster-button:hover {
    width: 25px;	    width: 25px;
    -webkit-border-top-left-radius: 5px;	    -webkit-border-top-left-radius: 5px;
    -webkit-border-top-right-radius: 0;	    -webkit-border-top-right-radius: 0;
@@ -152,9 +165,9 @@ body.cropduster-upload-form #nav-left.rounded-button:hover {
    margin: 0;	    margin: 0;
	padding: 4px 5px 5px 5px !important;		padding: 4px 5px 5px 5px !important;
}	}
body.cropduster-upload-form #nav-right.rounded-button,	body.cropduster-upload-form #nav-right.cropduster-button,
body.cropduster-upload-form #nav-right.rounded-button:active,	body.cropduster-upload-form #nav-right.cropduster-button:active,
body.cropduster-upload-form #nav-right.rounded-button:hover {	body.cropduster-upload-form #nav-right.cropduster-button:hover {
    width: 25px;	    width: 25px;
    -webkit-border-top-right-radius: 5px;	    -webkit-border-top-right-radius: 5px;
    -webkit-border-bottom-right-radius: 5px;	    -webkit-border-bottom-right-radius: 5px;
@@ -171,13 +184,14 @@ body.cropduster-upload-form #nav-right.rounded-button:hover {
    margin: 0;	    margin: 0;
    padding: 4px 5px 5px 5px !important;	    padding: 4px 5px 5px 5px !important;
}	}
body.cropduster-upload-form #nav-left.rounded-button:active,	body.cropduster-upload-form #nav-left.cropduster-button:active,
body.cropduster-upload-form #nav-right.rounded-button:active {	body.cropduster-upload-form #nav-right.cropduster-button:active {
    padding: 5px 5px 4px 5px !important;	    padding: 5px 5px 4px 5px !important;
}	}


body.cropduster-upload-form h1#step-header {	body.cropduster-upload-form h1#step-header {
    margin: 24px 0 8px;	    margin: 0 0 8px;
    padding: 15px 0 5px;
}	}


body.cropduster-upload-form #content-main {	body.cropduster-upload-form #content-main {
@@ -193,6 +207,7 @@ body.cropduster-upload-form form#size .row {
    width: 50%;	    width: 50%;
    float: left;	    float: left;
    padding: 8px 0;	    padding: 8px 0;
    clear: none;
}	}
body.cropduster-upload-form form#size .row,	body.cropduster-upload-form form#size .row,
body.cropduster-upload-form form#size .row:first-child,	body.cropduster-upload-form form#size .row:first-child,
@@ -237,4 +252,59 @@ body.cropduster-upload-form.cropduster-standalone form#upload #reupload-button {
}	}
body.cropduster-upload-form.cropduster-standalone #grp-content #content-inner {	body.cropduster-upload-form.cropduster-standalone #grp-content #content-inner {
    bottom: 0;	    bottom: 0;
}	}

/* Django styles without grappelli */
body.cropduster-upload-form #container {
    position: absolute;
    height: 100%;
}
body.cropduster-upload-form #content.colM {
    position: absolute;
    width: 100%;
    height: 100%;
    margin: 0;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    padding: 0 15px 10px 15px;
    box-sizing: border-box;
    -moz-box-sizing: border-box;
}
body.cropduster-upload-form #content.colM footer {
    border: 0;
    border-top: 1px solid #111;
    position: absolute;
    width: auto;
    height: 34px;
    bottom: 0;
    left: 0;
    right: 0;
    margin: 0;
    padding: 2px 5px;
    line-height: 17px;
    color: #fff;
    background: #333;
    background: -moz-linear-gradient(top, #444, #333);
    background: -webkit-gradient(linear, left top, left bottom, from(#444), to(#333));
    background: -o-linear-gradient(top, #444, #333);
    box-sizing: border-box;
    -moz-box-sizing: border-box;
    -webkit-box-sizing: border-box;
}
body.cropduster-upload-form #content.colM footer ul,
body.cropduster-upload-form #content.colM footer ul li {
    margin: 0;
    padding: 0;
    list-style-type: none;
}
body.cropduster-upload-form #content.colM footer ul li {
    float: right;
    margin-left: 10px;
}

/* Help Text: Minimum image size*/
body.cropduster-upload-form #upload-min-size-help {
    float:right;
}
  234  
cropduster/static/cropduster/js/cropduster.js
@@ -3,6 +3,106 @@ window.CropDuster = {};


(function($) {	(function($) {


    // Backport jQuery.fn.data and jQuery.fn.on/off for jQuery 1.4.2,
    // which ships with Django 1.4
    if ($.prototype.jquery == '1.4.2') {
        var rbrace = /^(?:\{[\w\W]*\}|\[[\w\W]*\])$/,
            rdashAlpha = /-([\da-z])/gi,
            rmultiDash = /([A-Z])/g,
            // Used by jQuery.camelCase as callback to replace()
            fcamelCase = function( all, letter ) {
                 return letter.toUpperCase();
             };
        $.camelCase = function(string) {
            return string.replace(rdashAlpha, fcamelCase);
        };
        $.prototype.data = (function (originalDataMethod) {
            // the parse value function is copied from the jQuery source
             function parseValue(data) {
                 if (typeof data === "string") {
                     try {
                         data = data === "true" ? true :
                             data === "false" ? false :
                             data === "null" ? null :
                             // Only convert to a number if it doesn't change the string
                             +data + "" === data ? +data :
                             rbrace.test(data) ? $.parseJSON(data) : data;
                     } catch (e) {}
                 } else {
                     data = undefined;
                 }
                 return data;
             }

             return function(key, val) {
                 var data;
                 if (typeof key === "undefined") {
                     if (this.length) {
                         data = $.data(this[0]);
                         if (this[0].nodeType === 1) {
                             var attr = this[0].attributes, name;
                             for (var i = 0, l = attr.length; i < l; i++) {
                                 name = attr[i].name;
                                 if (name.indexOf("data-") === 0) {
                                     name = $.camelCase(name.substring(5));
                                     var value = parseValue(attr[i].value);
                                     $(this[0]).data(name, value);
                                     data[name] = value;
                                 }
                             }
                         }
                     }
                     return data;
                 }

                 var result = originalDataMethod.apply(this, arguments);

                 // only when it's an getter and the result from the original data method is null
                 if ((result === null || result === undefined) && val === undefined) {
                     var attrValue = this.attr("data-" + key.replace(rmultiDash, "-$1").toLowerCase());
                     return parseValue(attrValue);
                 }
                 return result;
             };
        })($.prototype.data);

        /**
         * add support for on and off methods
         * @type {Function|*|on}
         */
        $.prototype.on = $.prototype.on || function(/* events [,selector] [,data], handler */) {
            var args = arguments;

            // delegation bind has minimal 3 arguments
            if(args.length >= 3) {
                var events = args[0],
                    selector = args[1],
                    data = (args[3]) ? args[2] : null,
                    handler = (args[3]) ? args[3] : args[2];

                this.bind(events, data, function(ev) {
                    var $target = $(ev.target).closest(selector);
                    if($target.length) {
                        handler.call($target[0], ev);
                    }
                });
            } else {
                this.bind.apply(this, args);
            }

            return this;
        };

        $.prototype.off = $.prototype.off || function(/* events [,selector] [,handler] */) {
            if(arguments.length == 3) {
                throw new Error("Delegated .off is not implemented.");
            } else {
                this.unbind.apply(this, arguments);
            }
            return this;
        };
    }

    var randomDigits = function(length) {	    var randomDigits = function(length) {
        length = parseInt(length, 10);	        length = parseInt(length, 10);
        if (!length) {	        if (!length) {
@@ -12,21 +112,6 @@ window.CropDuster = {};
        return (zeroes + Math.ceil(Math.random() * Math.pow(10, length)).toString()).slice(-1 * length);	        return (zeroes + Math.ceil(Math.random() * Math.pow(10, length)).toString()).slice(-1 * length);
    };	    };


    var image_css = function(src, width, height, opts, is_ie) {	
        var css = '';	
        src = encodeURI(src || '') + '?v=' + randomDigits(9);	
        css += 'background-image:url("' + src + '");';	
        css += 'width:' + width + 'px;';	
        css += 'height:' + height + 'px;';	
        if (is_ie) {	
            var filter = 'progid:DXImageTransform.Microsoft.AlphaImageLoader(src=\'' + src + '\', sizingMethod=\'scale\')';	
            css += 'filter:' + filter + ';';	
            css += '-ms-filter:"' + filter + '";';	
        }	
        return css;	
    };	


    var GET_params = (function() {	    var GET_params = (function() {
        var url = window.location.search.substr(1);	        var url = window.location.search.substr(1);
        var parts = url.split('&');	        var parts = url.split('&');
@@ -45,20 +130,15 @@ window.CropDuster = {};


    // jsrender templates	    // jsrender templates
    if ($.views) {	    if ($.views) {
        $.views.helpers({	
            image_css: image_css,	
            ie_image_css: function(src, width, height, opts) {	
                return image_css.call(this, src, width, height, opts, true);	
            }	
        });	

        $.templates({	        $.templates({
            cropdusterImage: '<a target="_blank" class="cropduster-image cropduster-image-{{>size_slug}}" href="{{>image_url}}">' +	            cropdusterImage: [
                '<!' + '--[if lt IE 9]' + '>' +	                '<a target="_blank"',
                '<span style="{{>~ie_image_css(image_url, width, height)}}"></span>' +	                ' class="cropduster-image cropduster-image-{{>size_slug}}"',
                '<![endif]--><![if gte IE 9]>' +	                ' href="{{>image_url}}">',
                '   <span style="{{>~image_css(image_url, width, height)}}"></span>' +	                '<img class="cropduster-image-thumb cropduster-image-thumb-{{>size_slug}}"',
                '<![endif]></a>'	                ' src="{{>image_url}}" width="{{>width}}" height="{{>height}}"/>',
                '</a>'
            ].join(""),
        });	        });
    }	    }


@@ -109,6 +189,7 @@ window.CropDuster = {};
                    'value': thumb.id,	                    'value': thumb.id,
                    'data-width': thumb.width,	                    'data-width': thumb.width,
                    'data-height': thumb.height,	                    'data-height': thumb.height,
                    'data-url': thumb.url,
                    'data-tmp-file': 'true',	                    'data-tmp-file': 'true',
                    'selected': 'selected'	                    'selected': 'selected'
                });	                });
@@ -117,13 +198,10 @@ window.CropDuster = {};
        },	        },


        complete: function(prefix, data) {	        complete: function(prefix, data) {
            var formData = {	
                'id': data.crop.image_id,	
                'image': data.crop.orig_image	
            };	
            $('#id_' + prefix + '-0-id').val(data.crop.image_id);	            $('#id_' + prefix + '-0-id').val(data.crop.image_id);
            if ($('#id_' + prefix + '-0-image').val() != data.crop.orig_image) {	            // If no image id, set INITIAL_FORM count to 0
                formData['id'] = '';	            if ($('#id_' + prefix + '-0-id').val() == '') {
                $('#id_' + prefix + '-INITIAL_FORMS').val('0');
            }	            }
            $('#id_' + prefix + '-0-image').val(data.crop.orig_image);	            $('#id_' + prefix + '-0-image').val(data.crop.orig_image);
            $('#id_' + prefix).val(data.crop.orig_image);	            $('#id_' + prefix).val(data.crop.orig_image);
@@ -132,7 +210,13 @@ window.CropDuster = {};
                return;	                return;
            }	            }
            CropDuster.setThumbnails(prefix, data.crop.thumbs);	            CropDuster.setThumbnails(prefix, data.crop.thumbs);

            // add preview_url, height, and width from context data onto input field for preview rendering
            $("#id_" + prefix).data('previewUrl', data.preview_url);
            $("#id_" + prefix).data('previewW', data.preview_w);
            $("#id_" + prefix).data('previewH', data.preview_h);
            CropDuster.createThumbnails(prefix);	            CropDuster.createThumbnails(prefix);
            $(document).trigger('cropduster:update', [prefix, data]);
        },	        },


        /**	        /**
@@ -141,13 +225,14 @@ window.CropDuster = {};
        registerInput: function(input) {	        registerInput: function(input) {
            var $input = $(input);	            var $input = $(input);
            var data = $input.data();	            var data = $input.data();
            data.prefix = $input.attr('id').replace(/^id_/, '');
            var $customField = $input.parent().find('> .cropduster-customfield');	            var $customField = $input.parent().find('> .cropduster-customfield');


            $customField.click(function(e) {	            $customField.click(function(e) {
                var $target = $(e.target).closest('.cropduster-customfield');	                var $target = $(e.target).closest('.cropduster-customfield');
                e.preventDefault();	                e.preventDefault();
                e.stopPropagation();	                e.stopPropagation();
                var $targetInput = $target.closest('.row,.grp-row').find('.cropduster-data-field').eq(0);	                var $targetInput = $target.closest('.form-row,.row,.grp-row').find('.cropduster-data-field').eq(0);
                if (!$targetInput.length) {	                if (!$targetInput.length) {
                    return;	                    return;
                }	                }
@@ -161,7 +246,7 @@ window.CropDuster = {};
                CropDuster.show(fieldName, cropdusterUrl);	                CropDuster.show(fieldName, cropdusterUrl);
            });	            });


            var $inlineForm = $input.parent().find('.cropduster-form').first();	            var $inlineForm = $input.closest('.cropduster-form');


            CropDuster.mediaUrl = $inlineForm.data('mediaUrl');	            CropDuster.mediaUrl = $inlineForm.data('mediaUrl');


@@ -171,7 +256,7 @@ window.CropDuster = {};
                name = matches[1];	                name = matches[1];
            }	            }


            var $inputRow = $input.parents('.grp-row.' + name + ',.row.' + name);	            var $inputRow = $input.closest('.grp-row.' + name + ',.row.' + name + ',.form-row.field-' + name);
            if ($inputRow.length) {	            if ($inputRow.length) {
                var inputLabel = $inputRow.find('label').html();	                var inputLabel = $inputRow.find('label').html();
                if (inputLabel) {	                if (inputLabel) {
@@ -184,11 +269,11 @@ window.CropDuster = {};
            }	            }


            $inlineForm.find('span.delete input').change(function() {	            $inlineForm.find('span.delete input').change(function() {
                form = $(this).parents('.cropduster-form');	                var $row = $(this).closest('.cropduster-form');
                if (this.checked) {	                if (this.checked) {
                    form.addClass('pre-delete');	                    $row.addClass('predelete grp-predelete');
                } else {	                } else {
                    form.removeClass('pre-delete');	                    $row.removeClass('predelete grp-predelete');
                }	                }
            });	            });
            // Re-initialize thumbnail images. This is necessary in the event that	            // Re-initialize thumbnail images. This is necessary in the event that
@@ -200,12 +285,15 @@ window.CropDuster = {};
        },	        },


        createThumbnails: function(prefix) {	        createThumbnails: function(prefix) {
            $input = $("input[data-prefix='" + prefix + "']");	            var $input = $("#id_" + prefix);
            var data = $input.data();	            var data = $input.data();
            if (!$input.length) {	            if (!$input.length) {
                return;	                return;
            }	            }
            var image = $('#id_' + prefix + '-0-image').val();	            var image = $('#id_' + prefix + '-0-image').val();
            if (!image) {
                return;
            }
            // The groups in this regex correspond to the path, basename (sans	            // The groups in this regex correspond to the path, basename (sans
            // extension), and file extension of a file path or url.	            // extension), and file extension of a file path or url.
            var matches = image.match(/^(.*)(\/(?:[^\/](?!\.[^\.\/\?]+))*[^\.\/\?])(\.[^\.\/\?]+)?$/);	            var matches = image.match(/^(.*)(\/(?:[^\/](?!\.[^\.\/\?]+))*[^\.\/\?])(\.[^\.\/\?]+)?$/);
@@ -234,26 +322,68 @@ window.CropDuster = {};
                if (data.tmpFile) {	                if (data.tmpFile) {
                    name += "_tmp";	                    name += "_tmp";
                }	                }
                var url = [CropDuster.mediaUrl, path, name + ext].join('/');	
                // This is in place of a negative lookbehind. It replaces all	
                // double slashes that don't follow a colon.	
                url = url.replace(/(:)?\/+/g, function($0, $1) { return $1 ? $0 : '/'; });	
                thumbData[slug] = {	                thumbData[slug] = {
                    'image_url': url,	                    'image_url': data.url,
                    'size_slug': slug,	                    'size_slug': slug,
                    'width': data.width,	                    'width': data.width,
                    'height': data.height	                    'height': data.height
                };	                };
            });	            });
            var $thumb = $input.closest('.row,.grp-row').find('.cropduster-images');	            var $thumb = $input.closest('.cropduster-form').find('.cropduster-images');
            $thumb.find('a').remove();	            $thumb.find('a').remove();
            preview_img = {
                'image_url': data.previewUrl,
                'size_slug': 'preview',
                'width': data.previewW,
                'height': data.previewH
            }
            $thumb.html($.render.cropdusterImage(preview_img) + $thumb.html());
        },


            $.each(data.sizes, function(i, size) {	        removeSize: function(prefix, sizeName) {
                if (!size || !size.name) return;	            var $selector = $('#id_' + prefix);
                if (thumbData[size.name]) {	
                    $thumb.html($thumb.html() + $.render.cropdusterImage(thumbData[size.name]));	            var sizes = $selector.data('sizes');

            for (var i = 0; i < sizes.length; i++) {
                if (sizes[i].name == sizeName) {
                    break;
                }	                }
            });	            }

            // Check that we found the size we need
            if (i == sizes.length) {
                return;
            }

            // values returned from $.fn.data() are references, so any modifications
            // we make to the array will persist across calls to $.fn.data()
            var removedSizes = sizes.splice(i, 1);

            var removedSizesData = $selector.data('removedSizes') || {};
            if ($.isEmptyObject(removedSizesData)) {
                $selector.data('removedSizes', removedSizesData);
            }

            removedSizesData[sizeName] = {
                index: i,
                size: removedSizes[0]
            };
        },

        restoreSize: function(prefix, sizeName) {
            var $selector = $('#id_' + prefix);
            var sizes = $selector.data('sizes');
            var removedSizesData = $selector.data('removedSizes');

            // If no size with sizeName has yet been removed, return
            if (!removedSizesData || !removedSizesData[sizeName]) {
                return;
            }

            var sizeToRestore = removedSizesData[sizeName];
            sizes.splice(sizeToRestore.index, 0, sizeToRestore.size);
            delete removedSizesData[sizeName];
        }	        }


    };	    };
  2  
cropduster/static/cropduster/js/jquery.form.js
@@ -88,7 +88,7 @@ $.fn.ajaxSubmit = function(options) {
		url:  url,			url:  url,
		success: $.ajaxSettings.success,			success: $.ajaxSettings.success,
		type: this[0].getAttribute('method') || 'GET', // IE7 massage (see issue 57)			type: this[0].getAttribute('method') || 'GET', // IE7 massage (see issue 57)
		iframeSrc: /^https/i.test(window.location.href || '') ? 'javascript:false' : 'about:blank'			iframeSrc: 'about:blank'
	}, options);		}, options);


	// hook for manipulating the form data before it is extracted;		// hook for manipulating the form data before it is extracted;
  144  
cropduster/static/cropduster/js/jquery.jcrop.js
@@ -62,6 +62,13 @@
    function setOptions(opt) //{{{	    function setOptions(opt) //{{{
    {	    {
      if (typeof(opt) !== 'object') opt = {};	      if (typeof(opt) !== 'object') opt = {};

      if (opt.aspectRatio) {
        opt.minAspectRatio = opt.aspectRatio;
        opt.maxAspectRatio = opt.aspectRatio;
        delete opt.aspectRatio;
      }

      options = $.extend(options, opt);	      options = $.extend(options, opt);


      $.each(['onChange','onSelect','onRelease','onDblClick'],function(i,e) {	      $.each(['onChange','onSelect','onRelease','onDblClick'],function(i,e) {
@@ -84,14 +91,15 @@


      Coords.setPressed(Coords.getCorner(opp));	      Coords.setPressed(Coords.getCorner(opp));
      Coords.setCurrent(opc);	      Coords.setCurrent(opc);
      Coords.setWidthHeight(fc.w, fc.h);


      Tracker.activateHandlers(dragmodeHandler(mode, fc), doneSelect, touch);	      Tracker.activateHandlers(dragmodeHandler(mode, fc), doneSelect, touch);
    }	    }
    //}}}	    //}}}
    function dragmodeHandler(mode, f) //{{{	    function dragmodeHandler(mode, f) //{{{
    {	    {
      return function (pos) {	      return function (pos) {
        if (!options.aspectRatio) {	        if (!options.minAspectRatio || !options.maxAspectRatio) {
          switch (mode) {	          switch (mode) {
          case 'e':	          case 'e':
            pos[1] = f.y2;	            pos[1] = f.y2;
@@ -122,7 +130,7 @@
            break;	            break;
          }	          }
        }	        }
        Coords.setCurrent(pos);	        Coords.setCurrent(pos, mode);
        Selection.update();	        Selection.update();
      };	      };
    }	    }
@@ -227,15 +235,11 @@
    //}}}	    //}}}
    function newSelection(e) //{{{	    function newSelection(e) //{{{
    {	    {
      var c = Coords.getFixed();	
      if ((c.w > options.minSelect[0]) && c.h > options.minSelect[1]) {	
        return false;	
      }	
      if (options.disabled) {	      if (options.disabled) {
        return false;	        return;
      }	      }
      if (!options.allowSelect) {	      if (!options.allowSelect) {
        return false;	        return;
      }	      }
      btndown = true;	      btndown = true;
      docOffset = getPos($img);	      docOffset = getPos($img);
@@ -463,7 +467,7 @@
          y1 = 0,	          y1 = 0,
          x2 = 0,	          x2 = 0,
          y2 = 0,	          y2 = 0,
          ox, oy;	          ox, oy, iw, ih;


      function setPressed(pos) //{{{	      function setPressed(pos) //{{{
      {	      {
@@ -472,13 +476,54 @@
        y2 = y1 = pos[1];	        y2 = y1 = pos[1];
      }	      }
      //}}}	      //}}}
      function setCurrent(pos) //{{{	      function setCurrent(pos, mode) //{{{
      {	      {
        pos = rebound(pos);	        pos = rebound(pos);
        var c1, c2, old_x1 = x1, old_y1 = y1;
        if (typeof mode != 'undefined') {
          c1 = Coords.getFixed();
          x1 = old_x1;
          y1 = old_y1;
        }
        ox = pos[0] - x2;	        ox = pos[0] - x2;
        oy = pos[1] - y2;	        oy = pos[1] - y2;
        x2 = pos[0];	        x2 = pos[0];
        y2 = pos[1];	        y2 = pos[1];
        if (typeof mode == 'undefined') {
          return;
        }
        c2 = Coords.getFixed();
        x1 = old_x1;
        y1 = old_y1;
        if (c1.w == c2.w && c1.h == c2.h) {
          return;
        }
        if (ox !== 0 && oy !== 0) {
          return;
        }
        var aspect = c2.w / c2.h,
            minAspect = options.minAspectRatio,
            maxAspect = options.maxAspectRatio;
        if (minAspect && aspect <= minAspect || maxAspect && aspect >= maxAspect) {
          switch (mode) {
            case 'n':
            case 's':
              var dx = c1.x2 - c2.x2;
              x1 += dx / 2;
              break;
            case 'e':
            case 'w':
              var dy = c1.y2 - c2.y2;
              y1 += dy / 2;
              break;
          }
        }
      }
      //}}}
      function setWidthHeight(w, h) //{{{
      {
        iw = w;
        ih = h;
      }	      }
      //}}}	      //}}}
      function getOffset() //{{{	      function getOffset() //{{{
@@ -528,11 +573,12 @@
      //}}}	      //}}}
      function getFixed() //{{{	      function getFixed() //{{{
      {	      {
        if (!options.aspectRatio) {	        if (!options.minAspectRatio && !options.maxAspectRatio) {
          return getRect();	          return getRect();
        }	        }
        // This function could use some optimization I think...	        // This function could use some optimization I think...
        var aspect = options.aspectRatio,	        var minAspect = options.minAspectRatio,
            maxAspect = options.maxAspectRatio,
            min_x = options.minSize[0] / xscale,	            min_x = options.minSize[0] / xscale,




@@ -544,43 +590,49 @@
            rwa = Math.abs(rw),	            rwa = Math.abs(rw),
            rha = Math.abs(rh),	            rha = Math.abs(rh),
            real_ratio = rwa / rha,	            real_ratio = rwa / rha,
            xx, yy, w, h;	            xx, yy, w, h, aspect,
            vertical = function() {
                yy = y2;
                w = rha * aspect;
                xx = rw < 0 ? x1 - w : w + x1;

                if (xx < 0) {
                  xx = 0;
                } else if (xx > boundx) {
                  xx = boundx;
                }
                h = Math.abs((xx - x1) / aspect);
                yy = rh < 0 ? y1 - h : h + y1;
            },
            horizontal = function() {
                xx = x2;
                h = rwa / aspect;
                yy = rh < 0 ? y1 - h : y1 + h;
                if (yy < 0) {
                  yy = 0;
                } else if (yy > boundy) {
                  yy = boundy;
                }
                w = Math.abs((yy - y1) * aspect);
                xx = rw < 0 ? x1 - w : w + x1;
            };


        if (max_x === 0) {	        if (max_x === 0) {
          max_x = boundx * 10;	          max_x = boundx * 10;
        }	        }
        if (max_y === 0) {	        if (max_y === 0) {
          max_y = boundy * 10;	          max_y = boundy * 10;
        }	        }
        if (real_ratio < aspect) {	        if (minAspect && real_ratio < minAspect) {
          yy = y2;	          aspect = minAspect;
          w = rha * aspect;	        } else if (maxAspect && real_ratio > maxAspect) {
          xx = rw < 0 ? x1 - w : w + x1;	          aspect = maxAspect;

          if (xx < 0) {	
            xx = 0;	
            h = Math.abs((xx - x1) / aspect);	
            yy = rh < 0 ? y1 - h : h + y1;	
          } else if (xx > boundx) {	
            xx = boundx;	
            h = Math.abs((xx - x1) / aspect);	
            yy = rh < 0 ? y1 - h : h + y1;	
          }	
        } else {	        } else {
          xx = x2;	          return getRect();
          h = rwa / aspect;	
          yy = rh < 0 ? y1 - h : y1 + h;	
          if (yy < 0) {	
            yy = 0;	
            w = Math.abs((yy - y1) * aspect);	
            xx = rw < 0 ? x1 - w : w + x1;	
          } else if (yy > boundy) {	
            yy = boundy;	
            w = Math.abs(yy - y1) * aspect;	
            xx = rw < 0 ? x1 - w : w + x1;	
          }	
        }	        }


        Math.abs(rwa - iw) > Math.abs(rha - ih) ? horizontal() : vertical();

        // Magic %-)	        // Magic %-)
        if (xx > x1) { // right side	        if (xx > x1) { // right side
          if (xx - x1 < min_x) {	          if (xx - x1 < min_x) {
@@ -633,7 +685,7 @@
        if (p[0] > boundx) p[0] = boundx;	        if (p[0] > boundx) p[0] = boundx;
        if (p[1] > boundy) p[1] = boundy;	        if (p[1] > boundy) p[1] = boundy;


        return [p[0], p[1]];	        return [Math.round(p[0]), Math.round(p[1])];
      }	      }
      //}}}	      //}}}
      function flipCoords(x1, y1, x2, y2) //{{{	      function flipCoords(x1, y1, x2, y2) //{{{
@@ -659,11 +711,11 @@
            ysize = y2 - y1,	            ysize = y2 - y1,
            delta;	            delta;


        if (xlimit && (Math.abs(xsize) > xlimit)) {	        if (xlimit && (Math.abs(xsize) > xlimit / xscale)) {
          x2 = (xsize > 0) ? (x1 + xlimit) : (x1 - xlimit);	          x2 = (xsize > 0) ? (x1 + xlimit / xscale) : (x1 - xlimit / xscale);
        }	        }
        if (ylimit && (Math.abs(ysize) > ylimit)) {	        if (ylimit && (Math.abs(ysize) > ylimit / yscale)) {
          y2 = (ysize > 0) ? (y1 + ylimit) : (y1 - ylimit);	          y2 = (ysize > 0) ? (y1 + ylimit / yscale) : (y1 - ylimit / yscale);
        }	        }


        if (ymin / yscale && (Math.abs(ysize) < ymin / yscale)) {	        if (ymin / yscale && (Math.abs(ysize) < ymin / yscale)) {
@@ -730,6 +782,7 @@
        flipCoords: flipCoords,	        flipCoords: flipCoords,
        setPressed: setPressed,	        setPressed: setPressed,
        setCurrent: setCurrent,	        setCurrent: setCurrent,
        setWidthHeight: setWidthHeight,
        getOffset: getOffset,	        getOffset: getOffset,
        moveOffset: moveOffset,	        moveOffset: moveOffset,
        getCorner: getCorner,	        getCorner: getCorner,
@@ -1664,7 +1717,8 @@
    handleOpacity: 0.5,	    handleOpacity: 0.5,
    handleSize: null,	    handleSize: null,


    aspectRatio: 0,	    minAspectRatio: 0,
    maxAspectRatio: 0,
    keySupport: true,	    keySupport: true,
    createHandles: ['n','s','e','w','nw','ne','se','sw'],	    createHandles: ['n','s','e','w','nw','ne','se','sw'],
    createDragbars: ['n','s','e','w'],	    createDragbars: ['n','s','e','w'],
 19  
cropduster/static/cropduster/js/jquery.jcrop.min.js
Large diffs are not rendered by default.

 219  
cropduster/static/cropduster/js/upload.js
Large diffs are not rendered by default.

  19  
cropduster/templates/cropduster/custom_field.html
@@ -1,17 +1,21 @@
{% load i18n adminmedia %}	{% load i18n %}

<div class="module cropduster-form nested-inline-form" id="{{ inline_admin_formset.formset.prefix }}-group" data-media-url="{{ media_url }}">


<input type="hidden" id="{{ final_attrs.id }}-0-id" name="{{ final_attrs.name }}-0-id" value="{{ final_attrs.value }}"/>	<input type="hidden" id="{{ final_attrs.id }}-0-id" name="{{ final_attrs.name }}-0-id" value="{{ final_attrs.value }}"/>
<input type="text"	<input type="text"
       id="{{ final_attrs.id }}"	       id="{{ final_attrs.id }}"
       name="{{ final_attrs.name }}"	       name="{{ final_attrs.name }}"
       value="{{ image_value }}"	       value="{{ file_value }}"
       class="cropduster-data-field cropduster-text-field"	       class="cropduster-data-field cropduster-text-field"
       data-sizes="{{ final_attrs.sizes }}"	       data-sizes="{{ sizes }}"
       data-upload-to="{{ upload_to }}"	       data-preview-url="{{ preview_url }}"
       data-prefix="{{ prefix }}"/>	       data-preview-w="{{ preview_w }}"
       data-preview-h="{{ preview_h }}"
       data-upload-to="{{ upload_to }}"/>


<a href="#" class="cropduster-customfield cropduster-upload-form" data-cropduster-url="{% url cropduster-index %}?pop=1">	<a href="#" class="cropduster-customfield cropduster-upload-form" data-cropduster-url="{% url 'cropduster-index' %}?pop=1">
    <div class="rounded-button">Upload Image</div>	    <div class="cropduster-button">Upload Image</div>
    <div style="clear:both; height:3px"></div>	    <div style="clear:both; height:3px"></div>
</a>	</a>


@@ -24,3 +28,4 @@
<div style="clear:both"></div>	<div style="clear:both"></div>




</div>
 8  
cropduster/templates/cropduster/inline.html
@@ -1,18 +1,14 @@
{% load i18n adminmedia %}	{% load i18n %}

<div class="module cropduster-form" id="{{ inline_admin_formset.formset.prefix }}-group" data-media-url="{{ media_url }}">	


{{ inline_admin_formset.formset.management_form }}	{{ inline_admin_formset.formset.management_form }}
{{ inline_admin_formset.formset.non_form_errors }}	{{ inline_admin_formset.formset.non_form_errors }}


{% for inline_admin_form in inline_admin_formset %}	{% for inline_admin_form in inline_admin_formset %}
    <div class="inline-related{% if forloop.last %} empty-form last-related{% endif %}" id="{{ inline_admin_formset.formset.prefix }}-{% if not forloop.last %}{{ forloop.counter0 }}{% else %}empty{% endif %}">	    <div class="{% if forloop.last %} empty-form grp-empty-form last-related{% endif %}" id="{{ inline_admin_formset.formset.prefix }}-{% if not forloop.last %}{{ forloop.counter0 }}{% else %}empty{% endif %}">
        {% if inline_admin_formset.formset.can_delete and inline_admin_form.original %}<span class="delete">{{ inline_admin_form.deletion_field.field }} {{ inline_admin_form.deletion_field.label_tag }}</span>{% endif %}	        {% if inline_admin_formset.formset.can_delete and inline_admin_form.original %}<span class="delete">{{ inline_admin_form.deletion_field.field }} {{ inline_admin_form.deletion_field.label_tag }}</span>{% endif %}
        {% if inline_admin_form.form.non_field_errors %}{{ inline_admin_form.form.non_field_errors }}{% endif %}	        {% if inline_admin_form.form.non_field_errors %}{{ inline_admin_form.form.non_field_errors }}{% endif %}
        {% for fieldset in inline_admin_form %}	        {% for fieldset in inline_admin_form %}
            {% include "admin/includes/fieldset.html" %}	            {% include "admin/includes/fieldset.html" %}
        {% endfor %}	        {% endfor %}
        {{ inline_admin_form.fk_field.field }}	
    </div>	    </div>
{% endfor %}	{% endfor %}
</div>	
  69  
cropduster/templates/cropduster/upload.html
@@ -1,9 +1,15 @@
{% extends parent_template %}	{% extends parent_template %}


<!-- LOADING -->	<!-- LOADING -->
{% load i18n adminmedia %}	{% load i18n %}


{% block extrahead %}	{% block extrahead %}
    {% if django_is_gte_19 %}
    <script type="text/javascript" src="{{ STATIC_URL }}admin/js/vendor/jquery/jquery.min.js"></script>
    {% else %}
    <script type="text/javascript" src="{{ STATIC_URL }}admin/js/jquery.min.js"></script>
    {% endif %}
    <script type="text/javascript" src="{{ STATIC_URL }}admin/js/jquery.init.js"></script>
    {{ block.super }}	    {{ block.super }}
    {{ crop_form.media }}	    {{ crop_form.media }}
    {{ thumb_formset.media }}	    {{ thumb_formset.media }}
@@ -25,47 +31,50 @@
<h1 id="step-header">Upload, Crop, and Generate Thumbnails</h1>	<h1 id="step-header">Upload, Crop, and Generate Thumbnails</h1>
{% endif %}	{% endif %}
<div id="content-main">	<div id="content-main">
    <fieldset class="module aligned">	    <fieldset class="module grp-module aligned">


        <form id="upload" action="{% url cropduster.views.upload %}{% if standalone %}?standalone=1{% endif %}" method="POST">	        <form id="upload" action="{% url 'cropduster-upload' %}{% if standalone %}?standalone=1{% endif %}" method="POST">
            {% for field in upload_form %}	            {% for field in upload_form %}
                <div class="row {{ field.name }}{% if field.name != 'image' %} hidden{% endif %}">	                <div class="grp-row row {{ field.name }}{% if field.name != 'image' %} hidden{% endif %}">
                    {% if field.name != "image" %}{{ field.label_tag|safe }}{% endif %}	                    {% if field.name != "image" %}{{ field.label_tag|safe }}{% endif %}
                    {{ field }}	                    {{ field }}
                    {% if field.name == "image" %}
                        <div id="upload-min-size-help"></div>
                    {% endif %}
                </div>	                </div>
            {% endfor %}	            {% endfor %}
            {% if standalone %}	            {% if standalone %}
            {# <li class="submit-button-container"> #}	
                <div id="upload-footer"{% if not image_id %} style="display: none"{% endif %}>	                <div id="upload-footer"{% if not image_id %} style="display: none"{% endif %}>
                <input id="upload-button" class="rounded-button disabled{% if standalone %} small{% endif %}" type="submit" name="_save" value='Upload'  onclick="return uploadSubmit();"/>	                    <input id="upload-button" class="cropduster-button disabled{% if standalone %} small{% endif %}" type="submit" name="_save" value='Upload'  onclick="return uploadSubmit(this);"/>
                </div>	                </div>
                <div id="crop-footer"{% if image_id %} style="display: none"{% endif %}>	                <div id="crop-footer"{% if image_id %} style="display: none"{% endif %}>
                <input id="reupload-button" class="rounded-button disabled{% if standalone %} small{% endif %}" type="submit" name="_save" value='Re-Upload' onclick="return uploadSubmit();" />	                    <input id="reupload-button" class="cropduster-button disabled{% if standalone %} small{% endif %}" type="submit" name="_save" value='Re-Upload' onclick="return uploadSubmit(this);" />
                </div>	                </div>
            {# </li> #}	
            {% endif %}	            {% endif %}
        </form>	        </form>


        {% if standalone %}	        {% if standalone %}
        <form id="size" action="" onsubmit="return false">	        <form id="size" action="" onsubmit="return false">
                <div class="row cells-1 width">	            <div class="row form-row grp-row cells-1 grp-cells-1 width">
                    <div class="column span-4">	                <div class="field-box l-2c-fluid l-d-4">
                    <div class="column span-4 c-1">
                        <label for="id_size-width">Width</label>	                        <label for="id_size-width">Width</label>
                    </div>	                    </div>
                    <div class="column span-flexible">	                    <div class="column span-flexible c-2">
                        <input type="text" name="size-width" id="id_size-width" />	                        <input type="text" name="size-width" id="id_size-width" />
                    </div>	                    </div>
                    <div class="float-clear-div" style="clear:both;height:0;width:0"></div>	
                </div>	                </div>
                <div class="row cells-1 height">	            </div>
                    <div class="column span-4">	            <div class="row form-row grp-row cells-1 grp-cells-1 height">
                <div class="field-box l-2c-fluid l-d-4">
                    <div class="column span-4 c-1">
                        <label for="id_size-height">Height</label>	                        <label for="id_size-height">Height</label>
                    </div>	                    </div>
                    <div class="column span-flexible">	                    <div class="column span-flexible c-2">
                        <input type="text" name="size-height" id="id_size-height" />	                        <input type="text" name="size-height" id="id_size-height" />
                    </div>	                    </div>
                    <div class="float-clear-div" style="clear:both;height:0;height:0"></div>	
                </div>	                </div>
            </div>
        </form>	        </form>
        {% endif %}	        {% endif %}


@@ -75,7 +84,7 @@ <h1 id="step-header">Upload, Crop, and Generate Thumbnails</h1>
        <p class="errornote"></p>	        <p class="errornote"></p>
    </div>	    </div>


    <form action="{% url cropduster.views.crop %}" method="POST" id="crop-form">	    <form action="{% url 'cropduster-crop' %}" method="POST" id="crop-form">
        <div id="image-container">	        <div id="image-container">
            <img src="{{ image }}" id="cropbox" />	            <img src="{{ image }}" id="cropbox" />
        </div>	        </div>
@@ -90,35 +99,35 @@ <h1 id="step-header">Upload, Crop, and Generate Thumbnails</h1>
                {% endfor %}	                {% endfor %}
            </div>	            </div>
        </div>	        </div>
        <div class="module footer">	        <footer class="module grp-module grp-submit-row footer grp-fixed-footer">
            <div id="crop-nav">	            <div id="crop-nav">
                <div id="nav-left" class="rounded-button disabled"><span></span></div>	                <div id="nav-left" class="cropduster-button disabled"><span></span></div>
                <div id="nav-right" class="rounded-button disabled"><span></span></div>	                <div id="nav-right" class="cropduster-button disabled"><span></span></div>
            </div>	            </div>
            <div id="current-thumb-info">	            <div id="current-thumb-info">
                <div id="current-thumb-index"></div>	                <div id="current-thumb-index"></div>
                <div id="thumb-total-count"></div>	                <div id="thumb-total-count"></div>
                <div id="current-thumb-label"></div>	                <div id="current-thumb-label"></div>
            </div>	            </div>
            {% if not standalone %}	            {% if not standalone %}
            <ul class="submit-row" id="upload-footer"{% if not image_id %} style="display: none"{% endif %}>	            <ul class="submit-row grp-submit-row" id="upload-footer"{% if not image_id %} style="display: none"{% endif %}>
                <li class="submit-button-container">	                <li class="submit-button-container grp-submit-button-container">
                    <input id="upload-button" class="rounded-button disabled{% if standalone %} small{% endif %}" type="submit" name="_save" value='Upload'  onclick="return uploadSubmit();"/>	                    <input id="upload-button" class="cropduster-button disabled{% if standalone %} small{% endif %}" type="submit" name="_save" value='Upload'  onclick="return uploadSubmit(this);"/>
                </li>	                </li>
            </ul>	            </ul>
            {% endif %}	            {% endif %}
            <ul class="submit-row" id="crop-footer"{% if image_id %} style="display: none"{% endif %}>	            <ul class="grp-submit-row submit-row" id="crop-footer"{% if image_id %} style="display: none"{% endif %}>
                <li class="submit-button-container">	                <li class="submit-button-container grp-submit-button-container">
                    <input id="crop-button" class="rounded-button{% if standalone %} small{% endif %}" type="submit" name="crop" value="Crop and Continue" />	                    <input id="crop-button" class="cropduster-button{% if standalone %} small{% endif %}" type="submit" name="crop" value="Crop and Continue" />
                </li>	                </li>
                {% if not standalone %}	                {% if not standalone %}
                <li class="submit-button-container">	                <li class="submit-button-container grp-submit-button-container">
                    <input id="reupload-button" class="rounded-button disabled{% if standalone %} small{% endif %}" type="submit" name="_save" value='Re-Upload' onclick="return uploadSubmit();" />	                    <input id="reupload-button" class="cropduster-button disabled{% if standalone %} small{% endif %}" type="submit" name="_save" value='Re-Upload' onclick="return uploadSubmit(this);" />
                </li>	                </li>
                {% endif %}	                {% endif %}
            </ul>	            </ul>
        </div>	        </footer>
    </form>	    </form>


</div>	</div>
{% endblock %}	{% endblock %}
 67  
cropduster/templatetags/cropduster_tags.py
@@ -1,33 +1,74 @@
import time
import warnings

import django
from django import template	from django import template
from cropduster.models import Image
from cropduster.resizing import Size


register = template.Library()	register = template.Library()


@register.assignment_tag	
def get_crop(image, crop_name):	if django.VERSION >= (1, 9):
    tag_decorator = register.simple_tag
else:
    tag_decorator = register.assignment_tag


@tag_decorator
def get_crop(image, crop_name, **kwargs):
    """	    """
    Get the crop of an image. Usage:	    Get the crop of an image. Usage:
    {% get_crop article.image 'square_thumbnail' as crop %}	    {% get_crop article.image 'square_thumbnail' attribution=1 as img %}
    will return a dictionary of	    will assign to `img` a dictionary that looks like:
    {	    {
        "url": /media/path/to/my.jpg,	        "url": '/media/path/to/my.jpg',
        "width": 150,	        "width": 150,
        "height" 150,	        "height" 150,
        "attribution": 'Stock Photoz',
        "attribution_link": 'http://stockphotoz.com',
        "caption": 'Woman laughing alone with salad.',
        "alt_text": 'Woman laughing alone with salad.'
    }	    }
    For use in an image tag or style block.	    For use in an image tag or style block like:
        <img src="{{ img.url }}">
    The `exact_size` kwarg is deprecated.
    Omitting the `attribution` kwarg will omit the attribution, attribution_link,
    and caption.
    """	    """


    # If this isn't a cropduster field, abort	    if "exact_size" in kwargs:
    if not getattr(image, 'cropduster_image', None):	        warnings.warn("get_crop's `exact_size` kwarg is deprecated.", DeprecationWarning)

    if not image or not image.related_object:
        return None	        return None
    w, h = image.cropduster_image.get_image_size(size_name=crop_name)	
    url = image.cropduster_image.get_image_url(size_name=crop_name)	


    url = getattr(Image.get_file_for_size(image, crop_name), 'url', None)

    thumbs = {thumb.name: thumb for thumb in image.related_object.thumbs.all()}
    try:
        thumb = thumbs[crop_name]
    except KeyError:
        if crop_name == "original":
            thumb = image.related_object
        else:
            return None

    cache_buster = str(time.mktime(thumb.date_modified.timetuple()))[:-2]
    return {	    return {
        "width": w,	        "url": "%s?%s" % (url, cache_buster),
        "height": h,	        "width": thumb.width,
        "url": url,	        "height": thumb.height,
        "attribution": image.related_object.attribution,
        "attribution_link": image.related_object.attribution_link,
        "caption": image.related_object.caption,
        "alt_text": image.related_object.alt_text,
    }	    }
 20  
cropduster/urls.py
@@ -1,12 +1,12 @@
try:	from django.conf.urls import url
    from django.conf.urls import patterns, url	
except ImportError:	
    from django.conf.urls.defaults import patterns, url	


import cropduster.views
import cropduster.standalone.views


urlpatterns = patterns('',	
    url(r'^$', 'cropduster.views.index', name='cropduster-index'),	urlpatterns = [
    url(r'^crop/', 'cropduster.views.crop', name='cropduster-crop'),	    url(r'^$', cropduster.views.index, name='cropduster-index'),
    url(r'^upload/', 'cropduster.views.upload', name='cropduster-upload'),	    url(r'^crop/', cropduster.views.crop, name='cropduster-crop'),
    url(r'^standalone/', 'cropduster.standalone.views.index', name='cropduster-standalone'),	    url(r'^upload/', cropduster.views.upload, name='cropduster-upload'),
)	    url(r'^standalone/', cropduster.standalone.views.index, name='cropduster-standalone'),
]
 8  
cropduster/utils/__init__.py
@@ -1,4 +1,8 @@
from .image import get_image_extension	from .image import (
from .paths import get_upload_foldername, get_media_path, get_relative_media_url	    get_image_extension, is_transparent, exif_orientation,
    correct_colorspace, is_animated_gif, has_animated_gif_support, process_image,
    smart_resize)
from .paths import get_upload_foldername
from .sizes import get_min_size	from .sizes import get_min_size
from .thumbs import set_as_auto_crop, unset_as_auto_crop
from . import jsonutils as json	from . import jsonutils as json
 55  
cropduster/utils/gifsicle.py
@@ -0,0 +1,55 @@
import logging
import os
import subprocess

from cropduster.settings import CROPDUSTER_GIFSICLE_PATH
from django.core.files.storage import default_storage


logger = logging.getLogger(__name__)


class GifsicleImage(object):

    def __init__(self, im):
        if not CROPDUSTER_GIFSICLE_PATH:
            raise Exception(
                "Cannot use GifsicleImage without the gifsicle binary in the PATH")

        self.pil_image = im
        self.size = im.size
        self.cmd_args = [CROPDUSTER_GIFSICLE_PATH, '-O3', '-I', '-I', '-w']
        self.crop_args = []
        self.resize_args = []

    @property
    def args(self):
        return self.cmd_args + self.crop_args + self.resize_args

    def crop(self, box):
        x1, y1, x2, y2 = box
        if x2 < x1:
            x2 = x1
        if y2 < y1:
            y2 = y1

        self.size = (x2 - x1, y2 - y1)
        self.crop_args = ['--crop', "%d,%d-%d,%d" % (x1, y1, x2, y2)]
        return self

    def resize(self, size, method):
        # Ignore method, PIL's algorithms don't match up
        self.resize_args = [
            "--resize-fit", "%dx%d" % size,
            "--resize-method", "mix",
            "--resize-colors", "128",
        ]
        return self

    def save(self, buf, **kwargs):
        proc = subprocess.Popen(self.args, stdin=subprocess.PIPE, stdout=subprocess.PIPE, stderr=subprocess.PIPE)
        with default_storage.open(self.pil_image.filename, 'rb') as f:
            out, err = proc.communicate(input=f.read())
        logger.debug(err)
        buf.write(out)
        buf.seek(0)
  188  
cropduster/utils/image.py
@@ -1,9 +1,35 @@
from __future__ import division	from __future__ import division


from io import BytesIO
import os
import warnings
import math
from distutils.version import LooseVersion

import PIL.Image	import PIL.Image
from PIL import ImageFile, JpegImagePlugin

from django.core.files.storage import default_storage
from django.utils import six
from django.utils.six.moves import xrange

from cropduster.settings import (
    get_jpeg_quality, JPEG_SAVE_ICC_SUPPORTED, CROPDUSTER_GIFSICLE_PATH)

from .gifsicle import GifsicleImage



__all__ = (
    'get_image_extension', 'is_transparent', 'exif_orientation',
    'correct_colorspace', 'is_animated_gif', 'has_animated_gif_support',
    'process_image', 'smart_resize')


__all__ = ('get_image_extension')	
# workaround for https://github.com/python-pillow/Pillow/issues/1138
# without this hack, pillow misidenfifies some jpeg files as "mpo" files
JpegImagePlugin._getmp = lambda x: None  # noqa

ImageFile.MAXBLOCK = 4096 * 4096 * 8




IMAGE_EXTENSIONS = {	IMAGE_EXTENSIONS = {
@@ -14,16 +40,174 @@
    "MSP":  ".msp",   "Palm": ".palm",  "PCD":  ".pcd",   "PCX":  ".pcx",   "PDF":  ".pdf",	    "MSP":  ".msp",   "Palm": ".palm",  "PCD":  ".pcd",   "PCX":  ".pcx",   "PDF":  ".pdf",
    "PNG":  ".png",   "PPM":  ".ppm",   "PSD":  ".psd",   "SGI":  ".rgb",   "SUN":  ".ras",	    "PNG":  ".png",   "PPM":  ".ppm",   "PSD":  ".psd",   "SGI":  ".rgb",   "SUN":  ".ras",
    "TGA":  ".tga",   "TIFF": ".tiff",  "WMF":  ".wmf",   "XBM":  ".xbm",   "XPM":  ".xpm",	    "TGA":  ".tga",   "TIFF": ".tiff",  "WMF":  ".wmf",   "XBM":  ".xbm",   "XPM":  ".xpm",
    "MPO":  ".jpg",  # Pillow mislabels some jpeg images as MPO files
}	}




def get_image_extension(img):	def get_image_extension(img):
    if img.format in IMAGE_EXTENSIONS:	    if img.format in IMAGE_EXTENSIONS:
        return IMAGE_EXTENSIONS[img.format]	        return IMAGE_EXTENSIONS[img.format]
    else:	    else:
        for ext, format in PIL.Image.EXTENSION.iteritems():	        for ext, format in six.iteritems(PIL.Image.EXTENSION):
            if format == img.format:	            if format == img.format:
                return ext	                return ext
        # Our fallback is the PIL format name in lowercase,	        # Our fallback is the PIL format name in lowercase,
        # which is probably the file extension	        # which is probably the file extension
        return ".%s" % img.format.lower()	        return ".%s" % img.format.lower()


def is_transparent(image):
    """
    Check to see if an image is transparent.
    """
    if not isinstance(image, PIL.Image.Image):
        # Can only deal with PIL images, fall back to the assumption that that
        # it's not transparent.
        return False
    return (image.mode in ('RGBA', 'LA') or
            (image.mode == 'P' and 'transparency' in image.info))


def exif_orientation(im):
    """
    Rotate and/or flip an image to respect the image's EXIF orientation data.
    """
    try:
        exif = im._getexif()
    except (AttributeError, IndexError, KeyError, IOError):
        exif = None
    if exif:
        orientation = exif.get(0x0112)
        if orientation == 2:
            im = im.transpose(PIL.Image.FLIP_LEFT_RIGHT)
        elif orientation == 3:
            im = im.rotate(180)
        elif orientation == 4:
            im = im.transpose(PIL.Image.FLIP_TOP_BOTTOM)
        elif orientation == 5:
            im = im.rotate(-90).transpose(PIL.Image.FLIP_LEFT_RIGHT)
        elif orientation == 6:
            im = im.rotate(-90)
        elif orientation == 7:
            im = im.rotate(90).transpose(PIL.Image.FLIP_LEFT_RIGHT)
        elif orientation == 8:
            im = im.rotate(90)
    return im


def correct_colorspace(im, bw=False):
    """
    Convert images to the correct color space.
    bw
        Make the thumbnail grayscale (not really just black & white).
    """
    if bw:
        if im.mode in ('L', 'LA'):
            return im
        if is_transparent(im):
            return im.convert('LA')
        else:
            return im.convert('L')

    if im.mode in ('L', 'RGB'):
        return im

    return im.convert('RGB')


def is_animated_gif(im):
    info = getattr(im, 'info', None) or {}
    return bool((im.format == 'GIF' or not im.format) and info.get('extension'))


def has_animated_gif_support():
    return bool(CROPDUSTER_GIFSICLE_PATH)


def process_image(im, save_filename=None, callback=lambda i: i, nq=0, save_params=None):
    is_animated = is_animated_gif(im)
    images = [im]

    if is_animated:
        if not CROPDUSTER_GIFSICLE_PATH:
            warnings.warn(
                u"This server does not have animated gif support; your uploaded image "
                u"has been made static.")
        else:
            images = [GifsicleImage(im)]

    new_images = [callback(i) for i in images]

    if is_animated and not save_filename:
        raise Exception("Animated gifs must be saved on each processing.")

    if save_filename:
        save_params = save_params or {}
        if im.format == 'JPEG':
            save_params.setdefault('quality', get_jpeg_quality(new_images[0].size[0], new_images[0].size[1]))
        if im.format in ('JPEG', 'PNG') and JPEG_SAVE_ICC_SUPPORTED:
            save_params.setdefault('icc_profile', im.info.get('icc_profile'))
        img = new_images[0]
        buf = BytesIO()
        img.save(buf, format=im.format, **save_params)
        with default_storage.open(save_filename, 'wb') as f:
            f.write(buf.getvalue())
        with default_storage.open(save_filename, mode='rb') as f:
            content = f.read()
            pil_image = PIL.Image.open(BytesIO(content))
        pil_image.filename = save_filename
        return pil_image

    return new_images[0]


def smart_resize(im, final_w, final_h):
    """
    Resizes a given image in multiple steps to ensure maximum quality and performance
    :param im: PIL.Image instance the image to be resized
    :param final_w: int the intended final width of the image
    :param final_h: int the intended final height of the image
    """

    (orig_w, orig_h) = im.size
    if orig_w <= final_w and orig_h <= final_h:
        # If the image is already the right size, don't change it
        return im

    # Pillow 2.7.0 greatly improved the bicubic resize algorithm, which makes
    # our multiple-step resizing unnecessary
    pillow_version = getattr(PIL, '__version__', None)
    if pillow_version and LooseVersion(pillow_version) >= LooseVersion('2.7.0'):
        return im.resize((final_w, final_h), PIL.Image.BICUBIC)

    # Attempt to resize the image 1/8, 2/8, such that it is at least 1.5x bigger
    # than the final size
    # (Libjpg-Turbo has optimizations for resizing images by a ratio of eights)
    (goal_w, goal_h) = (final_w * 1.5, final_h * 1.5)
    # Ratios from 1/8, 2/8... 7/8
    for i in xrange(1, 8):
        ratio = i / 8
        scaled_w = orig_w * ratio
        scaled_h = orig_h * ratio
        if scaled_w >= goal_w and scaled_h >= goal_h:

            # The image may need to be cropped slightly to ensure an even
            # size reduction
            crop_w = orig_w % 8
            crop_h = orig_h % 8
            if not crop_w or not crop_h:
                im.crop((math.floor(crop_w / 2),
                         math.floor(crop_h / 2),
                         orig_w - math.ceil(crop_w / 2),
                         orig_h - math.ceil(crop_h / 2)))
                (orig_w, orig_h) = im.size

            # Resize part of the way using the fastest algorithm
            im = im.resize((int(orig_w * ratio), int(orig_w * ratio)),
                           PIL.Image.NEAREST)
            break

    # Return the image with the final resizing done at best quality
    return im.resize((final_w, final_h), PIL.Image.ANTIALIAS)
  20  
cropduster/utils/jsonutils.py
@@ -1,9 +1,15 @@
from jsonutil import jsonutil	import json
from django.utils import six
from django.utils.six.moves import filter

from cropduster.resizing import Size	from cropduster.resizing import Size




__all__ = ('dumps', 'loads')


def json_default(obj):	def json_default(obj):
    if callable(getattr(obj, '__serialize__', None)):	    if six.callable(getattr(obj, '__serialize__', None)):
        dct = obj.__serialize__()	        dct = obj.__serialize__()
        module = obj.__module__	        module = obj.__module__
        if module == '__builtin__':	        if module == '__builtin__':
@@ -24,22 +30,26 @@ def object_hook(dct):
    if dct.get('__type__') in ['Size', 'cropduster.resizing.Size']:	    if dct.get('__type__') in ['Size', 'cropduster.resizing.Size']:
        return Size(	        return Size(
            name=dct.get('name'),	            name=dct.get('name'),
            label=dct.get('label'),
            w=dct.get('w'),	            w=dct.get('w'),
            h=dct.get('h'),	            h=dct.get('h'),
            min_w=dct.get('min_w'),	            min_w=dct.get('min_w'),
            min_h=dct.get('min_h'),	            min_h=dct.get('min_h'),
            max_w=dct.get('max_w'),	            max_w=dct.get('max_w'),
            max_h=dct.get('max_h'),	            max_h=dct.get('max_h'),
            retina=dct.get('retina'),	            retina=dct.get('retina'),
            auto=dct.get('auto'))	            auto=dct.get('auto'),
            required=dct.get('required'))
    return dct	    return dct




def dumps(obj, *args, **kwargs):	def dumps(obj, *args, **kwargs):
    kwargs.setdefault('default', json_default)	    kwargs.setdefault('default', json_default)
    return jsonutil.dumps(obj, *args, **kwargs)	    return json.dumps(obj, *args, **kwargs)




def loads(s, *args, **kwargs):	def loads(s, *args, **kwargs):
    if isinstance(s, six.binary_type):
        s = s.decode('utf-8')
    kwargs.setdefault('object_hook', object_hook)	    kwargs.setdefault('object_hook', object_hook)
    return jsonutil.loads(s, *args, **kwargs)	    return json.loads(s, *args, **kwargs)
  56  
cropduster/utils/paths.py
@@ -1,19 +1,15 @@
from __future__ import unicode_literals

import os	import os
import re	import re


from django.core.files.storage import default_storage, FileSystemStorage
from django.conf import settings	from django.conf import settings
from django.db.models.fields.files import FileField	from django.db.models.fields.files import FileField
from django.utils import six




__all__ = ('get_upload_foldername', 'get_media_path', 'get_relative_media_url')	__all__ = ('get_upload_foldername')


MEDIA_ROOT = os.path.abspath(settings.MEDIA_ROOT)	

re_media_root = re.compile(r'^%s' % re.escape(MEDIA_ROOT))	
re_media_url = re.compile(r'^%s' % re.escape(settings.MEDIA_URL))	
re_url_slashes = re.compile(r'(?:\A|(?<=/))/')	
re_path_slashes = re.compile(r'(?<=/)/')	




def get_upload_foldername(file_name, upload_to='%Y/%m'):	def get_upload_foldername(file_name, upload_to='%Y/%m'):
@@ -23,28 +19,24 @@ def get_upload_foldername(file_name, upload_to='%Y/%m'):
        file_name = 'no_name'	        file_name = 'no_name'
    filename = file_field.generate_filename(None, file_name)	    filename = file_field.generate_filename(None, file_name)
    filename = re.sub(r'[_\-]+', '_', filename)	    filename = re.sub(r'[_\-]+', '_', filename)

    if six.PY2 and isinstance(filename, unicode):
        filename = filename.encode('utf-8')

    root_dir = os.path.splitext(filename)[0]	    root_dir = os.path.splitext(filename)[0]
    root_dir = dir_name = os.path.join(settings.MEDIA_ROOT, root_dir)	    parent_dir, _, basename = root_dir.rpartition('/')
    image_dir = ''
    i = 1	    i = 1
    while os.path.exists(dir_name):	    dir_name = basename
        dir_name = u'%s-%d' % (root_dir, i)	    while not image_dir:
        i += 1	        try:
    os.makedirs(dir_name)	            sub_dirs, _ = default_storage.listdir(parent_dir)
    return dir_name	            while dir_name in sub_dirs:

                dir_name = "%s-%d" % (basename, i)

                i += 1
def get_media_path(url):	        except OSError:
    """Determine media URL's system file."""	            os.makedirs(os.path.join(settings.MEDIA_ROOT, parent_dir))
    path = MEDIA_ROOT + '/' + re_media_url.sub('', url)	        else:
    return re_path_slashes.sub('', path)	            image_dir = os.path.join(parent_dir, dir_name)



    return image_dir
def get_relative_media_url(path, clean_slashes=True):	
    """Determine system file's media URL without MEDIA_URL prepended."""	
    if path.startswith(settings.MEDIA_URL):	
        url = re_media_url.sub('', path)	
    else:	
        url = re_media_root.sub('', path)	
    if clean_slashes:	
        url = re_url_slashes.sub('', url)	
    return url	
  11  
cropduster/utils/sizes.py
@@ -1,5 +1,7 @@
from __future__ import division	from __future__ import division


from django.utils import six

from . import jsonutils as json	from . import jsonutils as json
from ..resizing import Size	from ..resizing import Size


@@ -10,14 +12,15 @@
def get_min_size(sizes):	def get_min_size(sizes):
    """Determine the minimum required width & height from a list of sizes."""	    """Determine the minimum required width & height from a list of sizes."""
    min_w, min_h = 0, 0	    min_w, min_h = 0, 0
    if sizes == u'null':	    if sizes == 'null':
        return (0, 0)	        return (0, 0)
    if isinstance(sizes, basestring):	    if isinstance(sizes, six.string_types):
        sizes = json.loads(sizes)	        sizes = json.loads(sizes)
    if not sizes:	    if not sizes:
        return (0, 0)	        return (0, 0)
    # The min width and height for the image = the largest w / h of the sizes	    # The min width and height for the image = the largest w / h of the sizes
    for size in Size.flatten(sizes):	    for size in Size.flatten(sizes):
        min_w = max(size.min_w, min_w)	        if size.required:
        min_h = max(size.min_h, min_h)	            min_w = max(size.min_w, min_w)
            min_h = max(size.min_h, min_h)
    return (min_w, min_h)	    return (min_w, min_h)
 60  
cropduster/utils/thumbs.py
@@ -0,0 +1,60 @@
from ..resizing import Crop
from ..exceptions import CropDusterException


class DummyImage(object):
    def __init__(self, image):
        self.size = [image.width, image.height]


def set_as_auto_crop(thumb, reference_thumb, force=False):
    """
    Sometimes you need to move crop sizes into different crop groups. This
    utility takes a Thumb and a new reference thumb that will become its
    parent.
    This function can be destructive so, by default, it does not re-set the
    parent crop if the new crop box is different than the old crop box.
    """
    dummy_image = DummyImage(thumb.image)
    current_best_fit = Crop(thumb.get_crop_box(), dummy_image).best_fit(thumb.width, thumb.height)
    new_best_fit = Crop(reference_thumb.get_crop_box(), dummy_image).best_fit(thumb.width, thumb.height)

    if current_best_fit.box != new_best_fit.box and not force:
        raise CropDusterException("Current image crop based on '%s' is "
            "different than new image crop based on '%s'." % (thumb.reference_thumb.name, reference_thumb.name))

    if reference_thumb.reference_thumb:
        raise CropDusterException("Reference thumbs cannot have reference thumbs.")

    if not thumb.reference_thumb:
        thumb.crop_w = None
        thumb.crop_h = None
        thumb.crop_x = None
        thumb.crop_y = None
    thumb.reference_thumb = reference_thumb
    thumb.save()


def unset_as_auto_crop(thumb):
    """
    Crop information is normalized on the parent Thumb row so auto-crops do not
    have crop height/width/x/y associated with them.
    This function takes a Thumb as an argument, generates the best_fit from
    its reference_thumb, sets the relevant geometry, and clears the original
    reference_thumb foreign key.
    """
    if not thumb.reference_thumb:
        return

    reference_thumb_box = thumb.reference_thumb.get_crop_box()
    crop = Crop(reference_thumb_box, DummyImage(thumb.image))
    best_fit = crop.best_fit(thumb.width, thumb.height)

    thumb.reference_thumb = None
    thumb.crop_w = best_fit.box.w
    thumb.crop_h = best_fit.box.h
    thumb.crop_x = best_fit.box.x1
    thumb.crop_y = best_fit.box.y1
    thumb.save()
 189  
cropduster/views/__init__.py
@@ -1,27 +1,65 @@
"""
View functions used by the cropduster dialog.
index() (defined in CropDusterIndex)
====================================
The initial page that a user sees when clicking on the "Upload Image" button.
This view renders the form used to interact with upload() and crop() via ajax.
standalone() (defined in CropDusterStandalone)
==============================================
Subclass of CropDusterIndex used for "standalone mode", which saves minimal
information in the database and instead stores information about the original
image and crop dimensions in metadata on the generated image. The intended use
case for standalone mode is a dialog in a WYSIWYG editor.
upload() / crop()
=================
Both upload() and crop() interact with the index page's html in the same way:
they receive a POST with data from the django forms and formsets, create new
image and thumb instances (respectively), and return a JSON object that map
back onto fields on the index page's forms / formsets.
"""
from __future__ import division	from __future__ import division


from io import BytesIO
import os	import os
import copy	import copy
import shutil	import shutil
import time


import django
from django.conf import settings	from django.conf import settings
from django.contrib.auth.decorators import login_required
from django.contrib.contenttypes.models import ContentType	from django.contrib.contenttypes.models import ContentType
from django.core.files.storage import default_storage
from django.db.models import Q	from django.db.models import Q
from django.forms.models import modelformset_factory	from django.forms.models import modelformset_factory
from django.http import HttpResponse	from django.http import HttpResponse
from django.shortcuts import render_to_response	from django.shortcuts import render
from django.template import RequestContext	from django.template import RequestContext
from django.utils.decorators import method_decorator
from django.utils.encoding import force_text
from django.utils.functional import cached_property	from django.utils.functional import cached_property
from django.utils import six
from django.utils.six.moves import filter, map, zip
from django.views.decorators.csrf import csrf_exempt	from django.views.decorators.csrf import csrf_exempt


import PIL.Image	import PIL.Image


from generic_plus.utils import get_relative_media_url

from cropduster.files import ImageFile	from cropduster.files import ImageFile
from cropduster.models import Thumb, Size, StandaloneImage, Image	from cropduster.models import Thumb, Size, StandaloneImage, Image
from cropduster.settings import (	from cropduster.settings import (
    CROPDUSTER_PREVIEW_WIDTH as PREVIEW_WIDTH,	    CROPDUSTER_PREVIEW_WIDTH as PREVIEW_WIDTH,
    CROPDUSTER_PREVIEW_HEIGHT as PREVIEW_HEIGHT)	    CROPDUSTER_PREVIEW_HEIGHT as PREVIEW_HEIGHT)
from cropduster.utils import json, get_relative_media_url	from cropduster.utils import (
    json, is_animated_gif, has_animated_gif_support, process_image)
from cropduster.exceptions import json_error, CropDusterResizeException, full_exc_info	from cropduster.exceptions import json_error, CropDusterResizeException, full_exc_info


from .base import View	from .base import View
@@ -35,6 +73,7 @@ class CropDusterIndex(View):


    is_standalone = False	    is_standalone = False


    @method_decorator(login_required)
    def dispatch(self, request, *args, **kwargs):	    def dispatch(self, request, *args, **kwargs):
        self.request = request	        self.request = request
        self.upload_to = self.request.GET.get('upload_to') or None	        self.upload_to = self.request.GET.get('upload_to') or None
@@ -94,7 +133,8 @@ def thumbs(self):
        else:	        else:
            thumbs = Thumb.objects.filter(pk__in=thumb_ids)	            thumbs = Thumb.objects.filter(pk__in=thumb_ids)
        thumb_dict = dict([(t.name, t) for t in thumbs])	        thumb_dict = dict([(t.name, t) for t in thumbs])
        ordered_thumbs = [thumb_dict.get(s.name, Thumb(name=s.name)) for s in self.sizes]	        ordered_thumbs = [
            thumb_dict.get(s.name, Thumb(name=s.name)) for s in self.sizes if not s.is_alias]
        return FakeQuerySet(ordered_thumbs, thumbs)	        return FakeQuerySet(ordered_thumbs, thumbs)


    @cached_property	    @cached_property
@@ -106,17 +146,23 @@ def orig_image(self):


    def get(self, *args, **kwargs):	    def get(self, *args, **kwargs):
        orig_image = self.orig_image	        orig_image = self.orig_image
        orig_w = getattr(orig_image, 'width', None) or 0	        try:
        orig_h = getattr(orig_image, 'height', None) or 0	            orig_w = getattr(orig_image, 'width', None) or 0
            orig_h = getattr(orig_image, 'height', None) or 0
            orig_image_name = getattr(orig_image, 'name', None)
        except Exception:
            # If original image not found, allow it to be re-uploaded
            orig_w, orig_h = 0, 0
            orig_image_name = None


        initial = {	        initial = {
            'standalone': self.is_standalone,	            'standalone': self.is_standalone,
            'sizes': json.dumps(self.sizes),	            'sizes': json.dumps(self.sizes),
            'thumbs': json.dumps(dict([	            'thumbs': json.dumps(dict([
                (t['name'], t)	                (t['name'], t)
                for t in self.thumbs.queryset.values('id', 'name', 'width', 'height')])),	                for t in self.thumbs.queryset.values('id', 'name', 'width', 'height')])),
            'image_id': getattr(self.db_image, 'pk', None),	            'image_id': getattr(self.db_image, 'pk', None) if orig_image else None,
            'orig_image': getattr(orig_image, 'name', None),	            'orig_image': orig_image_name,
            'orig_w': orig_w,	            'orig_w': orig_w,
            'orig_h': orig_h,	            'orig_h': orig_h,
        }	        }
@@ -139,7 +185,8 @@ def get(self, *args, **kwargs):
                'changed': False,	                'changed': False,
            })	            })


        return render_to_response('cropduster/upload.html', RequestContext(self.request, {	        return render(self.request, 'cropduster/upload.html', {
            'django_is_gte_19': (django.VERSION[:2] >= (1, 9)),
            'is_popup': True,	            'is_popup': True,
            'orig_image': '',	            'orig_image': '',
            'parent_template': get_admin_base_template(),	            'parent_template': get_admin_base_template(),
@@ -155,69 +202,86 @@ def get(self, *args, **kwargs):
            }),	            }),
            'crop_form': CropForm(initial=initial, prefix='crop'),	            'crop_form': CropForm(initial=initial, prefix='crop'),
            'thumb_formset': thumb_formset,	            'thumb_formset': thumb_formset,
        }))	        })






index = CropDusterIndex.as_view()	index = CropDusterIndex.as_view()




@csrf_exempt	@csrf_exempt
@login_required
def upload(request):	def upload(request):
    if request.method == 'GET':	    if request.method == 'GET':
        return index(request)	        return index(request)


    # The data we'll be returning as JSON
    data = {
        'warning': [],
    }

    form = UploadForm(request.POST, request.FILES)	    form = UploadForm(request.POST, request.FILES)


    if not form.is_valid():	    if not form.is_valid():
        errors = form['image'].errors or form.errors	        errors = form['image'].errors or form.errors
        return json_error(request, 'upload', action="uploading file",	        return json_error(request, 'upload', action="uploading file",
                errors=[unicode(errors)])	                errors=[force_text(errors)])


    form_data = form.cleaned_data	    form_data = form.cleaned_data
    is_standalone = bool(form_data.get('standalone'))


    orig_file_path = form_data['image'].name	    orig_file_path = form_data['image'].name
    if six.PY2 and isinstance(orig_file_path, six.text_type):
        orig_file_path = orig_file_path.encode('utf-8')
    orig_image = get_relative_media_url(orig_file_path)	    orig_image = get_relative_media_url(orig_file_path)
    img = PIL.Image.open(orig_file_path)	
    with default_storage.open(orig_image, mode='rb') as f:
        img = PIL.Image.open(BytesIO(f.read()))
        img.filename = f.name

    (w, h) = (orig_w, orig_h) = img.size	    (w, h) = (orig_w, orig_h) = img.size


    if is_animated_gif(img) and not has_animated_gif_support():
        data['warning'].append(
            u"This server does not have animated gif support; your uploaded image "
            u"has been made static.")

    tmp_image = Image(image=orig_image)	    tmp_image = Image(image=orig_image)
    preview_w = form_data.get('preview_width') or PREVIEW_WIDTH	    preview_w = form_data.get('preview_width') or PREVIEW_WIDTH
    preview_h = form_data.get('preview_height') or PREVIEW_HEIGHT	    preview_h = form_data.get('preview_height') or PREVIEW_HEIGHT


    # First pass resize if it's too large	    # First pass resize if it's too large
    resize_ratio = min(preview_w / w, preview_h / h)	    resize_ratio = min(preview_w / w, preview_h / h)
    if resize_ratio < 1:	
        w = int(round(w * resize_ratio))	
        h = int(round(h * resize_ratio))	
        preview_img = img.resize((w, h), PIL.Image.ANTIALIAS)	
    else:	
        preview_img = img	


    preview_file_path = tmp_image.get_image_path('_preview')	    def fit_preview(im):

        (w, h) = im.size
    img_save_params = {}	        if resize_ratio < 1:
    if preview_img.format == 'JPEG':	            w = int(round(w * resize_ratio))
        img_save_params['quality'] = 95	            h = int(round(h * resize_ratio))
            preview_img = im.resize((w, h), PIL.Image.ANTIALIAS)
        else:
            preview_img = im
        return preview_img


    preview_img.save(preview_file_path, **img_save_params)	    if not is_standalone:
        preview_file_path = tmp_image.get_image_path('_preview')
        process_image(img, preview_file_path, fit_preview)


    data = {	    data.update({
        'crop': {	        'crop': {
            'orig_image': orig_image,	            'orig_image': orig_image,
            'orig_w': orig_w,	            'orig_w': orig_w,
            'orig_h': orig_h,	            'orig_h': orig_h,
            'image_id': None,
        },	        },
        'url': tmp_image.get_image_url('_preview'),	        'url': tmp_image.get_image_url('_preview'),
        'orig_image': orig_image,	        'orig_image': orig_image,
        'orig_w': orig_w,	        'orig_w': orig_w,
        'orig_h': orig_h,	        'orig_h': orig_h,
        'width': w,	        'width': w,
        'height': h,	        'height': h,
    }	    })
    if not form_data.get('standalone'):	    if not is_standalone:
        return HttpResponse(json.dumps(data), mimetype='application/json')	        return HttpResponse(json.dumps(data), content_type='application/json')


    size = Size('crop', w=img.size[0], h=img.size[1])	    size = Size('crop', w=img.size[0], h=img.size[1])


@@ -233,7 +297,20 @@ def upload(request):


    if not cropduster_image.image:	    if not cropduster_image.image:
        cropduster_image.image = orig_image	        cropduster_image.image = orig_image
    thumb = cropduster_image.save_size(size, standalone=True)	        cropduster_image.save()
    elif cropduster_image.image.name != orig_image:
        data['crop']['orig_image'] = data['orig_image'] = cropduster_image.image.name
        data['url'] = cropduster_image.get_image_url('_preview')

    with cropduster_image.image as f:
        f.open()
        img = PIL.Image.open(BytesIO(f.read()))
        img.filename = f.name
    preview_file_path = cropduster_image.get_image_path('_preview')
    if not default_storage.exists(preview_file_path):
        process_image(img, preview_file_path, fit_preview)

    thumb = cropduster_image.save_size(size, standalone=True, commit=False)


    sizes = form_data.get('sizes') or []	    sizes = form_data.get('sizes') or []
    if len(sizes) == 1:	    if len(sizes) == 1:
@@ -259,10 +336,11 @@ def upload(request):
        'image_id': cropduster_image.pk,	        'image_id': cropduster_image.pk,
        'sizes': json.dumps([size]),	        'sizes': json.dumps([size]),
    })	    })
    return HttpResponse(json.dumps(data), mimetype='application/json')	    return HttpResponse(json.dumps(data), content_type='application/json')




@csrf_exempt	@csrf_exempt
@login_required
def crop(request):	def crop(request):
    if request.method == "GET":	    if request.method == "GET":
        return json_error(request, 'crop', action="cropping image",	        return json_error(request, 'crop', action="cropping image",
@@ -274,9 +352,17 @@ def crop(request):
                log=True, exc_info=full_exc_info())	                log=True, exc_info=full_exc_info())


    crop_data = copy.deepcopy(crop_form.cleaned_data)	    crop_data = copy.deepcopy(crop_form.cleaned_data)
    db_image = Image(image=crop_data['orig_image'])	
    if crop_data.get('image_id'):
        db_image = Image.objects.get(pk=crop_data['image_id'])
    else:
        db_image = Image(image=crop_data['orig_image'])

    try:	    try:
        pil_image = PIL.Image.open(db_image.image.path)	        with db_image.image as f:
            f.open()
            pil_image = PIL.Image.open(BytesIO(f.read()))
            pil_image.filename = f.name
    except IOError:	    except IOError:
        pil_image = None	        pil_image = None


@@ -299,6 +385,13 @@ def crop(request):


    standalone_mode = crop_data['standalone']	    standalone_mode = crop_data['standalone']


    # Address a standalone mode issue where, because the thumbs don't have a pk value,
    # Django no longer returns them in Formset.save() if they are in initial_forms
    if standalone_mode and not cropped_thumbs and len(thumb_formset.initial_forms):
        thumb_form = thumb_formset.initial_forms[0]
        obj = thumb_form.instance
        cropped_thumbs = [thumb_formset.save_existing(thumb_form, obj, commit=False)]

    for i, (thumb, thumb_form) in enumerate(zip(cropped_thumbs, thumb_formset)):	    for i, (thumb, thumb_form) in enumerate(zip(cropped_thumbs, thumb_formset)):
        changed_fields = set(thumb_form.changed_data) - non_model_fields	        changed_fields = set(thumb_form.changed_data) - non_model_fields
        thumb_form._changed_data = list(changed_fields)	        thumb_form._changed_data = list(changed_fields)
@@ -316,7 +409,7 @@ def crop(request):
                new_thumbs = db_image.save_size(size, thumb, tmp=True, standalone=standalone_mode)	                new_thumbs = db_image.save_size(size, thumb, tmp=True, standalone=standalone_mode)
            except CropDusterResizeException as e:	            except CropDusterResizeException as e:
                return json_error(request, 'crop',	                return json_error(request, 'crop',
                                  action="saving size", errors=[unicode(e)])	                                  action="saving size", errors=[force_text(e)])


            if not new_thumbs:	            if not new_thumbs:
                continue	                continue
@@ -336,18 +429,22 @@ def crop(request):
                'url': db_image.get_image_url(thumb.name),	                'url': db_image.get_image_url(thumb.name),
            })	            })


            for name, new_thumb in new_thumbs.iteritems():	            for name, new_thumb in six.iteritems(new_thumbs):
                thumb_data = dict([(k, getattr(new_thumb, k)) for k in json_thumb_fields])	                thumb_data = dict([(k, getattr(new_thumb, k)) for k in json_thumb_fields])
                thumb_data['url'] = db_image.get_image_url(name, tmp=not(new_thumb.image_id))
                crop_data['thumbs'].update({name: thumb_data})	                crop_data['thumbs'].update({name: thumb_data})
                if new_thumb.reference_thumb_id:	                if new_thumb.reference_thumb_id:
                    continue	                    continue
                thumbs_data[i]['thumbs'].update({name: thumb_data})	                thumbs_data[i]['thumbs'].update({name: thumb_data})
        elif thumb.pk and thumb.name and thumb.crop_w and thumb.crop_h:	        elif thumb.pk and thumb.name and thumb.crop_w and thumb.crop_h:
            thumb_path = db_image.get_image_path(thumb.name, tmp=False)	            thumb_path = db_image.get_image_path(thumb.name, tmp=False)
            tmp_thumb_path = db_image.get_image_path(thumb.name, tmp=True)	            tmp_thumb_path = db_image.get_image_path(thumb.name, tmp=True)
            if os.path.exists(thumb_path):	
                if not thumb_form.cleaned_data.get('changed') or not os.path.exists(tmp_thumb_path):	            if default_storage.exists(thumb_path):
                    shutil.copy(thumb_path, tmp_thumb_path)	                if not thumb_form.cleaned_data.get('changed') or not default_storage.exists(tmp_thumb_path):
                    with default_storage.open(thumb_path) as f:
                        with default_storage.open(tmp_thumb_path, 'wb') as tmp_file:
                            tmp_file.write(f.read())


        if not thumb.pk and not thumb.crop_w and not thumb.crop_h:	        if not thumb.pk and not thumb.crop_w and not thumb.crop_h:
            if not len(thumbs_with_crops):	            if not len(thumbs_with_crops):
@@ -361,14 +458,28 @@ def crop(request):
                    'crop_w': best_fit.box.w,	                    'crop_w': best_fit.box.w,
                    'crop_h': best_fit.box.h,	                    'crop_h': best_fit.box.h,
                    'changed': True,	                    'changed': True,
                    'id': None,
                })	                })


    for thumb_data in thumbs_data:	    for thumb_data in thumbs_data:
        if isinstance(thumb_data['id'], Thumb):	        if isinstance(thumb_data['id'], Thumb):
            thumb_data['id'] = thumb_data['id'].pk	            thumb_data['id'] = thumb_data['id'].pk


    preview_url = db_image.get_image_url('_preview')
    preview_w = PREVIEW_WIDTH
    preview_h = PREVIEW_HEIGHT
    orig_width, orig_height = crop_data['orig_w'], crop_data['orig_h']
    if (orig_width and orig_height):
        resize_ratio = min(PREVIEW_WIDTH / float(orig_width), PREVIEW_HEIGHT / float(orig_height))
        if resize_ratio < 1:
            preview_w = int(round(orig_width * resize_ratio))
            preview_h = int(round(orig_height * resize_ratio))

    return HttpResponse(json.dumps({	    return HttpResponse(json.dumps({
        'crop': crop_data,	        'crop': crop_data,
        'thumbs': thumbs_data,	        'thumbs': thumbs_data,
        'initial': True,	        'initial': True,
    }), mimetype='application/json')	        'preview_url': preview_url,
        'preview_w': preview_w,
        'preview_h': preview_h
    }), content_type='application/json')
 8  
cropduster/views/base.py
 68  
cropduster/views/forms.py
 18  
cropduster/views/utils.py
 210  
cropduster/widgets.py
This file was deleted.

 2  
cropduster3/__init__.py
This file was deleted.

 29  
cropduster3/admin.py
This file was deleted.

 28  
cropduster3/media/css/CropDuster.css
This file was deleted.

 BIN  
cropduster3/media/css/Jcrop.gif
Binary file not shown.
 60  
cropduster3/media/css/admin.cropduster.css
This file was deleted.

 BIN  
cropduster3/media/css/blank.gif
Binary file not shown.
 86  
cropduster3/media/css/jquery.Jcrop.css
This file was deleted.

 28  
cropduster3/media/css/jquery.Jcrop.min.css
This file was deleted.

 BIN  
cropduster3/media/img/blank.gif
Binary file not shown.
 BIN  
cropduster3/media/img/cropduster_icon_upload_hover.png
Binary file not shown.
 BIN  
cropduster3/media/img/cropduster_icon_upload_select.png
Binary file not shown.
 BIN  
cropduster3/media/img/cropduster_icon_upload_select_small.png
Binary file not shown.
 BIN  
cropduster3/media/img/progressbar.gif
Binary file not shown.
 183  
cropduster3/media/js/CropDuster.js
This file was deleted.

 102  
cropduster3/media/js/admin.cropduster.js
This file was deleted.

 13  
cropduster3/media/js/init.js
This file was deleted.

 4  
cropduster3/media/js/jquery-1.7.2.min.js
This file was deleted.

 1,695  
cropduster3/media/js/jquery.Jcrop.js
This file was deleted.

 22  
cropduster3/media/js/jquery.Jcrop.min.js
This file was deleted.

 60  
cropduster3/media/js/jquery.class.js
This file was deleted.

 123  
cropduster3/media/js/jquery.color.js
This file was deleted.

 925  
cropduster3/media/js/jquery.form.js
This file was deleted.

 4  
cropduster3/media/js/jquery.min.js
This file was deleted.

 108  
cropduster3/media/js/jquery.progressbar.js
This file was deleted.

 20  
cropduster3/media/js/jquery.progressbar.min.js
This file was deleted.

 483  
cropduster3/media/js/json2.js
This file was deleted.

 1,036  
cropduster3/media/js/jsrender.js
This file was deleted.

 164  
cropduster3/media/js/upload.js
This file was deleted.

 809  
cropduster3/models.py
This file was deleted.

 20  
cropduster3/settings.py
This file was deleted.

 71  
cropduster3/templates/admin/complete.html
This file was deleted.

 203  
cropduster3/templates/admin/crop_images.html
This file was deleted.

 45  
cropduster3/templates/admin/inline.html
This file was deleted.

 103  
cropduster3/templates/admin/inline_tabular.html
This file was deleted.

 143  
cropduster3/templates/admin/upload.html
This file was deleted.

 50  
cropduster3/templates/admin/upload_image.html
This file was deleted.

 11  
cropduster3/templates/templatetags/html4.html
This file was deleted.

 11  
cropduster3/templates/templatetags/image.html
This file was deleted.

 54  
cropduster3/templatetags/cropdusteradmin.py
This file was deleted.

 30  
cropduster3/templatetags/cropdusterimages.py
This file was deleted.

 15  
cropduster3/templatetags/cropdustermedia.py
This file was deleted.

 9  
cropduster3/urls.py
This file was deleted.

 166  
cropduster3/utils.py
This file was deleted.

 362  
cropduster3/views.py
This file was deleted.

 93  
cropduster3/widgets.py
This file was deleted.

 192  
docs/Makefile
 5  
docs/changelog.rst
 296  
docs/conf.py
 16  
docs/customization.rst
 67  
docs/how_it_works.rst
 39  
docs/index.rst
 112  
docs/quickstart.rst
 6  
pytest.ini
@@ -0,0 +1,6 @@
[pytest]
DJANGO_SETTINGS_MODULE = tests.settings
addopts = --tb=short --create-db --cov=cropduster
django_find_project = false
python_files = tests.py test_*.py *_tests.py
testpaths = tests
 11  
setup.cfg
@@ -0,0 +1,11 @@
[bumpversion]
current_version = 4.13.0
commit = True
tag = True
message = v{new_version} [ci skip]

[bdist_wheel]
universal = 1

[bumpversion:file:setup.py]

 31  
setup.py
 100644 ??? 100755
@@ -12,23 +12,32 @@
    name='django-cropduster',	    name='django-cropduster',
    version=__import__('cropduster').__version__,	    version=__import__('cropduster').__version__,
    author='The Atlantic',	    author='The Atlantic',
    author_email='atmoprogrammers@theatlantic.com',	    author_email='programmers@theatlantic.com',
    url='http://github.com/theatlantic/django-cropduster',	    url='https://github.com/theatlantic/django-cropduster',
    description='Image uploader and cropping tool',	    description='Django image uploader and cropping tool',
    packages=find_packages(),	    packages=find_packages(exclude=["tests"]),
    zip_safe=False,	    zip_safe=False,
    long_description=open('README.rst').read(),
    license='BSD',
    platforms='any',
    install_requires=[	    install_requires=[
        'Pillow',	        'Pillow',
        'jsonutil',	
        'Django>=1.2',	
        'python-xmp-toolkit',	        'python-xmp-toolkit',
        'django-generic-plus>=2.0.3',
    ],	    ],
    include_package_data=True,	    include_package_data=True,
    classifiers=[	    classifiers=[
        'Framework :: Django',	        'Development Status :: 5 - Production/Stable',
        'Environment :: Web Environment',
        'Intended Audience :: Developers',	        'Intended Audience :: Developers',
        'Intended Audience :: System Administrators',	        'Natural Language :: English',
        'Operating System :: OS Independent',	        'Operating System :: OS Independent',
        'Topic :: Software Development'	        'Framework :: Django',
    ],	        'Programming Language :: Python',
)	        "Programming Language :: Python :: 2",
        'Programming Language :: Python :: 2.7',
        'Programming Language :: Python :: 3',
        'Programming Language :: Python :: 3.4',
        'Programming Language :: Python :: 3.5',
        'Programming Language :: Python :: 3.6',
    ])
 0  
cropduster/templates/cropduster/blank.html ??? tests/__init__.py
File renamed without changes.
 8  
tests/admin.py
@@ -0,0 +1,8 @@
from django.contrib import admin
from .models import Author, Article, OptionalSizes, OrphanedThumbs


admin.site.register(Author)
admin.site.register(Article)
admin.site.register(OptionalSizes)
admin.site.register(OrphanedThumbs)
 16  
tests/conftest.py
@@ -0,0 +1,16 @@
import warnings

import pytest
from django.test import TestCase


TestCase.pytestmark = pytest.mark.django_db(transaction=True, reset_sequences=True)


@pytest.fixture(autouse=True)
def suppress_warnings():
    warnings.simplefilter("error", Warning)
    warnings.filterwarnings('ignore', message='.*?ckeditor')
    warnings.filterwarnings('ignore', message='.*?collections')
    warnings.filterwarnings('ignore', message='.*?Resampling')
    warnings.filterwarnings('ignore', message='.*?distutils')
 BIN  
tests/data/animated-duration.gif

 BIN  
tests/data/animated.gif

 BIN  
tests/data/best-fit-off-by-one-bug.png

 BIN  
tests/data/cmyk.jpg

 BIN  
tests/data/img.jpg

 BIN  
tests/data/img.png

 BIN  
tests/data/img2.jpg

 BIN  
tests/data/size-order-bug.png

 BIN  
tests/data/transparent.png

 86  
tests/helpers.py
@@ -0,0 +1,86 @@
from io import open
import tempfile
import os
import shutil
import uuid

import PIL.Image

from django.core.files.storage import default_storage
from django.core.files.base import ContentFile
from django.test import override_settings

from .utils import repr_rgb


PATH = os.path.split(__file__)[0]
ORIG_IMG_PATH = os.path.join(PATH, 'data')


class CropdusterTestCaseMediaMixin(object):

    def _pre_setup(self):
        super(CropdusterTestCaseMediaMixin, self)._pre_setup()
        self.temp_media_root = tempfile.mkdtemp(prefix='TEST_MEDIA_ROOT_')
        self.override = override_settings(MEDIA_ROOT=self.temp_media_root)
        self.override.enable()

    def _post_teardown(self):
        if hasattr(default_storage, 'bucket'):
            default_storage.bucket.objects.filter(Prefix=default_storage.location).delete()
        shutil.rmtree(self.temp_media_root)
        self.override.disable()
        super(CropdusterTestCaseMediaMixin, self)._post_teardown()

    def setUp(self):
        super(CropdusterTestCaseMediaMixin, self).setUp()

        random = uuid.uuid4().hex
        self.TEST_IMG_DIR = ORIG_IMG_PATH
        self.TEST_IMG_DIR_RELATIVE = os.path.join(random, 'data')

    def assertImageColorEqual(self, element, image):
        self.selenium.execute_script('arguments[0].scrollIntoView()', element)
        scroll_top = -1 * self.selenium.execute_script(
            'return document.body.getBoundingClientRect().top')
        tmp_file = tempfile.NamedTemporaryFile(suffix='.png')
        pixel_density = self.selenium.execute_script('return window.devicePixelRatio') or 1
        x1 = int(round(element.location['x'] + (element.size['width'] // 2.0)))
        y1 = int(round(element.location['y'] - scroll_top + (element.size['height'] // 2.0)))

        image_path = os.path.join(os.path.dirname(__file__), 'data', image)
        ref_im = PIL.Image.open(image_path).convert('RGB')
        w, h = ref_im.size
        x2, y2 = int(round(w // 2.0)), int(round(h // 2.0))
        ref_rgb = ref_im.getpixel((x2, y2))
        ref_im.close()

        def get_screenshot_rgb():
            if not self.selenium.save_screenshot(tmp_file.name):
                raise Exception("Failed to save screenshot")
            im = PIL.Image.open(tmp_file.name).convert('RGB')
            rgb = im.getpixel((x1 * pixel_density, y1 * pixel_density))
            im.close()
            return rgb

        self.wait_until(
            lambda d: get_screenshot_rgb() == ref_rgb,
            message=(
                "Colors differ: %s != %s" % (repr_rgb(ref_rgb), repr_rgb(get_screenshot_rgb()))))

    def create_unique_image(self, image):
        image_uuid = uuid.uuid4().hex

        ext = os.path.splitext(image)[1]
        image_name = os.path.join(
            self.TEST_IMG_DIR_RELATIVE, image_uuid, "original%s" % ext)
        preview_image_name = os.path.join(                                                                            
            self.TEST_IMG_DIR_RELATIVE, image_uuid, "_preview%s" % ext) 

        with open("%s/%s" % (ORIG_IMG_PATH, image), mode='rb') as f:
            default_storage.save(image_name, ContentFile(f.read()))

        with open("%s/%s" % (ORIG_IMG_PATH, image), mode='rb') as f:
            default_storage.save(preview_image_name, ContentFile(f.read()))

        return image_name
 119  
tests/models.py
@@ -0,0 +1,119 @@
from django.db import models
from django.utils.encoding import python_2_unicode_compatible

from cropduster.fields import ReverseForeignRelation
from cropduster.models import CropDusterField, Size


class Author(models.Model):
    name = models.CharField(max_length=255)
    HEADSHOT_SIZES = [
        Size('main', w=220, h=180, auto=[
            Size('thumb', w=110, h=90),
        ]),
    ]
    headshot = CropDusterField(upload_to="author/headshots/%Y/%m", sizes=HEADSHOT_SIZES,
        related_name="author_headshotset")


class Article(models.Model):
    title = models.CharField(max_length=255)
    author = models.ForeignKey(to=Author, blank=True, null=True,
        on_delete=models.SET_NULL)
    LEAD_IMAGE_SIZES = [
        Size(u'main', w=600, h=480, auto=[
            Size(u'thumb', w=110, h=90),
        ]),
        Size(u'no_height', w=600),
    ]
    ALT_IMAGE_SIZES = [
        Size(u'wide', w=600, h=300),
    ]
    lead_image = CropDusterField(upload_to="article/lead_image/%Y/%m",
                                db_column='image',
                                related_name="test_article_lead_image",
                                sizes=LEAD_IMAGE_SIZES)
    alt_image = CropDusterField(upload_to="article/alt_image/%Y/%m",
                                related_name="test_article_alt_image",
                                sizes=ALT_IMAGE_SIZES,
                                field_identifier="alt")


class OptionalSizes(models.Model):

    TEST_SIZES = [
        Size('main', w=600, h=480, auto=[
            Size('optional', w=1200, h=960, required=False),
        ])]

    slug = models.SlugField()
    image = CropDusterField(upload_to="test", sizes=TEST_SIZES)


class OrphanedThumbs(models.Model):

    TEST_SIZES = [
        Size('main', w=600, h=480, auto=[
            Size('main@2x', w=1200, h=960),
        ]),
        Size('secondary', w=600, h=480, auto=[
            Size('secondary@2x', w=1200, h=960),
        ])]

    slug = models.SlugField()
    image = CropDusterField(upload_to="test", sizes=TEST_SIZES)


class MultipleFieldsInheritanceParent(models.Model):

    slug = models.SlugField()
    image = CropDusterField(upload_to="test", sizes=[Size(u'main', w=600, h=480)])


class MultipleFieldsInheritanceChild(MultipleFieldsInheritanceParent):

    image2 = CropDusterField(upload_to="test", sizes=[Size(u'main', w=600, h=480)],
        field_identifier="2")


@python_2_unicode_compatible
class ReverseForeignRelA(models.Model):
    slug = models.SlugField()
    c = models.ForeignKey('ReverseForeignRelC', on_delete=models.CASCADE)
    a_type = models.CharField(max_length=10, choices=(
        ("x", "X"),
        ("y", "Y"),
        ("z", "Z"),
    ))

    def __str__(self):
        return self.slug


@python_2_unicode_compatible
class ReverseForeignRelB(models.Model):
    slug = models.SlugField()
    c = models.ForeignKey('ReverseForeignRelC', on_delete=models.CASCADE)

    def __str__(self):
        return self.slug


@python_2_unicode_compatible
class ReverseForeignRelC(models.Model):
    slug = models.SlugField()
    rel_a = ReverseForeignRelation(
        ReverseForeignRelA, field_name='c', limit_choices_to={'a_type': 'x'})
    rel_b = ReverseForeignRelation(ReverseForeignRelB, field_name='c')

    def __str__(self):
        return self.slug


@python_2_unicode_compatible
class ReverseForeignRelM2M(models.Model):
    slug = models.SlugField()
    m2m = models.ManyToManyField(ReverseForeignRelC)

    def __str__(self):
        return self.slug
 70  
tests/settings.py
@@ -0,0 +1,70 @@
import os
import uuid

import django
from django.core.signals import setting_changed
from django.dispatch import receiver
from django.utils.functional import lazy
from django.urls import reverse

from selenosis.settings import *


lazy_reverse = lazy(reverse, str)


if django.VERSION > (1, 11):
    MIGRATION_MODULES = {
        'auth': None,
        'contenttypes': None,
        'sessions': None,
        'cropduster': None,
    }

INSTALLED_APPS += (
    'generic_plus',
    'cropduster',
    'cropduster.standalone',
    'tests',
    'tests.standalone',
    'ckeditor',
)

ROOT_URLCONF = 'tests.urls'

TEMPLATES[0]['OPTIONS']['debug'] = True

if os.environ.get('S3') == '1':
    DEFAULT_FILE_STORAGE = 'storages.backends.s3boto3.S3Boto3Storage'
    AWS_STORAGE_BUCKET_NAME = 'ollie-cropduster-media-test-bucket-dev'
    AWS_DEFAULT_ACL = 'public-read'
    AWS_LOCATION = 'cropduster/%s/' % uuid.uuid4().hex
    AWS_S3_SIGNATURE_VERSION = 's3v4'
else:
    DEFAULT_FILE_STORAGE = 'django.core.files.storage.FileSystemStorage'

CKEDITOR_CONFIGS = {
    'default': {
        'extraPlugins': 'cropduster',
        'removePlugins': 'flash,forms,contextmenu,liststyle,table,tabletools,iframe',
        'disableAutoInline': True,
        "height": 450,
        "width": 840,
        'cropduster_uploadTo': 'ckeditor',
        'cropduster_previewSize': [570, 300],
        'cropduster_url': lazy_reverse('cropduster-standalone'),
        'cropduster_urlParams': {'max_w': 672, 'full_w': 960},
    },
}

CKEDITOR_UPLOAD_PATH = "%s/upload" % MEDIA_ROOT
CROPDUSTER_CREATE_THUMBS = True


@receiver(setting_changed)
def reload_settings(**kwargs):
    if kwargs['setting'] == 'CROPDUSTER_CREATE_THUMBS':
        from cropduster import settings as cropduster_settings
        cropduster_settings.CROPDUSTER_CREATE_THUMBS = kwargs['value']

os.makedirs(CKEDITOR_UPLOAD_PATH)
 1  
tests/standalone/__init__.py
@@ -0,0 +1 @@
default_app_config = 'tests.standalone.apps.StandaloneTestConfig'
 6  
tests/standalone/admin.py
@@ -0,0 +1,6 @@
from django.contrib import admin

from .models import Article


admin.site.register(Article)
 6  
tests/standalone/apps.py
@@ -0,0 +1,6 @@
from django.apps import AppConfig


class StandaloneTestConfig(AppConfig):
    name = 'tests.standalone'
    label = 'standalone_test'
 7  
tests/standalone/models.py
@@ -0,0 +1,7 @@
from django.db import models

from ckeditor.fields import RichTextField


class Article(models.Model):
    content = RichTextField(blank=True, config_name='default')
 194  
tests/standalone/test_admin.py
@@ -0,0 +1,194 @@
from __future__ import absolute_import

import contextlib
import re
import time
from unittest import SkipTest
import os

import django
from django.core.files.storage import default_storage
from django.test import override_settings

import PIL.Image
from selenosis import AdminSelenosisTestCase

from cropduster.models import Image, Thumb
from tests.helpers import CropdusterTestCaseMediaMixin

from .models import Article


class TestStandaloneAdmin(CropdusterTestCaseMediaMixin, AdminSelenosisTestCase):

    root_urlconf = 'tests.urls'

    @property
    def available_apps(self):
        apps = [
            'django.contrib.auth',
            'django.contrib.contenttypes',
            'django.contrib.messages',
            'django.contrib.sessions',
            'django.contrib.sites',
            'django.contrib.staticfiles',
            'django.contrib.admin',
            'generic_plus',
            'cropduster',
            'cropduster.standalone',
            'tests',
            'tests.standalone',
            'ckeditor',
            'selenosis',
        ]
        if self.has_grappelli:
            apps.insert(0, 'grappelli')
        return apps

    def _pre_setup(self):
        super(TestStandaloneAdmin, self)._pre_setup()
        self.ckeditor_override = override_settings(
            CKEDITOR_UPLOAD_PATH="%s/files/" % self.temp_media_root)
        self.ckeditor_override.enable()

    def _post_teardown(self):
        super(TestStandaloneAdmin, self)._post_teardown()
        self.ckeditor_override.disable()

    def setUp(self):
        if django.VERSION >= (2, 1):
            raise SkipTest("django-ckeditor not compatible with this version of Django")
        super(TestStandaloneAdmin, self).setUp()
        self.is_s3 = os.environ.get('S3') == '1'

    @contextlib.contextmanager
    def switch_to_ckeditor_iframe(self):
        with self.visible_selector('.cke_editor_cropduster_content_dialog iframe') as iframe:
            time.sleep(1)
            self.selenium.switch_to.frame(iframe)
            yield iframe
            self.selenium.switch_to.parent_frame()

    @contextlib.contextmanager
    def open_cropduster_ckeditor_dialog(self):
        with self.clickable_selector('.cke_button__cropduster_icon') as el:
            el.click()

        with self.switch_to_ckeditor_iframe():
            time.sleep(1)
            with self.visible_selector('#id_image'):
                yield

    def toggle_caption_checkbox(self):
        caption_checkbox_xpath = '//input[following-sibling::label[text()="Captioned image"]]'
        with self.clickable_xpath(caption_checkbox_xpath) as checkbox:
            checkbox.click()
        time.sleep(0.2)

    def cropduster_ckeditor_ok(self):
        with self.clickable_selector('.cke_dialog_ui_button_ok') as ok:
            ok.click()
        time.sleep(2 if self.is_s3 else 0.2)

    def test_basic_usage(self):
        self.load_admin(Article)

        with self.open_cropduster_ckeditor_dialog():
            with self.visible_selector('#id_image') as el:
                el.send_keys(os.path.join(self.TEST_IMG_DIR, 'img.png'))
            with self.clickable_selector('#upload-button') as el:
                el.click()
            self.wait_until_visible_selector('#id_size-width')

        self.toggle_caption_checkbox()
        self.cropduster_ckeditor_ok()

        if self.is_s3:
            time.sleep(5)

        content_html = self.selenium.execute_script('return $("#id_content").val()')

        img_src_matches = re.search(r' src="([^"]+)"', content_html)
        self.assertIsNotNone(img_src_matches, "Image not found in content: %s" % content_html)
        image_url = img_src_matches.group(1)
        image_hash = re.search(r'img/([0-9a-f]+)\.png', image_url).group(1)

        try:
            image = Image.objects.get(image='ckeditor/img/original.png')
        except Image.DoesNotExist:
            raise AssertionError("Image not found in database")

        try:
            thumb = Thumb.objects.get(name=image_hash, image=image)
        except Thumb.DoesNotExist:
            raise AssertionError("Thumb not found in database")

        self.assertEqual(
            list(Thumb.objects.all()), [thumb],
            "Exactly one Thumb object should have been created")

        self.assertHTMLEqual(
            content_html,
            u"""
            <figure>
                <img alt="" width="672" height="798" src="%s" />
                <figcaption class="caption">Caption</figcaption>
            </figure>
            <p>&nbsp;</p>
            """ % image_url)

    def test_dialog_change_width(self):
        """
        Test that changing the width in the cropduster CKEDITOR dialog produces
        an image and html with the correct dimensions
        """
        self.load_admin(Article)

        with self.open_cropduster_ckeditor_dialog():
            with self.visible_selector('#id_image') as el:
                el.send_keys(os.path.join(self.TEST_IMG_DIR, 'img.png'))
            with self.clickable_selector('#upload-button') as el:
                el.click()
            time.sleep(1)
            with self.clickable_selector('#id_size-width') as el:
                el.send_keys(300)

        self.toggle_caption_checkbox()
        self.cropduster_ckeditor_ok()

        if self.is_s3:
            time.sleep(5)

        content_html = self.selenium.execute_script('return $("#id_content").val()')

        img_src_matches = re.search(r' src="([^"]+)"', content_html)
        self.assertIsNotNone(img_src_matches, "Image not found in content: %s" % content_html)
        image_url = img_src_matches.group(1)
        image_hash = re.search(r'img/([0-9a-f]+)\.png', image_url).group(1)

        try:
            image = Image.objects.get(image='ckeditor/img/original.png')
        except Image.DoesNotExist:
            raise AssertionError("Image not found in database")

        try:
            thumb = Thumb.objects.get(name=image_hash, image=image)
        except Thumb.DoesNotExist:
            raise AssertionError("Thumb not found in database")

        self.assertEqual(
            list(Thumb.objects.all()), [thumb],
            "Exactly one Thumb object should have been created")

        with default_storage.open("ckeditor/img/%s.png" % image_hash, mode='rb') as f:
            self.assertEqual(PIL.Image.open(f).size, (300, 356))

        self.assertHTMLEqual(
            content_html,
            u"""
            <figure>
                <img alt="" width="300" height="356" src="%s" />
                <figcaption class="caption">Caption</figcaption>
            </figure>
            <p>&nbsp;</p>
            """ % image_url)
 10  
tests/templates/404.html
@@ -0,0 +1,10 @@
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en" lang="en">
<head>
	<meta http-equiv="Content-Type" content="text/html; charset=utf-8"/>
	<title>404</title>	
</head>
<body>
    <h1>404</h1>
</body>
</html>
 10  
tests/templates/500.html
@@ -0,0 +1,10 @@
<!DOCTYPE html>
<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en" lang="en">
<head>
	<meta http-equiv="Content-Type" content="text/html; charset=utf-8"/>
	<title>500</title>	
</head>
<body>
    <h1>500</h1>
</body>
</html>
 244  
tests/test_admin.py
@@ -0,0 +1,244 @@
from __future__ import absolute_import

import os

from django.core.files.storage import default_storage
from selenosis import AdminSelenosisTestCase

from cropduster.models import Image, Size
from .helpers import CropdusterTestCaseMediaMixin
from .models import Article, Author, OptionalSizes


class TestAdmin(CropdusterTestCaseMediaMixin, AdminSelenosisTestCase):

    root_urlconf = 'tests.urls'

    @property
    def available_apps(self):
        apps = [
            'django.contrib.auth',
            'django.contrib.contenttypes',
            'django.contrib.messages',
            'django.contrib.sessions',
            'django.contrib.sites',
            'django.contrib.staticfiles',
            'django.contrib.admin',
            'generic_plus',
            'cropduster',
            'tests',
            'tests.standalone',
            'selenosis',
        ]
        if self.has_grappelli:
            apps.insert(0, 'grappelli')
        return apps

    def test_addform_single_image(self):
        self.load_admin(Author)

        browser = self.selenium
        browser.find_element_by_id('id_name').send_keys('Mark Twain')
        with self.clickable_selector('#headshot-group .cropduster-button') as el:
            el.click()

        with self.switch_to_popup_window():
            with self.visible_selector('#id_image') as el:
                el.send_keys(os.path.join(self.TEST_IMG_DIR, 'img.png'))
            with self.clickable_selector('#upload-button') as el:
                el.click()
            with self.clickable_selector('#crop-button') as el:
                el.click()

        self.save_form()

        author = Author.objects.all()[0]
        sizes = list(Size.flatten(Author.HEADSHOT_SIZES))
        self.assertTrue(bool(author.headshot.name))

        image = author.headshot.related_object
        thumbs = image.thumbs.all()
        self.assertEqual(len(thumbs), len(sizes))
        main_thumb = image.thumbs.get(name='main')
        self.assertEqual(main_thumb.to_dict(), {
            'reference_thumb_id': None,
            'name': 'main',
            'width': 220,
            'height': 180,
            'crop_w': 674,
            'crop_h': 551,
            'crop_x': 0,
            'crop_y': 125,
            'image_id': image.pk,
            'id': main_thumb.pk,
        })
        auto_thumb = image.thumbs.get(name='thumb')
        self.assertEqual(auto_thumb.to_dict(), {
            'reference_thumb_id': main_thumb.pk,
            'name': 'thumb',
            'width': 110,
            'height': 90,
            'crop_w': None,
            'crop_h': None,
            'crop_x': None,
            'crop_y': None,
            'image_id': image.pk,
            'id': auto_thumb.pk,
        })
        self.assertTrue(default_storage.exists(auto_thumb.image_name))

    def test_addform_multiple_image(self):
        author = Author.objects.create(name="Mark Twain")
        self.load_admin(Article)
        browser = self.selenium
        browser.find_element_by_id('id_title').send_keys("A Connecticut Yankee in King Arthur's Court")

        # Upload and crop first Image
        browser.find_element_by_css_selector('#lead_image-group .cropduster-button').click()

        with self.switch_to_popup_window():
            with self.visible_selector('#id_image') as el:
                el.send_keys(os.path.join(self.TEST_IMG_DIR, 'img.jpg'))
            with self.clickable_selector('#upload-button') as el:
                el.click()
            with self.clickable_selector('#crop-button') as el:
                el.click()
            with self.clickable_selector('#crop-button:not(.disabled)') as el:
                el.click()

        # Upload and crop second Image
        with self.clickable_selector('#alt_image-group .cropduster-button') as el:
            # With the Chrome driver, using Grappelli, this button can be covered
            # by the fixed footer. So we scroll the button into view.
            browser.execute_script('window.scrollTo(0, %d)' % el.location['y'])
            el.click()

        with self.switch_to_popup_window():
            with self.visible_selector('#id_image') as el:
                el.send_keys(os.path.join(self.TEST_IMG_DIR, 'img.png'))
            with self.clickable_selector('#upload-button') as el:
                el.click()
            with self.clickable_selector('#crop-button') as el:
                el.click()

        # Add required FK
        browser.find_element_by_xpath('//select[@id="id_author"]/option[@value=%d]' % author.pk).click()

        self.save_form()

        # Test that crops saved correctly
        article = Article.objects.all()[0]
        lead_sizes = list(Size.flatten(Article.LEAD_IMAGE_SIZES))
        alt_sizes = list(Size.flatten(Article.ALT_IMAGE_SIZES))

        self.assertTrue(article.lead_image.name.endswith('.jpg'))
        self.assertEqual(len(article.lead_image.related_object.thumbs.all()), len(lead_sizes))
        self.assertTrue(article.alt_image.name.endswith('.png'))
        self.assertEqual(len(article.alt_image.related_object.thumbs.all()), len(alt_sizes))

    def test_changeform_single_image(self):
        image_path = self.create_unique_image('img.png')
        author = Author.objects.create(name="Samuel Langhorne Clemens",
            headshot=image_path)
        Image.objects.create(image=image_path, content_object=author)
        author.refresh_from_db()
        author.headshot.generate_thumbs()

        self.load_admin(author)

        preview_image_el = self.selenium.find_element_by_css_selector('#headshot-group .cropduster-image-thumb')
        src_image_path = os.path.join(self.TEST_IMG_DIR, 'img.png')
        self.assertImageColorEqual(preview_image_el, src_image_path)

        elem = self.selenium.find_element_by_id('id_name')
        elem.clear()
        elem.send_keys("Mark Twain")

        self.save_form()

        author = Author.objects.get(pk=author.pk)
        self.assertEqual(author.name, 'Mark Twain')
        self.assertEqual(author.headshot.name, image_path)
        self.assertEqual(len(author.headshot.related_object.thumbs.all()), 2)

    def test_changeform_multiple_images(self):
        author = Author.objects.create(name="Samuel Langhorne Clemens")
        lead_image_path = self.create_unique_image('img.jpg')
        alt_image_path = self.create_unique_image('img.png')
        article = Article.objects.create(title="title", author=author,
            lead_image=lead_image_path,
            alt_image=alt_image_path)
        Image.objects.create(image=lead_image_path, content_object=article)
        Image.objects.create(
            image=alt_image_path, content_object=article, field_identifier='alt')
        article.refresh_from_db()
        article.lead_image.generate_thumbs()
        article.alt_image.generate_thumbs()

        self.load_admin(article)

        elem = self.selenium.find_element_by_id('id_title')
        elem.clear()
        elem.send_keys("Updated Title")

        self.save_form()

        article.refresh_from_db()
        self.assertEqual(article.title, 'Updated Title')
        self.assertEqual(article.lead_image.name, lead_image_path)
        self.assertEqual(article.alt_image.name, alt_image_path)
        self.assertEqual(len(article.lead_image.related_object.thumbs.all()), 3)
        self.assertEqual(len(article.alt_image.related_object.thumbs.all()), 1)

    def test_changeform_with_optional_sizes_small_image(self):
        test_a = OptionalSizes.objects.create(slug='a')

        self.load_admin(test_a)

        # Upload and crop image
        with self.clickable_selector('#image-group .cropduster-button') as el:
            # With the Chrome driver, using Grappelli, this button can be covered
            # by the fixed footer. So we scroll the button into view.
            self.selenium.execute_script('window.scrollTo(0, %d)' % el.location['y'])
            el.click()

        with self.switch_to_popup_window():
            with self.visible_selector('#id_image') as el:
                el.send_keys(os.path.join(self.TEST_IMG_DIR, 'img.jpg'))
            with self.clickable_selector('#upload-button') as el:
                el.click()
            with self.clickable_selector('#crop-button') as el:
                el.click()

        self.save_form()

        test_a = OptionalSizes.objects.get(slug='a')
        image = test_a.image.related_object
        num_thumbs = len(image.thumbs.all())
        self.assertEqual(num_thumbs, 1, "Expected one thumb; instead got %d" % num_thumbs)

    def test_changeform_with_optional_sizes_large_image(self):
        test_a = OptionalSizes.objects.create(slug='a')
        self.load_admin(test_a)

        # Upload and crop image
        with self.clickable_selector('#image-group .cropduster-button') as el:
            # With the Chrome driver, using Grappelli, this button can be covered
            # by the fixed footer. So we scroll the button into view.
            self.selenium.execute_script('window.scrollTo(0, %d)' % el.location['y'])
            el.click()

        with self.switch_to_popup_window():
            with self.visible_selector('#id_image') as el:
                el.send_keys(os.path.join(self.TEST_IMG_DIR, 'img2.jpg'))
            with self.clickable_selector('#upload-button') as el:
                el.click()
            with self.clickable_selector('#crop-button') as el:
                el.click()

        self.save_form()

        test_a = OptionalSizes.objects.get(slug='a')
        image = test_a.image.related_object
        num_thumbs = len(image.thumbs.all())
        self.assertEqual(num_thumbs, 2, "Expected one thumb; instead got %d" % num_thumbs)
 27  
tests/test_gifsicle.py
@@ -0,0 +1,27 @@
from io import open, BytesIO
import os
import shutil
import tempfile

from PIL import Image, ImageSequence
from io import BytesIO

from django import test
from django.core.files.storage import default_storage
from django.conf import settings

from .helpers import CropdusterTestCaseMediaMixin


class TestUtilsImage(CropdusterTestCaseMediaMixin, test.TestCase):

    def _get_img(self, filename):
        return Image.open(os.path.join(self.TEST_IMG_DIR, filename))

    def test_is_animated_gif(self):
        from cropduster.utils import is_animated_gif
        yes = self._get_img('animated.gif')
        no = self._get_img('img.jpg')
        self.assertTrue(is_animated_gif(yes))
        self.assertFalse(is_animated_gif(no))

 400  
tests/test_models.py
@@ -0,0 +1,400 @@
from __future__ import absolute_import, division

from io import BytesIO
import os
import PIL

from django.core.files.storage import default_storage
from django.test import TestCase, override_settings
from django.contrib.contenttypes.models import ContentType
from django.utils.six.moves import range

from .helpers import CropdusterTestCaseMediaMixin
from .models import (
    Article, Author, OptionalSizes, MultipleFieldsInheritanceChild,
    ReverseForeignRelA, ReverseForeignRelB, ReverseForeignRelC,
    ReverseForeignRelM2M, OrphanedThumbs)
from cropduster.models import Size, Image, Thumb
from cropduster.exceptions import CropDusterResizeException
from cropduster import settings as cropduster_settings


class TestImage(CropdusterTestCaseMediaMixin, TestCase):

    def setUp(self):
        super(TestImage, self).setUp()
        self.author = Author.objects.create(name="Samuel Langhorne Clemens")

    def test_original_image(self):
        article = Article.objects.create(title="Pudd'nhead Wilson",
            author=self.author, lead_image=self.create_unique_image('img.jpg'))
        article.lead_image.generate_thumbs()
        article = Article.objects.get(pk=article.pk)
        self.assertEqual(article.lead_image.width, 674)
        self.assertEqual(article.lead_image.height, 800)
        self.assertIs(article.lead_image.sizes, Article.LEAD_IMAGE_SIZES)

    def test_generate_thumbs(self):
        article = Article.objects.create(title="Pudd'nhead Wilson",
            author=self.author, lead_image=self.create_unique_image('img.jpg'))
        article.lead_image.generate_thumbs()
        article = Article.objects.get(pk=article.pk)
        sizes = sorted(list(Size.flatten(Article.LEAD_IMAGE_SIZES)), key=lambda x: x.name)
        thumbs = sorted(list(article.lead_image.related_object.thumbs.all()), key=lambda x: x.name)
        self.assertEqual(len(thumbs), len(sizes))
        for size, thumb in zip(sizes, thumbs):
            self.assertEqual(size.name, thumb.name)
            if size.width:
                self.assertEqual(size.width, thumb.width)
            if size.height:
                self.assertEqual(size.height, thumb.height)
            else:
                ratio = article.lead_image.height / article.lead_image.width
                self.assertAlmostEqual(thumb.height, ratio * size.width, delta=1)
            self.assertEqual(thumb.image.image, article.lead_image.related_object.image)
            self.assertTrue(default_storage.exists(thumb.image_name))
            with default_storage.open(thumb.image_name, mode='rb') as f:
                self.assertEqual((thumb.width, thumb.height), PIL.Image.open(f).size)

        image = PIL.Image.open(os.path.join(self.TEST_IMG_DIR, 'img.jpg'))
        image.thumbnail((50, 50))
        buf = BytesIO()
        image.save(buf, format=image.format)
        default_storage.save('new-img.jpg', buf)
        article = Article.objects.create(
            title="Img Too Small", author=self.author, lead_image='new-img.jpg')
        self.assertRaises(CropDusterResizeException, article.lead_image.generate_thumbs)

    @override_settings(CROPDUSTER_CREATE_THUMBS=False)
    def test_dont_generate_thumbs(self):
        article = Article.objects.create(title="Pudd'nhead Wilson",
            author=self.author, lead_image=self.create_unique_image('img.jpg'))
        article.lead_image.generate_thumbs()
        article = Article.objects.get(pk=article.pk)
        sizes = sorted(list(Size.flatten(Article.LEAD_IMAGE_SIZES)), key=lambda x: x.name)
        thumbs = sorted(list(article.lead_image.related_object.thumbs.all()), key=lambda x: x.name)
        self.assertEqual(len(thumbs), len(sizes))
        for size, thumb in zip(sizes, thumbs):
            self.assertEqual(size.name, thumb.name)
            if size.width:
                self.assertEqual(size.width, thumb.width)
            if size.height:
                self.assertEqual(size.height, thumb.height)
            else:
                ratio = article.lead_image.height / article.lead_image.width
                self.assertAlmostEqual(thumb.height, ratio * size.width, delta=1)
            self.assertEqual(thumb.image.image, article.lead_image.related_object.image)
            self.assertFalse(default_storage.exists(thumb.image_name))
            with self.assertRaises(IOError):
                default_storage.open(thumb.image_name, mode='rb')

    def test_prefetch_related_with_images(self):
        for x in range(3):
            lead_image = self.create_unique_image('img.jpg')
            article = Article.objects.create(title="", author=self.author, lead_image=lead_image)
            article.lead_image.generate_thumbs()

        with self.assertNumQueries(2):
            articles = Article.objects.filter(pk__in=[article.pk])
            for article in articles.prefetch_related('lead_image'):
                article.lead_image.related_object

        with self.assertNumQueries(3):
            articles = Article.objects.filter(pk__in=[article.pk])
            for article in articles.prefetch_related('lead_image__thumbs'):
                list(article.lead_image.related_object.thumbs.all())

    def test_prefetch_related_reverse_relation_cache(self):
        for x in range(3):
            lead_image = self.create_unique_image('img.jpg')
            article = Article.objects.create(title="", author=self.author, lead_image=lead_image)
            article.lead_image.generate_thumbs()

        with self.assertNumQueries(3):
            articles = Article.objects.filter(pk__in=[article.pk])
            for article in articles.prefetch_related('lead_image__thumbs'):
                for thumb in article.lead_image.related_object.thumbs.all():
                    thumb.image

    def test_redundant_prefetch_related_args_with_images(self):
        for x in range(3):
            lead_image = self.create_unique_image('img.jpg')
            article = Article.objects.create(title="", author=self.author, lead_image=lead_image)
            article.lead_image.generate_thumbs()

        with self.assertNumQueries(3):
            articles = Article.objects.filter(pk__in=[article.pk])
            for article in articles.prefetch_related('lead_image', 'lead_image__thumbs'):
                list(article.lead_image.related_object.thumbs.all())

    def test_prefetch_related_with_alt_images(self):
        img_map = {}
        for x in range(3):
            lead_image_path = self.create_unique_image('img.jpg')
            alt_image_path = self.create_unique_image('img.jpg')
            article = Article.objects.create(title="", author=self.author,
                lead_image=lead_image_path, alt_image=alt_image_path)
            article.lead_image.generate_thumbs()
            article.alt_image.generate_thumbs()
            img_map[article.pk] = (lead_image_path, alt_image_path)

        with self.assertNumQueries(5):
            articles = (Article.objects.filter(id__in=img_map.keys())
                .prefetch_related('lead_image__thumbs', 'alt_image__thumbs'))
            for article in articles:
                lead_name, alt_name = img_map[article.pk]
                self.assertEqual(lead_name, article.lead_image.related_object.image.name)
                self.assertEqual(alt_name, article.alt_image.related_object.image.name)

                lead_sizes = [s.name for s in Size.flatten(Article.LEAD_IMAGE_SIZES)]
                lead_thumbs = list(article.lead_image.related_object.thumbs.all())
                self.assertEqual(len(lead_thumbs), len(lead_sizes))
                for thumb in lead_thumbs:
                    self.assertEqual(thumb.image_id, article.lead_image.related_object.pk)
                    self.assertIn(thumb.name, lead_sizes)

                alt_sizes = [s.name for s in Size.flatten(Article.ALT_IMAGE_SIZES)]
                alt_thumbs = list(article.alt_image.related_object.thumbs.all())
                self.assertEqual(len(alt_thumbs), len(alt_sizes))
                for thumb in alt_thumbs:
                    self.assertEqual(thumb.image_id, article.alt_image.related_object.pk)
                    self.assertIn(thumb.name, alt_sizes)

    def test_prefetch_related_through_table(self):
        author = Author.objects.create(name="Author")
        for x in range(10):
            article = Article.objects.create(
                title="prefetch", author=author,
                lead_image=self.create_unique_image('img.jpg'),
                alt_image=self.create_unique_image('img.png'))
            article.lead_image.generate_thumbs()
            article.alt_image.generate_thumbs()

        lead_sizes = [s.name for s in Size.flatten(Article.LEAD_IMAGE_SIZES)]
        alt_sizes = [s.name for s in Size.flatten(Article.ALT_IMAGE_SIZES)]

        with self.assertNumQueries(6):
            authors = Author.objects.filter(pk=author.pk).prefetch_related(
                'article_set__lead_image__thumbs',
                'article_set__alt_image__thumbs')
            for author in authors:
                for article in author.article_set.all():
                    self.assertTrue(article.lead_image.name.endswith('jpg'))
                    self.assertTrue(article.alt_image.name.endswith('png'))
                    for thumb in article.lead_image.related_object.thumbs.all():
                        self.assertIn(thumb.name, lead_sizes)
                    for thumb in article.alt_image.related_object.thumbs.all():
                        self.assertIn(thumb.name, alt_sizes)


class TestModelSaving(CropdusterTestCaseMediaMixin, TestCase):

    def test_save_image_updates_model(self):
        img_path = self.create_unique_image('img.png')
        article = Article.objects.create(title="test", author=Author.objects.create(name='test'))
        article_ct = ContentType.objects.get_for_model(Article, for_concrete_model=False)
        Image.objects.create(
            content_type=article_ct,
            object_id=article.pk,
            image=img_path)
        self.assertFalse(article.lead_image)

        # Refresh the article from the database
        article.refresh_from_db()
        self.assertTrue(article.lead_image)
        self.assertEqual(article.lead_image.name, img_path)

    def test_resave_single_image_model(self):
        img_path = self.create_unique_image('img.jpg')
        author = Author(name='test')
        author.headshot = img_path
        author.save()

        author = Author.objects.get(pk=author.pk)
        author.save()

        author = Author.objects.get(pk=author.pk)
        self.assertEqual(author.headshot.name, img_path)

    def test_resave_single_image_model_with_thumbs(self):
        img_path = self.create_unique_image('img.jpg')
        author = Author(name='test')
        author.headshot = img_path
        author.save()

        author.headshot.generate_thumbs()

        author = Author.objects.get(pk=author.pk)
        author.save()

        author = Author.objects.get(pk=author.pk)
        self.assertEqual(author.headshot.name, img_path)

    def test_resave_multi_image_model_with_one_image(self):
        img_path = self.create_unique_image('img.jpg')
        article = Article(title="title", author=Author.objects.create(name='test'))
        article.lead_image = img_path
        article.save()

        article = Article.objects.get(pk=article.pk)
        article.save()

        article = Article.objects.get(pk=article.pk)
        self.assertEqual(article.lead_image.name, img_path)

    def test_resave_multi_image_model_with_one_image_and_thumbs(self):
        img_path = self.create_unique_image('img.jpg')
        article = Article(title="title", author=Author.objects.create(name='test'))
        article.lead_image = img_path
        article.save()

        article.lead_image.generate_thumbs()

        article = Article.objects.get(pk=article.pk)
        article.save()

        article = Article.objects.get(pk=article.pk)
        self.assertEqual(article.lead_image.name, img_path)

    def test_resave_multi_image_model_with_two_images(self):
        lead_image = self.create_unique_image('img.jpg')
        alt_image = self.create_unique_image('img.png')
        article = Article(title="title", author=Author.objects.create(name='test'))
        article.lead_image = lead_image
        article.alt_image = alt_image
        article.save()

        article = Article.objects.get(pk=article.pk)
        article.save()

        article = Article.objects.get(pk=article.pk)
        self.assertEqual(article.lead_image.name, lead_image)
        self.assertEqual(article.alt_image.name, alt_image)

    def test_resave_multi_image_model_with_two_images_and_thumbs(self):
        lead_image = self.create_unique_image('img.jpg')
        alt_image = self.create_unique_image('img.png')

        article = Article(title="title", author=Author.objects.create(name='test'))
        article.lead_image = lead_image
        article.alt_image = alt_image
        article.save()

        article.lead_image.generate_thumbs()
        article.alt_image.generate_thumbs()

        article = Article.objects.get(pk=article.pk)
        article.save()

        article = Article.objects.get(pk=article.pk)
        self.assertEqual(article.lead_image.name, lead_image)
        self.assertEqual(article.alt_image.name, alt_image)

    def test_change_image_on_model_with_two_images(self):
        lead_image = self.create_unique_image('img.jpg')
        alt_image = self.create_unique_image('img.png')

        article = Article(title="title", author=Author.objects.create(name='test'))
        article.lead_image = lead_image
        article.save()

        article = Article.objects.get(pk=article.pk)
        article.alt_image = alt_image
        article.save()

        article = Article.objects.get(pk=article.pk)
        self.assertEqual(article.lead_image.name, lead_image)
        self.assertEqual(article.alt_image.name, alt_image)

    def test_optional_sizes(self):
        test_a = OptionalSizes.objects.create(slug='a')
        test_a.image = self.create_unique_image('img.jpg')
        test_a.save()
        test_a.image.generate_thumbs()

        image = Image.objects.get(content_type=ContentType.objects.get_for_model(test_a),
            object_id=test_a.pk)
        num_thumbs = len(image.thumbs.all())
        self.assertEqual(num_thumbs, 1, "Expected one thumb; instead got %d" % num_thumbs)

        test_b = OptionalSizes.objects.create(slug='b')
        test_b.image = self.create_unique_image('img2.jpg')
        test_b.save()
        test_b.image.generate_thumbs()

        image = Image.objects.get(content_type=ContentType.objects.get_for_model(test_b),
            object_id=test_b.pk)
        num_thumbs = len(image.thumbs.all())
        self.assertEqual(num_thumbs, 2, "Expected one thumb; instead got %d" % num_thumbs)

    def test_multiple_fields_with_inheritance(self):
        child_fields = [f.name for f in MultipleFieldsInheritanceChild._meta.local_fields]
        self.assertNotIn('image', child_fields,
            "Field 'image' from parent model should not be in the child model's local_fields")

    def test_orphaned_thumbs_after_delete(self):
        test_a = OrphanedThumbs.objects.create(
            slug='a', image=self.create_unique_image('img2.jpg'))
        test_a.image.generate_thumbs()
        test_a = OrphanedThumbs.objects.get(slug='a')
        test_a.delete()

        num_thumbs = len(Thumb.objects.all())
        self.assertEqual(num_thumbs, 0, "%d orphaned thumbs left behind after deletion")


class TestReverseForeignRelation(TestCase):

    def test_standard_manager(self):
        c = ReverseForeignRelC.objects.create(slug='c-1')
        for i in range(0, 3):
            ReverseForeignRelB.objects.create(slug="b-%d" % i, c=c)

        c.refresh_from_db()
        self.assertEqual(len(c.rel_b.all()), 3)

    def test_standard_prefetch_related(self):
        for i in range(0, 2):
            m2m = ReverseForeignRelM2M.objects.create(slug='standard-m2m-%d' % i)
            for j in range(0, 2):
                c = ReverseForeignRelC.objects.create(slug='c-%d-%d' % (i, j))
                m2m.m2m.add(c)
                for k in range(0, 3):
                    ReverseForeignRelB.objects.create(slug="b-%d-%d-%d" % (i, j, k), c=c)
        objs = ReverseForeignRelM2M.objects.prefetch_related('m2m__rel_b')
        with self.assertNumQueries(3):
            for obj in objs:
                for m2m_obj in obj.m2m.all():
                    self.assertEqual(len(m2m_obj.rel_b.all()), 3)

    def test_manager_with_limit_choices_to(self):
        """
        A ReverseForeignRelation with limit_choices_to applies the filter to the manager
        """
        c = ReverseForeignRelC.objects.create(slug='c-1')
        for i in range(0, 3):
            ReverseForeignRelA.objects.create(slug="a-%d" % i, c=c, a_type="x")
        ReverseForeignRelA.objects.create(slug="a-4", c=c, a_type="y")

        c.refresh_from_db()
        a_len = len(c.rel_a.all())
        self.assertNotEqual(a_len, 4, "limit_choices_to filter not applied")
        self.assertNotEqual(a_len, 0, "manager returned no objects, expected 3")
        self.assertEqual(a_len, 3)

    def test_prefetch_related_with_limit_choices_to(self):
        for i in range(0, 2):
            m2m = ReverseForeignRelM2M.objects.create(slug='standard-m2m-%d' % i)
            for j in range(0, 2):
                c = ReverseForeignRelC.objects.create(slug='c-%d-%d' % (i, j))
                m2m.m2m.add(c)
                for k in range(0, 3):
                    ReverseForeignRelA.objects.create(
                        slug="a-%d-%d-%d" % (i, j, k), c=c, a_type='x')
                ReverseForeignRelA.objects.create(
                    slug="a-%d-%d-%d" % (i, j, 4), c=c, a_type='y')
        objs = ReverseForeignRelM2M.objects.prefetch_related('m2m__rel_a')
        with self.assertNumQueries(3):
            for obj in objs:
                for m2m_obj in obj.m2m.all():
                    self.assertEqual(len(m2m_obj.rel_a.all()), 3)
 25  
tests/test_resizing.py
@@ -0,0 +1,25 @@
import os

from django import test

from .helpers import CropdusterTestCaseMediaMixin
from cropduster.resizing import Crop, Box, Size


class TestResizing(CropdusterTestCaseMediaMixin, test.TestCase):

    def test_off_by_one_bug(self):
        img_path = self.create_unique_image('best-fit-off-by-one-bug.png')
        crop = Crop(Box(x1=0, y1=0, x2=960, y2=915), img_path)
        size = Size('960', w=960, h=594)
        new_crop = size.fit_to_crop(crop)
        self.assertNotEqual(new_crop.box.h, 593, "Calculated best fit height is 1 pixel too short")
        self.assertEqual(new_crop.box.h, 594)

    def test_size_order_bug(self):
        img_path = self.create_unique_image('size-order-bug.png')
        crop = Crop(Box(x1=160, y1=0, x2=800, y2=640), img_path)
        size = Size('650', w=650, min_h=250)
        new_crop = size.fit_to_crop(crop)
        self.assertGreaterEqual(new_crop.box.w, 650,
            "Calculated best fit (%d) didn't get required width (650)" % new_crop.box.w)
 108  
tests/test_utils.py
@@ -0,0 +1,108 @@
from io import open, BytesIO
import os
import shutil
import tempfile

from PIL import Image

from django import test
from django.core.files.storage import default_storage
from django.conf import settings

from .helpers import CropdusterTestCaseMediaMixin


class TestUtilsImage(CropdusterTestCaseMediaMixin, test.TestCase):

    def _get_img(self, filename):
        return Image.open(os.path.join(self.TEST_IMG_DIR, filename))

    def test_that_test_work(self):
        self.assertEqual(True, True)

    def test_get_image_extension(self):
        from cropduster.utils import get_image_extension

        tmp_jpg_bad_ext_pdf = tempfile.NamedTemporaryFile(suffix='.pdf')
        tmp_png_bad_ext_jpg = tempfile.NamedTemporaryFile(suffix='.png')

        with open(os.path.join(self.TEST_IMG_DIR, 'img.jpg'), mode='rb') as f:
            tmp_jpg_bad_ext_pdf.write(f.read())
            tmp_jpg_bad_ext_pdf.seek(0)

        with open(os.path.join(self.TEST_IMG_DIR, 'img.png'), mode='rb') as f:
            tmp_png_bad_ext_jpg.write(f.read())
            tmp_png_bad_ext_jpg.seek(0)

        imgs = [
            (self._get_img('img.jpg'), '.jpg'),
            (self._get_img('img.png'), '.png'),
            (self._get_img('animated.gif'), '.gif'),
            (Image.open(tmp_jpg_bad_ext_pdf.name), '.jpg'),
            (Image.open(tmp_png_bad_ext_jpg.name), '.png'),
        ]
        for img, ext in imgs:
            self.assertEqual(get_image_extension(img), ext)

    def test_is_transparent(self):
        from cropduster.utils import is_transparent
        yes = self._get_img('transparent.png')
        no = self._get_img('img.png')

        self.assertTrue(is_transparent(yes))
        self.assertFalse(is_transparent(no))

    def test_correct_colorspace(self):
        from cropduster.utils import correct_colorspace
        img = self._get_img('cmyk.jpg')
        self.assertEqual(img.mode, 'CMYK')
        converted = correct_colorspace(img)
        self.assertEqual(img.mode, 'CMYK')
        self.assertEqual(converted.mode, 'RGB')

    def test_is_animated_gif(self):
        from cropduster.utils import is_animated_gif
        yes = self._get_img('animated.gif')
        no = self._get_img('img.jpg')
        self.assertTrue(is_animated_gif(yes))
        self.assertFalse(is_animated_gif(no))


class TestUtilsPaths(CropdusterTestCaseMediaMixin, test.TestCase):

    def test_get_upload_foldername(self):
        import uuid
        from cropduster.utils import get_upload_foldername

        path = random = uuid.uuid4().hex
        folder_path = get_upload_foldername('my img.jpg', upload_to=path)
        self.assertEqual(folder_path, "%s/my_img" % (path))
        default_storage.save("%s/original.jpg" % folder_path, BytesIO(b''))
        self.assertEqual(get_upload_foldername('my img.jpg', upload_to=path),
                         os.path.join(path, 'my_img-1'))

    def test_get_min_size(self):
        from cropduster.utils import get_min_size
        from cropduster.resizing import Size

        sizes = [
            Size('a', w=200, h=200),
            Size('b', w=100, h=300),
            Size('c', w=20, h=20)
        ]
        self.assertEqual(get_min_size(sizes), (200, 300))

        sizes = [
            Size('a', min_w=200, min_h=200, max_h=500),
            Size('b', min_w=100, min_h=300),
            Size('c', w=20, h=20)
        ]
        self.assertEqual(get_min_size(sizes), (200, 300))

    def test_get_media_path(self):
        from generic_plus.utils import get_media_path

        img_name = '/test/some-test-image.jpg'
        from_url = settings.MEDIA_URL + img_name
        to_url = settings.MEDIA_ROOT + img_name
        self.assertEqual(get_media_path(from_url), to_url)
 113  
tests/test_views.py
@@ -0,0 +1,113 @@
import os

from django import test
from django.core.files.storage import default_storage
try:
    from django.urls import reverse
except ImportError:
    from django.core.urlresolvers import reverse
from django.contrib.auth.models import User
from django.http import HttpRequest

from cropduster import views
from cropduster.utils import json

from .helpers import CropdusterTestCaseMediaMixin


class CropdusterViewTestRunner(CropdusterTestCaseMediaMixin, test.TestCase):
    def setUp(self):
        super(CropdusterViewTestRunner, self).setUp()
        self.factory = test.RequestFactory()
        self.user = User.objects.create_superuser('test',
            'test@test.com', 'password')


class TestIndex(CropdusterViewTestRunner):

    def test_get_is_200(self):
        request = self.factory.get(reverse('cropduster-index'))
        request.user = self.user
        response = views.index(request)
        self.assertEqual(response.status_code, 200)

    def test_post_is_405(self):
        request = self.factory.post(reverse('cropduster-index'), {})
        request.user = self.user
        response = views.index(request)
        self.assertEqual(response.status_code, 405)


class TestUpload(CropdusterViewTestRunner):

    def test_get_request(self):
        request = HttpRequest()
        request.method = "GET"
        request.user = self.user
        self.assertEqual(
            views.upload(request).content,
            views.index(request).content)

    def test_post_request(self):
        img_file = open(os.path.join(self.TEST_IMG_DIR, 'img.jpg'), 'rb')
        data = {
            u'image': img_file,
            u'upload_to': [u'test'],
            u'image_element_id': u'mt_image',
            u'md5': u'',
            u'preview_height': u'500',
            u'preview_width': u'800',
            u'sizes': u'''
            [{
            "auto": [{
                        "max_w": null,
                        "retina": 0,
                        "min_h": 1,
                        "name": "lead",
                        "w": 570,
                        "h": null,
                        "min_w": 570,
                        "__type__": "Size",
                        "max_h": null,
                        "label": "Lead"
                    }, {
                        "max_w": null,
                        "retina": 0,
                        "min_h": 110,
                        "name": "featured_small",
                        "w": 170,
                        "h": 110,
                        "min_w": 170,
                        "__type__": "Size",
                        "max_h": null,
                        "label": "Featured Small"
                    }, {
                        "max_w": null,
                        "retina": 0,
                        "min_h": 250,
                        "name": "featured_large",
                        "w": 386,
                        "h": 250,
                        "min_w": 386,
                        "__type__": "Size",
                        "max_h": null,
                        "label": "Featured Large"
                    }],
            "retina": 0,
            "name": "lead_large",
            "h": null,
            "min_w": 615,
            "__type__": "Size",
            "max_h": null,
            "label": "Lead Large",
            "max_w": null,
            "min_h": 250,
            "w": 615
        }]''',
        }
        request = self.factory.post(reverse('cropduster-upload'), data)
        request.user = self.user
        response = views.upload(request)
        self.assertEqual(response.status_code, 200)
        data = json.loads(response.content)
        self.assertTrue(default_storage.exists(data['orig_image']))
 24  
tests/urls.py
@@ -0,0 +1,24 @@
import django
from django.conf import settings
from django.conf.urls import include, url, static
from django.contrib import admin


admin.autodiscover()

urlpatterns = [
    url(r"^cropduster/", include("cropduster.urls")),
    url(r'^ckeditor/', include('ckeditor.urls')),
]

if django.VERSION < (1, 9):
    urlpatterns += [url(r'^admin/', include(admin.site.urls))]
else:
    urlpatterns += [url(r'^admin/', admin.site.urls)]

try:
    import grappelli.urls
except ImportError:
    pass
else:
    urlpatterns += [url(r"^grappelli/", include(grappelli.urls))]
 40  
tests/utils.py
@@ -0,0 +1,40 @@
import six


def esc_code(codes=None):
    if codes is None:
        # reset escape code
        return "\x1b[0m"
    if not isinstance(codes, (list, tuple)):
        codes = [codes]
    return '\x1b[0;' + ';'.join(map(six.text_type, codes)) + 'm'


def get_luminance(rgb):
    rgb_map = []
    for val in rgb:
        val = val / 256
        if val <= 0.03928:
            rgb_map.append(val / 12.92)
        else:
            rgb_map.append(pow((val + 0.055) / 1.055, 2.4))

    return (0.2126 * rgb_map[0]) + (0.7152 * rgb_map[1]) + (0.0722 * rgb_map[2])


def repr_rgb(rgb):
    r, g, b = rgb
    codes = (48, 2, r, g, b)
    reset = "\x1b[0m"
    hex_color = "#%s" % ("".join(["%02x" % c for c in rgb]))
    luminance = get_luminance(rgb)
    if luminance > 0.5:
        codes += (38, 2, 0, 0, 0)
    else:
        codes += (38, 2, 255, 255, 255)

    return "%(codes)s%(hex)s%(reset)s" % {
        'codes': esc_code(codes),
        'hex': hex_color,
        'reset': reset,
    }
 77  
tox.ini
@@ -0,0 +1,77 @@
[tox]
envlist =
    py{27,36}-dj111-{grp,nogrp}
    py{36,37,38}-dj{22,30,31}-{grp,nogrp}
skipsdist = True

[gh-actions]
python =
    2.7: py27
    3.6: py36
    3.7: py37
    3.8: py38

[gh-actions:env]
DJANGO =
    1.11: dj111
    2.2: dj22
    3.0: dj30
    3.1: dj31
GRAPPELLI =
    0: nogrp
    1: grp

[testenv]
commands =
    pytest --junitxml={toxinidir}/reports/test-{envname}.xml {posargs}
usedevelop = True
setenv =
    COVERAGE_FILE={toxworkdir}/coverage/.coverage.{envname}
passenv =
    CI
    TRAVIS
    TRAVIS_*
    DEFAULT_FILE_STORAGE
    AWS_ACCESS_KEY_ID
    AWS_SECRET_ACCESS_KEY
    S3
deps =
    pytest
    pytest-cov
    pytest-django
    selenium
    py27: django-selenosis<2.0.0
    !py27: django-selenosis
    boto3==1.12.18
    django-storages==1.9.1
    dj111: Django>=1.11a1,<1.11.99
    dj20: Django>=2.0.0,<2.0.99
    dj21: Django>=2.1.0,<2.1.99
    dj22: Django>=2.2a1,<2.2.99
    dj30: Django>=3.0,<3.1
    dj31: Django>=3.1a0,<3.2
    dj111-grp: django-grappelli==2.10.4
    dj22-grp: django-grappelli==2.13.4
    dj30-grp: django-grappelli==2.14.3
    dj31-grp: django-grappelli==2.14.3
    lxml
    -e git+https://github.com/theatlantic/django-ckeditor.git@v4.5.7+atl.6.1#egg=django-ckeditor

[testenv:coverage-report]
skip_install = true
deps = coverage
setenv=COVERAGE_FILE=.coverage
changedir = {toxworkdir}/coverage
commands =
    coverage combine
    coverage report
    coverage xml

[testenv:codecov]
skip_install = true
deps = codecov
depends = coverage-report
passenv = CODECOV_TOKEN
changedir = {toxinidir}
commands =
    codecov --file {toxworkdir}/coverage/*.xml {posargs}
0 comments on commit ae09a9f
@mowjoejoejoejoe
 
Add heading textAdd bold text, <Ctrl+b>Add italic text, <Ctrl+i>
Add a quote, <Ctrl+Shift+.>Add code, <Ctrl+e>Add a link, <Ctrl+k>
Add a bulleted list, <Ctrl+Shift+8>Add a numbered list, <Ctrl+Shift+7>Add a task list, <Ctrl+Shift+l>
Directly mention a user or team
Reference an issue, pull request, or discussion
Add saved reply
Leave a comment
No file chosen
Attach files by dragging & dropping, selecting or pasting them.
Styling with Markdown is supported
 You???re not receiving notifications from this thread.
Footer
?? 2023 GitHub, Inc.
Footer navigation
Terms
Privacy
Security
Status
Docs
Contact GitHub
Pricing
API
Training
Blog
About
Merge branch 'master' into trunk ?? theatlantic/django-cropduster@ae09a9f
Add heading textAdd bold text, <Ctrl+b>Add italic text, <Ctrl+i>
Add a quote, <Ctrl+Shift+.>Add code, <Ctrl+e>Add a link, <Ctrl+k>
Add a bulleted list, <Ctrl+Shift+8>Add a numbered list, <Ctrl+Shift+7>Add a task list, <Ctrl+Shift+l>
Directly mention a user or team
Reference an issue, pull request, or discussion
Add saved reply
Leave a comment
No file chosen
Attach files by dragging & dropping, selecting or pasting them.
Styling with Markdown is supported
 You???re not receiving notifications from this thread.
Footer
?? 2023 GitHub, Inc.
Footer navigation
Terms
Privacy
Security
Status
Docs
Contact GitHub
Pricing
API
Training
Blog
About
Merge branch 'master' into trunk'@ci/CI'@electron/atom.md'@django-cropduster@ae09a9f
'*'"'*'{'' '"author'' ':ZachryTWood''@Administrator''@'.it'.git'' ':
mowjoejoejoe'' 'README.md'' 'Skip'' 'to'' 'content'' 'Search'' 'or'' 'jump'' 'to???'' 'Pull'' 'requests'' 'Issues'' 'Codespaces'' 'Marketplace'' 'Explore'' ''@mowjoejoejoejoe'' 'Your'' 'account'' 'has'' 'been'' 'flagged.'' 'Because'' 'of'' 'that,'' 'your'' 'profile'' 'is'' 'hidden'' 'from'' 'the'' 'public.'' 'If'' 'you'' 'believe'' 'this'' 'is'' 'a'' 'mistake,'' 'contact'' 'support'' 'to'' 'have'' 'your'' 'account'' 'status'' 'reviewed.'' 'github'' '/'' 'docs'' 'Public'' 'Fork'' 'your'' 'own'' 'copy'' 'of'' 'github/docs'' 'Code'' 'Issues'' '97'' 'Pull'' 'requests'' '62'' 'Discussions'' 'Actions'' 'Projects'' '4'' 'Security'' 'Insights'' 'PAT'' 'v2'' 'beta'' '(#31013)'' 'Co''
'-authored''
'-by:'' 'Hirsch'' 'Singhal'' '1666363+hpsin'@users.noreply.github.com'' 'Co''
'-authored''
'-by:'' 'Jovel'' 'Crisostomo'' 'jovel'@github.com'' 'Co''
'-authored''
'-by:'' 'Lucas'' 'Costi'' 'lucascosti'@users.noreply.github.com'' 'Co''
'-authored''
'-by:'' 'Vanessa'' 'vgrl'@github.com'' 'main'' '(#21457)'' 'v1.0.1'' ''@skedwards88'' ''@hpsin'' ''@jovel'' ''@lucascosti'' ''@vgrl'' '5'' 'people'' 'committed'' 'on'' 'Oct'' '18,'' '2022'' '1'' 'parent'' '60a2264'' 'commit'' 'dac4144'' 'Show'' 'file'' 'tree'' 'Hide'' 'file'' 'tree'' 'Showing'' '179'' 'changed'' 'files'' 'with'' '2,349'' 'additions'' 'and'' '312'' 'deletions.'' '4
...''
'-account''
'-on''
'-github/managing''
'-your''
'-personal''
'-account/managing''
'-multiple''
'-accounts.md'' ''@'@'' '''
'-36,9'' '+36,9'' ''@'@'' 'You'' 'can'' 'find'' 'both'' 'the'' 'HTTPS'' 'or'' 'an'' 'SSH'' 'URLs'' 'for'' 'cloning'' 'a'' 'repository'' 'on'' '{%'' 'data'' 'vFor'' 'more'' 'information'' 'about'' 'the'' 'use'' 'of'' 'SSH'' 'to'' 'access'' 'repositories'' 'on'' '{%'' 'data'' 'variables.product.product_name'' '%},'' 'see'' '"Connecting'' 'to'' '{%'' 'data'' 'variables.product.prodname_dotcom'' '%}'' 'with'' 'SSH."Contributing'' 'to'' 'multiple'' 'accounts'' 'using'' 'HTTPS'' 'and'' 'PATs
Contributing'' 'to'' 'multiple'' 'accounts'' 'using'' 'HTTPS'' 'and'' '{%'' 'data'' 'variables.product.pat_generic'' '%}s
Alternatively,'' 'if'' 'you'' 'want'' 'to'' 'use'' 'the'' 'HTTPS'' 'protocol'' 'for'' 'both'' 'accounts,'' 'you'' 'can'' 'use'' 'different'' 'personal'' 'access'' 'tokens'' '(PAT)'' 'for'' 'each'' 'account'' 'by'' 'configuring'' 'Git'' 'to'' 'store'' 'different'' 'credentials'' 'for'' 'each'' 'repository.'' 'Alternatively,'' 'if'' 'you'' 'want'' 'to'' 'use'' 'the'' 'HTTPS'' 'protocol'' 'for'' 'both'' 'accounts,'' 'you'' 'can'' 'use'' 'different'' '{%'' 'data'' 'variables.product.pat_generic'' '%}s'' 'for'' 'each'' 'account'' 'by'' 'configuring'' 'Git'' 'to'' 'store'' 'different'' 'credentials'' 'for'' 'each'' 'repository.{%'' 'mac'' '%}4
...your''
'-cloud''
'-provider/deploying''
'-to''
'-azure/deploying''
'-docker''
'-to''
'-azure''
'-app''
'-service.md'' ''@'@'' '''
'-55,9'' '+55,9'' ''@'@'' 'Before'' 'creating'' 'your'' '{%'' 'data'' 'variables.product.prodname_actions'' '%}'' 'workflow,'' 'youSet'' 'registry'' 'credentials'' 'for'' 'your'' 'web'' 'app.Create'' 'a'' 'personal'' 'access'' 'token'' 'with'' 'the'' 'repo'' 'and'' 'read:packages'' 'scopes.'' 'For'' 'more'' 'information,'' 'see'' '"Creating'' 'a'' 'personal'' 'access'' 'token."'' 'Create'' 'a'' '{%'' 'data'' 'variables.product.pat_v1'' '%}'' 'with'' 'the'' 'repo'' 'and'' 'read:packages'' 'scopes.'' 'For'' 'more'' 'information,'' 'see'' '"Creating'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}."Set'' 'DOCKER_REGISTRY_SERVER_URL'' 'to'' 'https://ghcr.io,'' 'DOCKER_REGISTRY_SERVER_USERNAME'' 'to'' 'the'' 'GitHub'' 'username'' 'or'' 'organization'' 'that'' 'owns'' 'the'' 'repository,'' 'and'' 'DOCKER_REGISTRY_SERVER_PASSWORD'' 'to'' 'your'' 'personal'' 'access'' 'token'' 'from'' 'above.'' 'This'' 'will'' 'give'' 'your'' 'web'' 'app'' 'credentials'' 'so'' 'it'' 'can'' 'pull'' 'the'' 'container'' 'image'' 'after'' 'your'' 'workflow'' 'pushes'' 'a'' 'newly'' 'built'' 'image'' 'to'' 'the'' 'registry.'' 'You'' 'can'' 'do'' 'this'' 'with'' 'the'' 'following'' 'Azure'' 'CLI'' 'command:'' 'Set'' 'DOCKER_REGISTRY_SERVER_URL'' 'to'' 'https://ghcr.io,'' 'DOCKER_REGISTRY_SERVER_USERNAME'' 'to'' 'the'' 'GitHub'' 'username'' 'or'' 'organization'' 'that'' 'owns'' 'the'' 'repository,'' 'and'' 'DOCKER_REGISTRY_SERVER_PASSWORD'' 'to'' 'your'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'from'' 'above.'' 'This'' 'will'' 'give'' 'your'' 'web'' 'app'' 'credentials'' 'so'' 'it'' 'can'' 'pull'' 'the'' 'container'' 'image'' 'after'' 'your'' 'workflow'' 'pushes'' 'a'' 'newly'' 'built'' 'image'' 'to'' 'the'' 'registry.'' 'You'' 'can'' 'do'' 'this'' 'with'' 'the'' 'following'' 'Azure'' 'CLI'' 'command:'' 'az'' 'webapp'' 'config'' 'appsettings'' 'set'' '\
2
content/actions/examples/using''
'-concurrency''
'-expressions''
'-and''
'-a''
'-test.md'' ''@'@'' '''
'-112,7'' '+112,7'' ''@'@'' 'jobs:'' '#'' 'NOT'' 'clone'' 'them'' 'initially'' 'and'' 'instead,'' 'include'' 'them'' 'manually'' '#'' 'only'' 'for'' 'the'' 'test'' 'groups'' 'that'' 'we'' 'know'' 'need'' 'the'' 'files.'' 'lfs:'' '{%'' 'raw'' '%}${{'' '.test''
'-group'' '=='' ''content''' '}}{%'' 'endraw'' '%}'' '#'' 'Enables'' 'cloning'' 'the'' 'Early'' 'Access'' 'repo'' 'later'' 'with'' 'the'' 'relevant'' 'PAT'' '#'' 'Enables'' 'cloning'' 'the'' 'Early'' 'Access'' 'repo'' 'later'' 'with'' 'the'' 'relevant'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'persist''
'-credentials:'' ''false''' ''' 'name:'' 'Figure'' 'out'' 'which'' 'docs''
'-early''
'-access'' 'branch'' 'to'' 'checkout,'' 'if'' 'internal'' 'repo'' '2
.../hosting''
'-your''
'-own''
'-runners/monitoring''
'-and''
'-troubleshooting''
'-self''
'-hosted''
'-runners.md'' ''@'@'' '''
'-42,7'' '+42,7'' ''@'@'' 'You'' 'can'' 'use'' 'the'' 'self''
'-hosted'' 'runner'' 'application's'' 'run'' 'script'' 'with'' 'the'' '''
'-check'' 'In'' 'addition'' 'to'' '''
'-check,'' 'you'' 'must'' 'provide'' 'two'' 'arguments'' 'to'' 'the'' 'script:''
'-url'' 'with'' 'the'' 'URL'' 'to'' 'your'' '{%'' 'data'' 'variables.product.company_short'' '%}'' 'repository,'' 'organization,'' 'or'' 'enterprise.'' 'For'' 'example,'' '''
'-url'' 'https://github.com/octo''
'-org/octo''
'-repo.
''
'-pat'' 'with'' 'the'' 'value'' 'of'' 'a'' 'personal'' 'access'' 'token,'' 'which'' 'must'' 'have'' 'the'' 'workflow'' 'scope.'' 'For'' 'example,'' '''
'-pat'' 'ghp_abcd1234.'' 'For'' 'more'' 'information,'' 'see'' '"Creating'' 'a'' 'personal'' 'access'' 'token."
''
'-pat'' 'with'' 'the'' 'value'' 'of'' 'a'' '{%'' 'data'' 'variables.product.pat_v1'' '%},'' 'which'' 'must'' 'have'' 'the'' 'workflow'' 'scope{%'' 'ifversion'' 'pat''
'-v2%},'' 'or'' 'a'' '{%'' 'data'' 'variables.product.pat_v2'' '%}'' 'with'' 'workflows'' 'read'' 'and'' 'write'' 'access'' '{%'' 'endif'' '%}.'' 'For'' 'example,'' '''
'-pat'' 'ghp_abcd1234.'' 'For'' 'more'' 'information,'' 'see'' '"Creating'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}."
For'' 'example:4
...s/managing''
'-issues''
'-and''
'-pull''
'-requests/moving''
'-assigned''
'-issues''
'-on''
'-project''
'-boards.md'' ''@'@'' '''
'-56,8'' '+56,8'' ''@'@'' 'In'' 'the'' 'tutorial,'' 'you'' 'will'' 'first'' 'make'' 'a'' 'workflow'' 'file'' 'that'' 'uses'' 'the'' '[`alex''
'-page/gChange'' 'the'' 'value'' 'for'' 'project'' 'to'' 'the'' 'name'' 'of'' 'your'' 'project'' 'board.'' 'If'' 'you'' 'have'' 'multiple'' 'project'' 'boards'' 'with'' 'the'' 'same'' 'name,'' 'the'' 'alex''
'-page/github''
'-project''
'-automation''
'-plus'' 'action'' 'will'' 'act'' 'on'' 'all'' 'projects'' 'with'' 'the'' 'specified'' 'name.
Change'' 'the'' 'value'' 'for'' 'column'' 'to'' 'the'' 'name'' 'of'' 'the'' 'column'' 'where'' 'you'' 'want'' 'issues'' 'to'' 'move'' 'when'' 'they'' 'are'' 'assigned.
Change'' 'the'' 'value'' 'for'' 'repo''
'-token:
Create'' 'a'' 'personal'' 'access'' 'token'' 'with'' 'the'' 'repo'' 'scope.'' 'For'' 'more'' 'information,'' 'see'' '"Creating'' 'a'' 'personal'' 'access'' 'token."
Store'' 'this'' 'personal'' 'access'' 'token'' 'as'' 'a'' 'secret'' 'in'' 'your'' 'repository.'' 'For'' 'more'' 'information'' 'about'' 'storing'' 'secrets,'' 'see'' '"Encrypted'' 'secrets."
Create'' 'a'' '{%'' 'data'' 'variables.product.pat_v1'' '%}'' 'with'' 'the'' 'repo'' 'scope.'' 'For'' 'more'' 'information,'' 'see'' '"Creating'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}."
Store'' 'this'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'as'' 'a'' 'secret'' 'in'' 'your'' 'repository.'' 'For'' 'more'' 'information'' 'about'' 'storing'' 'secrets,'' 'see'' '"Encrypted'' 'secrets."
In'' 'your'' 'workflow'' 'file,'' 'replace'' 'PERSONAL_ACCESS_TOKEN'' 'with'' 'the'' 'name'' 'of'' 'your'' 'secret.
{%'' 'data'' 'reusables.actions.commit''
'-workflow'' '%}
2
content/actions/publishing''
'-packages/publishing''
'-nodejs''
'-packages.md'' ''@'@'' '''
'-115,7'' '+115,7'' ''@'@'' 'If'' 'you'' 'do'' 'provide'' 'the'' 'repository'' 'key'' 'in'' 'your'' 'package.json'' 'file,'' 'then'' 'the'' 'rep'' 'To'' 'perform'' 'authenticated'' 'operations'' 'against'' 'the'' '{%'' 'data'' 'variables.product.prodname_registry'' '%}'' 'registry'' 'in'' 'your'' 'workflow,'' 'you'' 'can'' 'use'' 'the'' 'GITHUB_TOKEN.'' '{%'' 'data'' 'reusables.actions.github''
'-token''
'-permissions'' '%}'' 'If'' 'you'' 'want'' 'to'' 'publish'' 'your'' 'package'' 'to'' 'a'' 'different'' 'repository,'' 'you'' 'must'' 'use'' 'a'' 'personal'' 'access'' 'token'' '(PAT)'' 'that'' 'has'' 'permission'' 'to'' 'write'' 'to'' 'packages'' 'in'' 'the'' 'destination'' 'repository.'' 'For'' 'more'' 'information,'' 'see'' '"Creating'' 'a'' 'personal'' 'access'' 'token"'' 'and'' '"Encrypted'' 'secrets."'' 'If'' 'you'' 'want'' 'to'' 'publish'' 'your'' 'package'' 'to'' 'a'' 'different'' 'repository,'' 'you'' 'must'' 'use'' 'a'' '{%'' 'data'' 'variables.product.pat_v1'' '%}'' 'that'' 'has'' 'permission'' 'to'' 'write'' 'to'' 'packages'' 'in'' 'the'' 'destination'' 'repository.'' 'For'' 'more'' 'information,'' 'see'' '"Creating'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}"'' 'and'' '"Encrypted'' 'secrets."Example'' 'workflow
4
content/actions/security''
'-guides/automatic''
'-token''
'-authentication.md'' ''@'@'' '''
'-117,9'' '+117,9'' ''@'@'' 'The'' 'permissions'' 'for'' 'the'' 'GITHUB_TOKEN'' 'are'' 'initially'' 'set'' 'to'' 'the'' 'default'' 'settingGranting'' 'additional'' 'permissions
If'' 'you'' 'need'' 'a'' 'token'' 'that'' 'requires'' 'permissions'' 'that'' 'aren't'' 'available'' 'in'' 'the'' 'GITHUB_TOKEN,'' 'you'' 'can'' 'create'' 'a'' 'personal'' 'access'' 'token'' 'and'' 'set'' 'it'' 'as'' 'a'' 'secret'' 'in'' 'your'' 'repository:'' 'If'' 'you'' 'need'' 'a'' 'token'' 'that'' 'requires'' 'permissions'' 'that'' 'aren't'' 'available'' 'in'' 'the'' 'GITHUB_TOKEN,'' 'you'' 'can'' 'create'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'and'' 'set'' 'it'' 'as'' 'a'' 'secret'' 'in'' 'your'' 'repository:Use'' 'or'' 'create'' 'a'' 'token'' 'with'' 'the'' 'appropriate'' 'permissions'' 'for'' 'that'' 'repository.'' 'For'' 'more'' 'information,'' 'see'' '"Creating'' 'a'' 'personal'' 'access'' 'token."
Use'' 'or'' 'create'' 'a'' 'token'' 'with'' 'the'' 'appropriate'' 'permissions'' 'for'' 'that'' 'repository.'' 'For'' 'more'' 'information,'' 'see'' '"Creating'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}."
Add'' 'the'' 'token'' 'as'' 'a'' 'secret'' 'in'' 'your'' 'workflow's'' 'repository,'' 'and'' 'refer'' 'to'' 'it'' 'using'' 'the'' '{%raw%}${{'' 'secrets.SECRET_NAME'' '}}{%'' 'endraw'' '%}'' 'syntax.'' 'For'' 'more'' 'information,'' 'see'' '"Creating'' 'and'' 'using'' 'encrypted'' 'secrets."
Further'' 'reading
2
content/actions/security''
'-guides/encrypted''
'-secrets.md'' ''@'@'' '''
'-60,7'' '+60,7'' ''@'@'' 'You'' 'can'' 'also'' 'manage'' 'secrets'' 'using'' 'the'' 'REST'' 'API.'' 'For'' 'more'' 'information,'' 'see'' '"[SecrLimiting'' 'credential'' 'permissions
When'' 'generating'' 'credentials,'' 'we'' 'recommend'' 'that'' 'you'' 'grant'' 'the'' 'minimum'' 'permissions'' 'possible.'' 'For'' 'example,'' 'instead'' 'of'' 'using'' 'personal'' 'credentials,'' 'use'' 'deploy'' 'keys'' 'or'' 'a'' 'service'' 'account.'' 'Consider'' 'granting'' 'read''
'-only'' 'permissions'' 'if'' 'that's'' 'all'' 'that'' 'is'' 'needed,'' 'and'' 'limit'' 'access'' 'as'' 'much'' 'as'' 'possible.'' 'When'' 'generating'' 'a'' 'personal'' 'access'' 'token'' '(PAT),'' 'select'' 'the'' 'fewest'' 'scopes'' 'necessary.'' 'When'' 'generating'' 'credentials,'' 'we'' 'recommend'' 'that'' 'you'' 'grant'' 'the'' 'minimum'' 'permissions'' 'possible.'' 'For'' 'example,'' 'instead'' 'of'' 'using'' 'personal'' 'credentials,'' 'use'' 'deploy'' 'keys'' 'or'' 'a'' 'service'' 'account.'' 'Consider'' 'granting'' 'read''
'-only'' 'permissions'' 'if'' 'that's'' 'all'' 'that'' 'is'' 'needed,'' 'and'' 'limit'' 'access'' 'as'' 'much'' 'as'' 'possible.'' 'When'' 'generating'' 'a'' '{%'' 'data'' 'variables.product.pat_v1'' '%},'' 'select'' 'the'' 'fewest'' 'scopes'' 'necessary.{%'' 'ifversion'' 'pat''
'-v2'' '%}'' 'When'' 'generating'' 'a'' '{%'' 'data'' 'variables.product.pat_v2'' '%},'' 'select'' 'the'' 'minimum'' 'repository'' 'access'' 'required.{%'' 'endif'' '%}{%'' 'note'' '%}8
content/actions/security''
'-guides/security''
'-hardening''
'-for''
'-github''
'-actions.md'' ''@'@'' '''
'-261,11'' '+261,11'' ''@'@'' 'This'' 'list'' 'describes'' 'the'' 'recommended'' 'approaches'' 'for'' 'accessing'' 'repository'' 'data'' 'wit'' ''' 'Note'' 'that'' 'deploy'' 'keys'' 'can'' 'only'' 'clone'' 'and'' 'push'' 'to'' 'the'' 'repository'' 'using'' 'Git,'' 'and'' 'cannot'' 'be'' 'used'' 'to'' 'interact'' 'with'' 'the'' 'REST'' 'or'' 'GraphQL'' 'API,'' 'so'' 'they'' 'may'' 'not'' 'be'' 'appropriate'' 'for'' 'your'' 'requirements.'' '3.'' '{%'' 'data'' 'variables.product.prodname_github_app'' '%}'' 'tokens'' ''' '{%'' 'data'' 'variables.product.prodname_github_apps'' '%}'' 'can'' 'be'' 'installed'' 'on'' 'select'' 'repositories,'' 'and'' 'even'' 'have'' 'granular'' 'permissions'' 'on'' 'the'' 'resources'' 'within'' 'them.'' 'You'' 'could'' 'create'' 'a'' '{%'' 'data'' 'variables.product.prodname_github_app'' '%}'' 'internal'' 'to'' 'your'' 'organization,'' 'install'' 'it'' 'on'' 'the'' 'repositories'' 'you'' 'need'' 'access'' 'to'' 'within'' 'your'' 'workflow,'' 'and'' 'authenticate'' 'as'' 'the'' 'installation'' 'within'' 'your'' 'workflow'' 'to'' 'access'' 'those'' 'repositories.'' '4.'' 'Personal'' 'access'' 'tokens'' ''' 'You'' 'should'' 'never'' 'use'' 'personal'' 'access'' 'tokens'' 'from'' 'your'' 'own'' 'account.'' 'These'' 'tokens'' 'grant'' 'access'' 'to'' 'all'' 'repositories'' 'within'' 'the'' 'organizations'' 'that'' 'you'' 'have'' 'access'' 'to,'' 'as'' 'well'' 'as'' 'all'' 'personal'' 'repositories'' 'in'' 'your'' 'personal'' 'account.'' 'This'' 'indirectly'' 'grants'' 'broad'' 'access'' 'to'' 'all'' 'write''
'-access'' 'users'' 'of'' 'the'' 'repository'' 'the'' 'workflow'' 'is'' 'in.'' 'In'' 'addition,'' 'if'' 'you'' 'later'' 'leave'' 'an'' 'organization,'' 'workflows'' 'using'' 'this'' 'token'' 'will'' 'immediately'' 'break,'' 'and'' 'debugging'' 'this'' 'issue'' 'can'' 'be'' 'challenging.'' ''' 'If'' 'a'' 'personal'' 'access'' 'token'' 'is'' 'used,'' 'it'' 'should'' 'be'' 'one'' 'that'' 'was'' 'generated'' 'for'' 'a'' 'new'' 'account'' 'that'' 'is'' 'only'' 'granted'' 'access'' 'to'' 'the'' 'specific'' 'repositories'' 'that'' 'are'' 'needed'' 'for'' 'the'' 'workflow.'' 'Note'' 'that'' 'this'' 'approach'' 'is'' 'not'' 'scalable'' 'and'' 'should'' 'be'' 'avoided'' 'in'' 'favor'' 'of'' 'alternatives,'' 'such'' 'as'' 'deploy'' 'keys.'' '4.'' '{%'' 'data'' 'variables.product.pat_generic'' '%}s'' ''' 'You'' 'should'' 'never'' 'use'' 'a'' '{%'' 'data'' 'variables.product.pat_v1'' '%}.'' 'These'' 'tokens'' 'grant'' 'access'' 'to'' 'all'' 'repositories'' 'within'' 'the'' 'organizations'' 'that'' 'you'' 'have'' 'access'' 'to,'' 'as'' 'well'' 'as'' 'all'' 'personal'' 'repositories'' 'in'' 'your'' 'personal'' 'account.'' 'This'' 'indirectly'' 'grants'' 'broad'' 'access'' 'to'' 'all'' 'write''
'-access'' 'users'' 'of'' 'the'' 'repository'' 'the'' 'workflow'' 'is'' 'in.'' ''' 'If'' 'you'' 'do'' 'use'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%},'' 'you'' 'should'' 'never'' 'use'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'from'' 'your'' 'own'' 'account.'' 'If'' 'you'' 'later'' 'leave'' 'an'' 'organization,'' 'workflows'' 'using'' 'this'' 'token'' 'will'' 'immediately'' 'break,'' 'and'' 'debugging'' 'this'' 'issue'' 'can'' 'be'' 'challenging.'' 'Instead,'' 'you'' 'should'' 'use'' 'a'' '{%'' 'ifversion'' 'pat''
'-v2%}{%'' 'data'' 'variables.product.pat_v2'' '%}s{%'' 'else'' '%}{%'' 'data'' 'variables.product.pat_generic'' '%}s{%'' 'endif'' '%}'' 'for'' 'a'' 'new'' 'account'' 'that'' 'belongs'' 'to'' 'your'' 'organization'' 'and'' 'that'' 'is'' 'only'' 'granted'' 'access'' 'to'' 'the'' 'specific'' 'repositories'' 'that'' 'are'' 'needed'' 'for'' 'the'' 'workflow.'' 'Note'' 'that'' 'this'' 'approach'' 'is'' 'not'' 'scalable'' 'and'' 'should'' 'be'' 'avoided'' 'in'' 'favor'' 'of'' 'alternatives,'' 'such'' 'as'' 'deploy'' 'keys.'' '5.'' 'SSH'' 'keys'' 'on'' 'a'' 'personal'' 'account'' ''' 'Workflows'' 'should'' 'never'' 'use'' 'the'' 'SSH'' 'keys'' 'on'' 'a'' 'personal'' 'account.'' 'Similar'' 'to'' 'personal'' 'access'' 'tokens,'' 'they'' 'grant'' 'read/write'' 'permissions'' 'to'' 'all'' 'of'' 'your'' 'personal'' 'repositories'' 'as'' 'well'' 'as'' 'all'' 'the'' 'repositories'' 'you'' 'have'' 'access'' 'to'' 'through'' 'organization'' 'membership.'' 'This'' 'indirectly'' 'grants'' 'broad'' 'access'' 'to'' 'all'' 'write''
'-access'' 'users'' 'of'' 'the'' 'repository'' 'the'' 'workflow'' 'is'' 'in.'' 'If'' 'you're'' 'intending'' 'to'' 'use'' 'an'' 'SSH'' 'key'' 'because'' 'you'' 'only'' 'need'' 'to'' 'perform'' 'repository'' 'clones'' 'or'' 'pushes,'' 'and'' 'do'' 'not'' 'need'' 'to'' 'interact'' 'with'' 'public'' 'APIs,'' 'then'' 'you'' 'should'' 'use'' 'individual'' 'deploy'' 'keys'' 'instead.'' ''' 'Workflows'' 'should'' 'never'' 'use'' 'the'' 'SSH'' 'keys'' 'on'' 'a'' 'personal'' 'account.'' 'Similar'' 'to'' '{%'' 'data'' 'variables.product.pat_v1_plural'' '%},'' 'they'' 'grant'' 'read/write'' 'permissions'' 'to'' 'all'' 'of'' 'your'' 'personal'' 'repositories'' 'as'' 'well'' 'as'' 'all'' 'the'' 'repositories'' 'you'' 'have'' 'access'' 'to'' 'through'' 'organization'' 'membership.'' 'This'' 'indirectly'' 'grants'' 'broad'' 'access'' 'to'' 'all'' 'write''
'-access'' 'users'' 'of'' 'the'' 'repository'' 'the'' 'workflow'' 'is'' 'in.'' 'If'' 'you're'' 'intending'' 'to'' 'use'' 'an'' 'SSH'' 'key'' 'because'' 'you'' 'only'' 'need'' 'to'' 'perform'' 'repository'' 'clones'' 'or'' 'pushes,'' 'and'' 'do'' 'not'' 'need'' 'to'' 'interact'' 'with'' 'public'' 'APIs,'' 'then'' 'you'' 'should'' 'use'' 'individual'' 'deploy'' 'keys'' 'instead.Hardening'' 'for'' 'self''
'-hosted'' 'runners
4
content/actions/using''
'-workflows/triggering''
'-a''
'-workflow.md'' ''@'@'' '''
'-36,9'' '+36,9'' ''@'@'' 'The'' 'following'' 'steps'' 'occur'' 'to'' 'trigger'' 'a'' 'workflow'' 'run:{%'' 'data'' 'reusables.actions.actions''
'-do''
'-not''
'-trigger''
'-workflows'' '%}'' 'For'' 'more'' 'information,'' 'see'' '"Authenticating'' 'with'' 'the'' 'GITHUB_TOKEN."If'' 'you'' 'do'' 'want'' 'to'' 'trigger'' 'a'' 'workflow'' 'from'' 'within'' 'a'' 'workflow'' 'run,'' 'you'' 'can'' 'use'' 'a'' 'personal'' 'access'' 'token'' 'instead'' 'of'' 'GITHUB_TOKEN'' 'to'' 'trigger'' 'events'' 'that'' 'require'' 'a'' 'token.'' 'You'll'' 'need'' 'to'' 'create'' 'a'' 'personal'' 'access'' 'token'' 'and'' 'store'' 'it'' 'as'' 'a'' 'secret.'' 'To'' 'minimize'' 'your'' '{%'' 'data'' 'variables.product.prodname_actions'' '%}'' 'usage'' 'costs,'' 'ensure'' 'that'' 'you'' 'don't'' 'create'' 'recursive'' 'or'' 'unintended'' 'workflow'' 'runs.'' 'For'' 'more'' 'information'' 'about'' 'creating'' 'a'' 'personal'' 'access'' 'token,'' 'see'' '"Creating'' 'a'' 'personal'' 'access'' 'token."'' 'For'' 'more'' 'information'' 'about'' 'storing'' 'a'' 'personal'' 'access'' 'token'' 'as'' 'a'' 'secret,'' 'see'' '"Creating'' 'and'' 'storing'' 'encrypted'' 'secrets."'' 'If'' 'you'' 'do'' 'want'' 'to'' 'trigger'' 'a'' 'workflow'' 'from'' 'within'' 'a'' 'workflow'' 'run,'' 'you'' 'can'' 'use'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'instead'' 'of'' 'GITHUB_TOKEN'' 'to'' 'trigger'' 'events'' 'that'' 'require'' 'a'' 'token.'' 'You'll'' 'need'' 'to'' 'create'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'and'' 'store'' 'it'' 'as'' 'a'' 'secret.'' 'To'' 'minimize'' 'your'' '{%'' 'data'' 'variables.product.prodname_actions'' '%}'' 'usage'' 'costs,'' 'ensure'' 'that'' 'you'' 'don't'' 'create'' 'recursive'' 'or'' 'unintended'' 'workflow'' 'runs.'' 'For'' 'more'' 'information'' 'about'' 'creating'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%},'' 'see'' '"Creating'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}."'' 'For'' 'more'' 'information'' 'about'' 'storing'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'as'' 'a'' 'secret,'' 'see'' '"Creating'' 'and'' 'storing'' 'encrypted'' 'secrets."For'' 'example,'' 'the'' 'following'' 'workflow'' 'uses'' 'a'' 'personal'' 'access'' 'token'' '(stored'' 'as'' 'a'' 'secret'' 'called'' 'MY_TOKEN)'' 'to'' 'add'' 'a'' 'label'' 'to'' 'an'' 'issue'' 'via'' '{%'' 'data'' 'variables.product.prodname_cli'' '%}.'' 'Any'' 'workflows'' 'that'' 'run'' 'when'' 'a'' 'label'' 'is'' 'added'' 'will'' 'run'' 'once'' 'this'' 'step'' 'is'' 'performed.'' 'For'' 'example,'' 'the'' 'following'' 'workflow'' 'uses'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' '(stored'' 'as'' 'a'' 'secret'' 'called'' 'MY_TOKEN)'' 'to'' 'add'' 'a'' 'label'' 'to'' 'an'' 'issue'' 'via'' '{%'' 'data'' 'variables.product.prodname_cli'' '%}.'' 'Any'' 'workflows'' 'that'' 'run'' 'when'' 'a'' 'label'' 'is'' 'added'' 'will'' 'run'' 'once'' 'this'' 'step'' 'is'' 'performed.on:
'' ''' '2'' ''' '
content/actions/using''
'-workflows/workflow''
'-syntax''
'-for''
'-github''
'-actions.md
'@'@'' '''
'-497,7'' '+497,7'' ''@'@'' 'jobs:####'' 'Example:'' 'Using'' 'an'' 'action'' 'inside'' 'a'' 'different'' 'private'' 'repository'' 'than'' 'the'' 'workflowYour'' 'workflow'' 'must'' 'checkout'' 'the'' 'private'' 'repository'' 'and'' 'reference'' 'the'' 'action'' 'locally.'' 'Generate'' 'a'' 'personal'' 'access'' 'token'' 'and'' 'add'' 'the'' 'token'' 'as'' 'an'' 'encrypted'' 'secret.'' 'For'' 'more'' 'information,'' 'see'' '"[Creating'' 'a'' 'personal'' 'access'' 'token](/github/authenticating''
'-to''
'-github/creating''
'-a''
'-personal''
'-access''
'-token)"'' 'and'' '"[Encrypted'' 'secrets](/actions/reference/encrypted''
'-secrets)."
Your'' 'workflow'' 'must'' 'checkout'' 'the'' 'private'' 'repository'' 'and'' 'reference'' 'the'' 'action'' 'locally.'' 'Generate'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'and'' 'add'' 'the'' 'token'' 'as'' 'an'' 'encrypted'' 'secret.'' 'For'' 'more'' 'information,'' 'see'' '"[Creating'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}](/github/authenticating''
'-to''
'-github/creating''
'-a''
'-personal''
'-access''
'-token)"'' 'and'' '"[Encrypted'' 'secrets](/actions/reference/encrypted''
'-secrets)."Replace'' '`PERSONAL_ACCESS_TOKEN`'' 'in'' 'the'' 'example'' 'with'' 'the'' 'name'' 'of'' 'your'' 'secret.'' ''' '2'' ''' '
content/admin/configuration/configuring''
'-your''
'-enterprise/site''
'-admin''
'-dashboard.md
'@'@'' '''
'-62,7'' '+62,7'' ''@'@'' 'Specifically,'' 'you'' 'can'' 'download'' 'CSV'' 'reports'' 'that'' 'list
'' 'all'' 'organizations
'' 'all'' 'repositoriesYou'' 'can'' 'also'' 'access'' 'these'' 'reports'' 'programmatically'' 'via'' 'standard'' 'HTTP'' 'authentication'' 'with'' 'a'' 'site'' 'admin'' 'account.'' 'You'' 'must'' 'use'' 'a'' 'personal'' 'access'' 'token'' 'with'' 'the'' '`site_admin`'' 'scope.'' 'For'' 'more'' 'information,'' 'see'' '"[Creating'' 'a'' 'personal'' 'access'' 'token](/github/authenticating''
'-to''
'-github/creating''
'-a''
'-personal''
'-access''
'-token)."
You'' 'can'' 'also'' 'access'' 'these'' 'reports'' 'programmatically'' 'via'' 'standard'' 'HTTP'' 'authentication'' 'with'' 'a'' 'site'' 'admin'' 'account.'' 'You'' 'must'' 'use'' 'a'' '{%'' 'data'' 'variables.product.pat_v1'' '%}'' 'with'' 'the'' '`site_admin`'' 'scope.'' 'For'' 'more'' 'information,'' 'see'' '"[Creating'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}](/github/authenticating''
'-to''
'-github/creating''
'-a''
'-personal''
'-access''
'-token)."For'' 'example,'' 'here'' 'is'' 'how'' 'you'' 'would'' 'download'' 'the'' '"all'' 'users"'' 'report'' 'using'' 'cURL:'' ''' '4'' ''' '
...ing''
'-access''
'-to''
'-actions''
'-from''
'-githubcom/manually''
'-syncing''
'-actions''
'-from''
'-githubcom.md
'@'@'' '''
'-44,7'' '+44,7'' ''@'@'' 'The'' '`actions''
'-sync`'' 'tool'' 'can'' 'only'' 'download'' 'actions'' 'from'' '{%'' 'data'' 'variables.product
##'' 'Prerequisites*'' 'Before'' 'using'' 'the'' '`actions''
'-sync`'' 'tool,'' 'you'' 'must'' 'ensure'' 'that'' 'all'' 'destination'' 'organizations'' 'already'' 'exist'' 'in'' 'your'' 'enterprise.'' 'The'' 'following'' 'example'' 'demonstrates'' 'how'' 'to'' 'sync'' 'actions'' 'to'' 'an'' 'organization'' 'named'' '`synced''
'-actions`.'' 'For'' 'more'' 'information,'' 'see'' '"[Creating'' 'a'' 'new'' 'organization'' 'from'' 'scratch](/organizations/collaborating''
'-with''
'-groups''
'-in''
'-organizations/creating''
'-a''
'-new''
'-organization''
'-from''
'-scratch)."
*'' 'You'' 'must'' 'create'' 'a'' 'personal'' 'access'' 'token'' '(PAT)'' 'on'' 'your'' 'enterprise'' 'that'' 'can'' 'create'' 'and'' 'write'' 'to'' 'repositories'' 'in'' 'the'' 'destination'' 'organizations.'' 'For'' 'more'' 'information,'' 'see'' '"[Creating'' 'a'' 'personal'' 'access'' 'token](/github/authenticating''
'-to''
'-github/creating''
'-a''
'-personal''
'-access''
'-token)."{%'' 'ifversion'' 'ghes'' '%}
*'' 'You'' 'must'' 'create'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'on'' 'your'' 'enterprise'' 'that'' 'can'' 'create'' 'and'' 'write'' 'to'' 'repositories'' 'in'' 'the'' 'destination'' 'organizations.'' 'For'' 'more'' 'information,'' 'see'' '"[Creating'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}](/github/authenticating''
'-to''
'-github/creating''
'-a''
'-personal''
'-access''
'-token)."{%'' 'ifversion'' 'ghes'' '%}
*'' 'If'' 'you'' 'want'' 'to'' 'sync'' 'the'' 'bundled'' 'actions'' 'in'' 'the'' '`actions`'' 'organization'' 'on'' '{%'' 'data'' 'variables.location.product_location'' '%},'' 'you'' 'must'' 'be'' 'an'' 'owner'' 'of'' 'the'' '`actions`'' 'organization.'' ''' '{%'' 'note'' '%}
'@'@'' '''
'-84,7'' '+84,7'' ''@'@'' 'This'' 'example'' 'demonstrates'' 'using'' 'the'' '`actions''
'-sync`'' 'tool'' 'to'' 'sync'' 'an'' 'individual'' 'ac
'' ''' ''' 'The'' 'above'' 'command'' 'uses'' 'the'' 'following'' 'arguments:'' ''' ''' '*'' '`''
'-cache''
'-dir`:'' 'The'' 'cache'' 'directory'' 'on'' 'the'' 'machine'' 'running'' 'the'' 'command.
'' ''' ''' '*'' '`''
'-destination''
'-token`:'' 'A'' 'personal'' 'access'' 'token'' 'for'' 'the'' 'destination'' 'enterprise'' 'instance.
'' ''' ''' '*'' '`''
'-destination''
'-token`:'' 'A'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'for'' 'the'' 'destination'' 'enterprise'' 'instance.
'' ''' ''' '*'' '`''
'-destination''
'-url`:'' 'The'' 'URL'' 'of'' 'the'' 'destination'' 'enterprise'' 'instance.
'' ''' ''' '*'' '`''
'-repo''
'-name`:'' 'The'' 'action'' 'repository'' 'to'' 'sync.'' 'This'' 'takes'' 'the'' 'format'' 'of'' '`owner/repository:destination_owner/destination_repository`.'' ''' '4'' ''' '
...''
'-management/managing''
'-iam''
'-for''
'-your''
'-enterprise/changing''
'-authentication''
'-methods.md
'@'@'' '''
'-33,9'' '+33,9'' ''@'@'' 'Other'' 'issues'' 'you'' 'should'' 'take'' 'into'' 'consideration'' 'include:*'' '**Group'' 'membership:**'' 'When'' 'you'' 'use'' 'LDAP'' 'to'' 'authenticate,'' 'users'' 'are'' 'automatically'' '[suspended'' 'and'' 'unsuspended](/enterprise/admin/guides/user''
'-management/suspending''
'-and''
'-unsuspending''
'-users)'' 'based'' 'on'' 'restricted'' 'group'' 'membership'' 'and'' 'account'' 'status'' 'with'' 'Active'' 'Directory.*'' '**Git'' 'authentication:**'' 'SAML'' 'and'' 'CAS'' 'only'' 'supports'' 'Git'' 'authentication'' 'over'' 'HTTP'' 'or'' 'HTTPS'' 'using'' 'a'' '[personal'' 'access'' 'token](/articles/creating''
'-an''
'-access''
'-token''
'-for''
'-command''
'-line''
'-use).'' 'Password'' 'authentication'' 'over'' 'HTTP'' 'or'' 'HTTPS'' 'is'' 'not'' 'supported.'' 'LDAP'' 'supports'' 'password''
'-based'' 'Git'' 'authentication'' 'by'' 'default,'' 'but'' 'we'' 'recommend'' 'that'' 'you'' '[disable'' 'that'' 'method](/enterprise/admin/authentication/using''
'-ldap#disabling''
'-password''
'-authentication''
'-for''
'-git''
'-operations)'' 'and'' 'force'' 'authentication'' 'via'' 'a'' 'personal'' 'access'' 'token'' 'or'' 'SSH'' 'key.
*'' '**Git'' 'authentication:**'' 'SAML'' 'and'' 'CAS'' 'only'' 'supports'' 'Git'' 'authentication'' 'over'' 'HTTP'' 'or'' 'HTTPS'' 'using'' 'a'' '[{%'' 'data'' 'variables.product.pat_generic'' '%}](/articles/creating''
'-an''
'-access''
'-token''
'-for''
'-command''
'-line''
'-use).'' 'Password'' 'authentication'' 'over'' 'HTTP'' 'or'' 'HTTPS'' 'is'' 'not'' 'supported.'' 'LDAP'' 'supports'' 'password''
'-based'' 'Git'' 'authentication'' 'by'' 'default,'' 'but'' 'we'' 'recommend'' 'that'' 'you'' '[disable'' 'that'' 'method](/enterprise/admin/authentication/using''
'-ldap#disabling''
'-password''
'-authentication''
'-for''
'-git''
'-operations)'' 'and'' 'force'' 'authentication'' 'via'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'or'' 'SSH'' 'key.*'' '**API'' 'authentication:**'' 'SAML'' 'and'' 'CAS'' 'only'' 'supports'' 'API'' 'authentication'' 'using'' 'a'' '[personal'' 'access'' 'token](/articles/creating''
'-an''
'-access''
'-token''
'-for''
'-command''
'-line''
'-use).'' 'Basic'' 'authentication'' 'is'' 'not'' 'supported.
*'' '**API'' 'authentication:**'' 'SAML'' 'and'' 'CAS'' 'only'' 'supports'' 'API'' 'authentication'' 'using'' 'a'' '[{%'' 'data'' 'variables.product.pat_generic'' '%}](/articles/creating''
'-an''
'-access''
'-token''
'-for''
'-command''
'-line''
'-use).'' 'Basic'' 'authentication'' 'is'' 'not'' 'supported.*'' '**Two''
'-factor'' 'authentication:**'' '{%'' 'data'' 'reusables.enterprise_user_management.external_auth_disables_2fa'' '%}'' ''' '2'' ''' '
.../admin/identity''
'-and''
'-access''
'-management/using''
'-cas''
'-for''
'-enterprise''
'-iam/using''
'-cas.md
'@'@'' '''
'-24,7'' '+24,7'' ''@'@'' 'topics:CAS'' 'is'' 'a'' 'single'' 'sign''
'-on'' '(SSO)'' 'protocol'' 'that'' 'centralizes'' 'authentication'' 'to'' 'multiple'' 'web'' 'applications.'' 'For'' 'more'' 'information,'' 'see'' '"[Central'' 'Authentication'' 'Service](https://en.wikipedia.org/wiki/Central_Authentication_Service)"'' 'on'' 'Wikipedia.After'' 'you'' 'configure'' 'CAS,'' 'people'' 'who'' 'use'' '{%'' 'data'' 'variables.location.product_location'' '%}'' 'must'' 'use'' 'a'' 'personal'' 'access'' 'token'' 'to'' 'authenticate'' 'API'' 'or'' 'Git'' 'requests'' 'over'' 'HTTP(S).'' 'CAS'' 'credentials'' 'cannot'' 'be'' 'used'' 'to'' 'authenticate'' 'these'' 'requests.'' 'For'' 'more'' 'information,'' 'see'' '"[Creating'' 'a'' 'personal'' 'access'' 'token](/authentication/keeping''
'-your''
'-account''
'-and''
'-data''
'-secure/creating''
'-a''
'-personal''
'-access''
'-token)."
After'' 'you'' 'configure'' 'CAS,'' 'people'' 'who'' 'use'' '{%'' 'data'' 'variables.location.product_location'' '%}'' 'must'' 'use'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'to'' 'authenticate'' 'API'' 'or'' 'Git'' 'requests'' 'over'' 'HTTP(S).'' 'CAS'' 'credentials'' 'cannot'' 'be'' 'used'' 'to'' 'authenticate'' 'these'' 'requests.'' 'For'' 'more'' 'information,'' 'see'' '"[Creating'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}](/authentication/keeping''
'-your''
'-account''
'-and''
'-data''
'-secure/creating''
'-a''
'-personal''
'-access''
'-token)."If'' 'you'' 'configure'' 'CAS,'' 'people'' 'with'' 'accounts'' 'on'' 'your'' 'identity'' 'provider'' '(IdP)'' 'do'' 'not'' 'consume'' 'a'' 'user'' 'license'' 'until'' 'the'' 'person'' 'signs'' 'into'' '{%'' 'data'' 'variables.location.product_location'' '%}.'' ''' '4'' ''' '
...''
'-managed''
'-users''
'-for''
'-iam/about''
'-support''
'-for''
'-your''
'-idps''
'-conditional''
'-access''
'-policy.md
'@'@'' '''
'-36,9'' '+36,9'' ''@'@'' 'For'' 'more'' 'information'' 'about'' 'using'' 'OIDC'' 'with'' '{%'' 'data'' 'variables.product.prodname_em###'' '{%'' 'data'' 'variables.product.prodname_actions'' '%}Actions'' 'that'' 'use'' 'a'' 'personal'' 'access'' 'token'' 'will'' 'likely'' 'be'' 'blocked'' 'by'' 'your'' 'IdP's'' 'CAP.'' 'We'' 'recommend'' 'that'' 'personal'' 'access'' 'tokens'' 'are'' 'created'' 'by'' 'a'' 'service'' 'account'' 'which'' 'is'' 'then'' 'exempted'' 'from'' 'IP'' 'controls'' 'in'' 'your'' 'IdP's'' 'CAP.'' '
Actions'' 'that'' 'use'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'will'' 'likely'' 'be'' 'blocked'' 'by'' 'your'' 'IdP's'' 'CAP.'' 'We'' 'recommend'' 'that'' '{%'' 'data'' 'variables.product.pat_generic'' '%}s'' 'are'' 'created'' 'by'' 'a'' 'service'' 'account'' 'which'' 'is'' 'then'' 'exempted'' 'from'' 'IP'' 'controls'' 'in'' 'your'' 'IdP's'' 'CAP.'' 'If'' 'you're'' 'unable'' 'to'' 'use'' 'a'' 'service'' 'account,'' 'another'' 'option'' 'for'' 'unblocking'' 'actions'' 'that'' 'use'' 'personal'' 'access'' 'tokens'' 'is'' 'to'' 'allow'' 'the'' 'IP'' 'ranges'' 'used'' 'by'' '{%'' 'data'' 'variables.product.prodname_actions'' '%}.'' 'For'' 'more'' 'information,'' 'see'' '"[About'' 'GitHub's'' 'IP'' 'addresses](/authentication/keeping''
'-your''
'-account''
'-and''
'-data''
'-secure/about''
'-githubs''
'-ip''
'-addresses)."
If'' 'you're'' 'unable'' 'to'' 'use'' 'a'' 'service'' 'account,'' 'another'' 'option'' 'for'' 'unblocking'' 'actions'' 'that'' 'use'' '{%'' 'data'' 'variables.product.pat_generic'' '%}s'' 'is'' 'to'' 'allow'' 'the'' 'IP'' 'ranges'' 'used'' 'by'' '{%'' 'data'' 'variables.product.prodname_actions'' '%}.'' 'For'' 'more'' 'information,'' 'see'' '"[About'' 'GitHub's'' 'IP'' 'addresses](/authentication/keeping''
'-your''
'-account''
'-and''
'-data''
'-secure/about''
'-githubs''
'-ip''
'-addresses)."###'' '{%'' 'data'' 'variables.product.prodname_github_apps'' '%}'' 'and'' '{%'' 'data'' 'variables.product.prodname_oauth_apps'' '%}'' ''' ''' '6'' ''' '
...for''
'-iam/configuring''
'-scim''
'-provisioning''
'-for''
'-enterprise''
'-managed''
'-users''
'-with''
'-okta.md
'@'@'' '''
'-25,7'' '+25,7'' ''@'@'' 'You'' 'can'' 'use'' '{%'' 'data'' 'variables.product.prodname_emus'' '%}'' 'with'' 'Okta'' 'as'' 'your'' 'identitBefore'' 'you'' 'can'' 'configure'' 'provisioning'' 'with'' 'Okta,'' 'you'' 'must'' 'configure'' 'SAML'' 'single''
'-sign'' 'on.'' 'For'' 'more'' 'information,'' 'see'' '"[Configuring'' 'SAML'' 'single'' 'sign''
'-on'' 'for'' 'Enterprise'' 'Managed'' 'Users](/admin/identity''
'-and''
'-access''
'-management/managing''
'-iam''
'-with''
'-enterprise''
'-managed''
'-users/configuring''
'-saml''
'-single''
'-sign''
'-on''
'-for''
'-enterprise''
'-managed''
'-users)."To'' 'configure'' 'provisioning'' 'with'' 'Okta,'' 'you'' 'must'' 'set'' 'your'' 'enterprise's'' 'name'' 'in'' 'the'' '{%'' 'data'' 'variables.product.prodname_emu_idp_application'' '%}'' 'application'' 'and'' 'enter'' 'your'' 'setup'' 'user's'' 'personal'' 'access'' 'token.'' 'You'' 'can'' 'then'' 'start'' 'provisioning'' 'users'' 'in'' 'Okta.
To'' 'configure'' 'provisioning'' 'with'' 'Okta,'' 'you'' 'must'' 'set'' 'your'' 'enterprise's'' 'name'' 'in'' 'the'' '{%'' 'data'' 'variables.product.prodname_emu_idp_application'' '%}'' 'application'' 'and'' 'enter'' 'your'' 'setup'' 'user's'' '{%'' 'data'' 'variables.product.pat_generic'' '%}.'' 'You'' 'can'' 'then'' 'start'' 'provisioning'' 'users'' 'in'' 'Okta.##'' 'Supported'' 'features'@'@'' '''
'-60,14'' '+60,14'' ''@'@'' 'After'' 'your'' '{%'' 'data'' 'variables.enterprise.prodname_emu_enterprise'' '%}'' 'has'' 'been'' 'creaAfter'' 'setting'' 'your'' 'enterprise'' 'name,'' 'you'' 'can'' 'proceed'' 'to'' 'configure'' 'provisioning'' 'settings.To'' 'configure'' 'provisioning,'' 'the'' 'setup'' 'user'' 'with'' 'the'' '**'@<em>SHORT''
'-CODE</em>_admin**'' 'username'' 'will'' 'need'' 'to'' 'provide'' 'a'' 'personal'' 'access'' 'token'' 'with'' 'the'' '**admin:enterprise**'' 'scope.'' 'For'' 'more'' 'information'' 'on'' 'creating'' 'a'' 'new'' 'token,'' 'see'' '"[Creating'' 'a'' 'personal'' 'access'' 'token](/github/setting''
'-up''
'-and''
'-managing''
'-your''
'-enterprise/managing''
'-your''
'-enterprise''
'-users''
'-with''
'-your''
'-identity''
'-provider/configuring''
'-scim''
'-provisioning''
'-for''
'-enterprise''
'-managed''
'-users#creating''
'-a''
'-personal''
'-access''
'-token)."
To'' 'configure'' 'provisioning,'' 'the'' 'setup'' 'user'' 'with'' 'the'' '**'@<em>SHORT''
'-CODE</em>_admin**'' 'username'' 'will'' 'need'' 'to'' 'provide'' 'a'' '{%'' 'data'' 'variables.product.pat_v1'' '%}'' 'with'' 'the'' '**admin:enterprise**'' 'scope.'' 'For'' 'more'' 'information'' 'on'' 'creating'' 'a'' 'new'' 'token,'' 'see'' '"[Creating'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}](/github/setting''
'-up''
'-and''
'-managing''
'-your''
'-enterprise/managing''
'-your''
'-enterprise''
'-users''
'-with''
'-your''
'-identity''
'-provider/configuring''
'-scim''
'-provisioning''
'-for''
'-enterprise''
'-managed''
'-users#creating''
'-a''
'-personal''
'-access''
'-token)."1.'' 'Navigate'' 'to'' 'your'' '{%'' 'data'' 'variables.product.prodname_emu_idp_application'' '%}'' 'application'' 'on'' 'Okta.
1.'' 'Click'' 'the'' '**Provisioning**'' 'tab.
1.'' 'In'' 'the'' 'settings'' 'menu,'' 'click'' '**Integration**.
1.'' 'To'' 'make'' 'changes,'' 'click'' '**Edit**.
1.'' 'Select'' '**Enable'' 'API'' 'integration**.
1.'' 'In'' 'the'' '"API'' 'Token"'' 'field,'' 'enter'' 'the'' 'personal'' 'access'' 'token'' 'with'' 'the'' '**admin:enterprise**'' 'scope'' 'belonging'' 'to'' 'the'' 'setup'' 'user.
1.'' 'In'' 'the'' '"API'' 'Token"'' 'field,'' 'enter'' 'the'' '{%'' 'data'' 'variables.product.pat_v1'' '%}'' 'with'' 'the'' '**admin:enterprise**'' 'scope'' 'belonging'' 'to'' 'the'' 'setup'' 'user.
![Screenshot'' 'showing'' 'the'' 'API'' 'Token'' 'field'' 'on'' 'Okta](/assets/images/help/enterprises/okta''
'-emu''
'-token.png)
1.'' 'Click'' '**Test'' 'API'' 'Credentials**.'' 'If'' 'the'' 'test'' 'is'' 'successful,'' 'a'' 'verification'' 'message'' 'will'' 'appear'' 'at'' 'the'' 'top'' 'of'' 'the'' 'screen.
1.'' 'To'' 'save'' 'the'' 'token,'' 'click'' '**Save**.
'' ''' '6'' ''' '
...ged''
'-users''
'-for''
'-iam/configuring''
'-scim''
'-provisioning''
'-for''
'-enterprise''
'-managed''
'-users.md
'@'@'' '''
'-30,9'' '+30,9'' ''@'@'' 'Before'' 'you'' 'can'' 'configure'' 'provisioning'' 'for'' '{%'' 'data'' 'variables.product.prodname_emu
'' 'For'' 'more'' 'information'' 'on'' 'configuring'' 'OIDC,'' 'see'' '"[Configuring'' 'OIDC'' 'for'' 'Enterprise'' 'Managed'' 'Users](/admin/identity''
'-and''
'-access''
'-management/using''
'-enterprise''
'-managed''
'-users''
'-for''
'-iam/configuring''
'-oidc''
'-for''
'-enterprise''
'-managed''
'-users)"
'' '{%'' 'endif'' '%}For'' 'information'' 'on'' 'configuring'' 'SAML,'' 'see'' '"[Configuring'' 'SAML'' 'single'' 'sign''
'-on'' 'for'' 'Enterprise'' 'Managed'' 'Users](/admin/identity''
'-and''
'-access''
'-management/managing''
'-iam''
'-with''
'-enterprise''
'-managed''
'-users/configuring''
'-saml''
'-single''
'-sign''
'-on''
'-for''
'-enterprise''
'-managed''
'-users)."##'' 'Creating'' 'a'' 'personal'' 'access'' 'token
##'' 'Creating'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}To'' 'configure'' 'provisioning'' 'for'' 'your'' '{%'' 'data'' 'variables.enterprise.prodname_emu_enterprise'' '%},'' 'you'' 'need'' 'a'' 'personal'' 'access'' 'token'' 'with'' 'the'' '**admin:enterprise**'' 'scope'' 'that'' 'belongs'' 'to'' 'the'' 'setup'' 'user.
To'' 'configure'' 'provisioning'' 'for'' 'your'' '{%'' 'data'' 'variables.enterprise.prodname_emu_enterprise'' '%},'' 'you'' 'need'' 'a'' '{%'' 'data'' 'variables.product.pat_v1'' '%}'' 'with'' 'the'' '**admin:enterprise**'' 'scope'' 'that'' 'belongs'' 'to'' 'the'' 'setup'' 'user.{%'' 'warning'' '%}'@'@'' '''
'-59,7'' '+59,7'' ''@'@'' 'To'' 'configure'' 'provisioning'' 'for'' 'your'' '{%'' 'data'' 'variables.enterprise.prodname_emu_ent##'' 'Configuring'' 'provisioning'' 'for'' '{%'' 'data'' 'variables.product.prodname_emus'' '%}After'' 'creating'' 'your'' 'personal'' 'access'' 'token'' 'and'' 'storing'' 'it'' 'securely,'' 'you'' 'can'' 'configure'' 'provisioning'' 'on'' 'your'' 'identity'' 'provider.'' '
After'' 'creating'' 'your'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'and'' 'storing'' 'it'' 'securely,'' 'you'' 'can'' 'configure'' 'provisioning'' 'on'' 'your'' 'identity'' 'provider.'' '{%'' 'data'' 'reusables.scim.emu''
'-scim''
'-rate''
'-limit'' '%}'' ''' '4'' ''' '
...anagement/using''
'-enterprise''
'-managed''
'-users''
'-for''
'-iam/migrating''
'-from''
'-saml''
'-to''
'-oidc.md
'@'@'' '''
'-47,11'' '+47,11'' ''@'@'' 'If'' 'you're'' 'new'' 'to'' '{%'' 'data'' 'variables.product.prodname_emus'' '%}'' 'and'' 'haven't'' 'yet'' 'conf
'' ''' ''' '![Screenshot'' 'showing'' 'the'' '"Configure'' 'with'' 'Azure"'' 'button](/assets/images/help/enterprises/saml''
'-to''
'-oidc''
'-button.png)
1.'' 'Read'' 'both'' 'warnings'' 'and'' 'click'' 'to'' 'continue.
{%'' 'data'' 'reusables.enterprise''
'-accounts.emu''
'-azure''
'-admin''
'-consent'' '%}
1.'' 'In'' 'a'' 'new'' 'tab'' 'or'' 'window,'' 'while'' 'signed'' 'in'' 'as'' 'the'' 'setup'' 'user'' 'on'' '{%'' 'data'' 'variables.product.prodname_dotcom_the_website'' '%},'' 'create'' 'a'' 'personal'' 'access'' 'token'' 'with'' 'the'' '**admin:enterprise**'' 'scope'' 'and'' '**no'' 'expiration**'' 'and'' 'copy'' 'it'' 'to'' 'your'' 'clipboard.'' 'For'' 'more'' 'information'' 'about'' 'creating'' 'a'' 'new'' 'token,'' 'see'' '"[Creating'' 'a'' 'personal'' 'access'' 'token](/github/setting''
'-up''
'-and''
'-managing''
'-your''
'-enterprise/managing''
'-your''
'-enterprise''
'-users''
'-with''
'-your''
'-identity''
'-provider/configuring''
'-scim''
'-provisioning''
'-for''
'-enterprise''
'-managed''
'-users#creating''
'-a''
'-personal''
'-access''
'-token)."
1.'' 'In'' 'a'' 'new'' 'tab'' 'or'' 'window,'' 'while'' 'signed'' 'in'' 'as'' 'the'' 'setup'' 'user'' 'on'' '{%'' 'data'' 'variables.product.prodname_dotcom_the_website'' '%},'' 'create'' 'a'' '{%'' 'data'' 'variables.product.pat_v1'' '%}'' 'with'' 'the'' '**admin:enterprise**'' 'scope'' 'and'' '**no'' 'expiration**'' 'and'' 'copy'' 'it'' 'to'' 'your'' 'clipboard.'' 'For'' 'more'' 'information'' 'about'' 'creating'' 'a'' 'new'' 'token,'' 'see'' '"[Creating'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}](/github/setting''
'-up''
'-and''
'-managing''
'-your''
'-enterprise/managing''
'-your''
'-enterprise''
'-users''
'-with''
'-your''
'-identity''
'-provider/configuring''
'-scim''
'-provisioning''
'-for''
'-enterprise''
'-managed''
'-users#creating''
'-a''
'-personal''
'-access''
'-token)."
1.'' 'In'' 'the'' 'settings'' 'for'' 'the'' '{%'' 'data'' 'variables.product.prodname_emu_idp_oidc_application'' '%}'' 'application'' 'in'' 'Azure'' 'Portal,'' 'under'' '"Tenant'' 'URL",'' 'type'' '`https://api.github.com/scim/v2/enterprises/YOUR_ENTERPRISE`,'' 'replacing'' 'YOUR_ENTERPRISE'' 'with'' 'the'' 'name'' 'of'' 'your'' 'enterprise'' 'account.'' ''' ''' ''' ''' 'For'' 'example,'' 'if'' 'your'' 'enterprise'' 'account's'' 'URL'' 'is'' '`https://github.com/enterprises/octo''
'-corp`,'' 'the'' 'name'' 'of'' 'the'' 'enterprise'' 'account'' 'is'' '`octo''
'-corp`.
1.'' 'Under'' '"Secret'' 'token",'' 'paste'' 'the'' 'personal'' 'access'' 'token'' 'with'' 'the'' '**admin:enterprise**'' 'scope'' 'that'' 'you'' 'created'' 'earlier.
1.'' 'Under'' '"Secret'' 'token",'' 'paste'' 'the'' '{%'' 'data'' 'variables.product.pat_v1'' '%}'' 'with'' 'the'' '**admin:enterprise**'' 'scope'' 'that'' 'you'' 'created'' 'earlier.
1.'' 'To'' 'test'' 'the'' 'configuration,'' 'click'' '**Test'' 'Connection**.
1.'' 'To'' 'save'' 'your'' 'changes,'' 'at'' 'the'' 'top'' 'of'' 'the'' 'form,'' 'click'' '**Save**.
1.'' 'In'' 'Azure'' 'Portal,'' 'copy'' 'the'' 'users'' 'and'' 'groups'' 'from'' 'the'' 'old'' '{%'' 'data'' 'variables.product.prodname_emu_idp_application'' '%}'' 'application'' 'to'' 'the'' 'new'' '{%'' 'data'' 'variables.product.prodname_emu_idp_oidc_application'' '%}'' 'application.
'' ''' '4'' ''' '
...dmin/identity''
'-and''
'-access''
'-management/using''
'-ldap''
'-for''
'-enterprise''
'-iam/using''
'-ldap.md
'@'@'' '''
'-89,11'' '+89,11'' ''@'@'' 'Use'' 'these'' 'attributes'' 'to'' 'finish'' 'configuring'' 'LDAP'' 'for'' '{%'' 'data'' 'variables.location.p###'' 'Disabling'' 'password'' 'authentication'' 'for'' 'Git'' 'operationsSelect'' '**Disable'' 'username'' 'and'' 'password'' 'authentication'' 'for'' 'Git'' 'operations**'' 'in'' 'your'' 'LDAP'' 'settings'' 'to'' 'enforce'' 'use'' 'of'' 'personal'' 'access'' 'tokens'' 'or'' 'SSH'' 'keys'' 'for'' 'Git'' 'access,'' 'which'' 'can'' 'help'' 'prevent'' 'your'' 'server'' 'from'' 'being'' 'overloaded'' 'by'' 'LDAP'' 'authentication'' 'requests.'' 'We'' 'recommend'' 'this'' 'setting'' 'because'' 'a'' 'slow''
'-responding'' 'LDAP'' 'server,'' 'especially'' 'combined'' 'with'' 'a'' 'large'' 'number'' 'of'' 'requests'' 'due'' 'to'' 'polling,'' 'is'' 'a'' 'frequent'' 'source'' 'of'' 'performance'' 'issues'' 'and'' 'outages.
Select'' '**Disable'' 'username'' 'and'' 'password'' 'authentication'' 'for'' 'Git'' 'operations**'' 'in'' 'your'' 'LDAP'' 'settings'' 'to'' 'enforce'' 'use'' 'of'' '{%'' 'data'' 'variables.product.pat_generic'' '%}s'' 'or'' 'SSH'' 'keys'' 'for'' 'Git'' 'access,'' 'which'' 'can'' 'help'' 'prevent'' 'your'' 'server'' 'from'' 'being'' 'overloaded'' 'by'' 'LDAP'' 'authentication'' 'requests.'' 'We'' 'recommend'' 'this'' 'setting'' 'because'' 'a'' 'slow''
'-responding'' 'LDAP'' 'server,'' 'especially'' 'combined'' 'with'' 'a'' 'large'' 'number'' 'of'' 'requests'' 'due'' 'to'' 'polling,'' 'is'' 'a'' 'frequent'' 'source'' 'of'' 'performance'' 'issues'' 'and'' 'outages.![Disable'' 'LDAP'' 'password'' 'auth'' 'for'' 'Git'' 'check'' 'box](/assets/images/enterprise/management''
'-console/ldap''
'-disable''
'-password''
'-auth''
'-for''
'-git.png)When'' 'this'' 'option'' 'is'' 'selected,'' 'if'' 'a'' 'user'' 'tries'' 'to'' 'use'' 'a'' 'password'' 'for'' 'Git'' 'operations'' 'via'' 'the'' 'command'' 'line,'' 'they'' 'will'' 'receive'' 'an'' 'error'' 'message'' 'that'' 'says,'' '`Password'' 'authentication'' 'is'' 'not'' 'allowed'' 'for'' 'Git'' 'operations.'' 'You'' 'must'' 'use'' 'a'' 'personal'' 'access'' 'token.`
When'' 'this'' 'option'' 'is'' 'selected,'' 'if'' 'a'' 'user'' 'tries'' 'to'' 'use'' 'a'' 'password'' 'for'' 'Git'' 'operations'' 'via'' 'the'' 'command'' 'line,'' 'they'' 'will'' 'receive'' 'an'' 'error'' 'message'' 'that'' 'says,'' '`Password'' 'authentication'' 'is'' 'not'' 'allowed'' 'for'' 'Git'' 'operations.'' 'You'' 'must'' 'use'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}.`###'' 'Enabling'' 'LDAP'' 'certificate'' 'verification'' ''' '6'' ''' '
...m/configuring''
'-authentication''
'-and''
'-provisioning''
'-for''
'-your''
'-enterprise''
'-using''
'-okta.md
'@'@'' '''
'-81,9'' '+81,9'' ''@'@'' 'To'' 'enable'' 'single'' 'sign''
'-on'' '(SSO)'' 'for'' '{%'' 'data'' 'variables.product.prodname_ghe_manage##'' 'Enabling'' 'API'' 'integrationThe'' '"GitHub'' 'AE"'' 'app'' 'in'' 'Okta'' 'uses'' 'the'' '{%'' 'data'' 'variables.product.product_name'' '%}'' 'API'' 'to'' 'interact'' 'with'' 'your'' 'enterprise'' 'for'' 'SCIM'' 'and'' 'SSO.'' 'This'' 'procedure'' 'explains'' 'how'' 'to'' 'enable'' 'and'' 'test'' 'access'' 'to'' 'the'' 'API'' 'by'' 'configuring'' 'Okta'' 'with'' 'a'' 'personal'' 'access'' 'token'' 'for'' '{%'' 'data'' 'variables.product.prodname_ghe_managed'' '%}.
The'' '"GitHub'' 'AE"'' 'app'' 'in'' 'Okta'' 'uses'' 'the'' '{%'' 'data'' 'variables.product.product_name'' '%}'' 'API'' 'to'' 'interact'' 'with'' 'your'' 'enterprise'' 'for'' 'SCIM'' 'and'' 'SSO.'' 'This'' 'procedure'' 'explains'' 'how'' 'to'' 'enable'' 'and'' 'test'' 'access'' 'to'' 'the'' 'API'' 'by'' 'configuring'' 'Okta'' 'with'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'for'' '{%'' 'data'' 'variables.product.prodname_ghe_managed'' '%}.1.'' 'In'' '{%'' 'data'' 'variables.product.prodname_ghe_managed'' '%},'' 'generate'' 'a'' 'personal'' 'access'' 'token'' 'with'' 'the'' '`admin:enterprise`'' 'scope.'' 'For'' 'more'' 'information,'' 'see'' '"[Creating'' 'a'' 'personal'' 'access'' 'token](/github/authenticating''
'-to''
'-github/keeping''
'-your''
'-account''
'-and''
'-data''
'-secure/creating''
'-a''
'-personal''
'-access''
'-token)".
1.'' 'In'' '{%'' 'data'' 'variables.product.prodname_ghe_managed'' '%},'' 'generate'' 'a'' '{%'' 'data'' 'variables.product.pat_v1'' '%}'' 'with'' 'the'' '`admin:enterprise`'' 'scope.'' 'For'' 'more'' 'information,'' 'see'' '"[Creating'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}](/github/authenticating''
'-to''
'-github/keeping''
'-your''
'-account''
'-and''
'-data''
'-secure/creating''
'-a''
'-personal''
'-access''
'-token)".
{%'' 'data'' 'reusables.saml.okta''
'-ae''
'-applications''
'-menu'' '%}
{%'' 'data'' 'reusables.saml.okta''
'-ae''
'-configure''
'-app'' '%}
{%'' 'data'' 'reusables.saml.okta''
'-ae''
'-provisioning''
'-tab'' '%}
'@'@'' '''
'-93,7'' '+93,7'' ''@'@'' 'The'' '"GitHub'' 'AE"'' 'app'' 'in'' 'Okta'' 'uses'' 'the'' '{%'' 'data'' 'variables.product.product_name'' '%}'' 'A'' ''' '![Enable'' 'API'' 'integration](/assets/images/help/saml/okta''
'-ae''
'-enable''
'-api''
'-integration.png)1.'' 'For'' '"API'' 'Token",'' 'type'' 'the'' '{%'' 'data'' 'variables.product.prodname_ghe_managed'' '%}'' 'personal'' 'access'' 'token'' 'you'' 'generated'' 'previously.
1.'' 'For'' '"API'' 'Token",'' 'type'' 'the'' '{%'' 'data'' 'variables.product.prodname_ghe_managed'' '%}'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'you'' 'generated'' 'previously.1.'' 'Click'' '**Test'' 'API'' 'Credentials**.'' ''' ''' '10'' ''' '
...ng''
'-saml''
'-for''
'-enterprise''
'-iam/configuring''
'-user''
'-provisioning''
'-for''
'-your''
'-enterprise.md
'@'@'' '''
'-48,17'' '+48,17'' ''@'@'' 'You'' 'must'' 'have'' 'administrative'' 'access'' 'on'' 'your'' 'IdP'' 'to'' 'configure'' 'the'' 'application'' 'for##'' 'Enabling'' 'user'' 'provisioning'' 'for'' 'your'' 'enterprise1.'' 'While'' 'signed'' 'into'' '{%'' 'data'' 'variables.location.product_location'' '%}'' 'as'' 'an'' 'enterprise'' 'owner,'' 'create'' 'a'' 'personal'' 'access'' 'token'' 'with'' '**admin:enterprise**'' 'scope.'' 'For'' 'more'' 'information,'' 'see'' '"[Creating'' 'a'' 'personal'' 'access'' 'token](/github/authenticating''
'-to''
'-github/creating''
'-a''
'-personal''
'-access''
'-token)."
1.'' 'While'' 'signed'' 'into'' '{%'' 'data'' 'variables.location.product_location'' '%}'' 'as'' 'an'' 'enterprise'' 'owner,'' 'create'' 'a'' '{%'' 'data'' 'variables.product.pat_v1'' '%}'' 'with'' '**admin:enterprise**'' 'scope.'' 'For'' 'more'' 'information,'' 'see'' '"[Creating'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}](/github/authenticating''
'-to''
'-github/creating''
'-a''
'-personal''
'-access''
'-token)."
'' ''' '{%'' 'note'' '%}'' ''' '**Notes**:
'' ''' ''' ''' ''' 'To'' 'create'' 'the'' 'personal'' 'access'' 'token,'' 'we'' 'recommend'' 'using'' 'the'' 'account'' 'for'' 'the'' 'first'' 'enterprise'' 'owner'' 'that'' 'you'' 'created'' 'during'' 'initialization.'' 'For'' 'more'' 'information,'' 'see'' '"[Initializing'' '{%'' 'data'' 'variables.product.prodname_ghe_managed'' '%}](/admin/configuration/initializing''
'-github''
'-ae)."
'' ''' ''' ''' ''' 'You'll'' 'need'' 'this'' 'personal'' 'access'' 'token'' 'to'' 'configure'' 'the'' 'application'' 'for'' 'SCIM'' 'on'' 'your'' 'IdP.'' 'Store'' 'the'' 'token'' 'securely'' 'in'' 'a'' 'password'' 'manager'' 'until'' 'you'' 'need'' 'the'' 'token'' 'again'' 'later'' 'in'' 'these'' 'instructions.
'' ''' ''' ''' ''' 'To'' 'create'' 'the'' '{%'' 'data'' 'variables.product.pat_generic'' '%},'' 'we'' 'recommend'' 'using'' 'the'' 'account'' 'for'' 'the'' 'first'' 'enterprise'' 'owner'' 'that'' 'you'' 'created'' 'during'' 'initialization.'' 'For'' 'more'' 'information,'' 'see'' '"[Initializing'' '{%'' 'data'' 'variables.product.prodname_ghe_managed'' '%}](/admin/configuration/initializing''
'-github''
'-ae)."
'' ''' ''' ''' ''' 'You'll'' 'need'' 'this'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'to'' 'configure'' 'the'' 'application'' 'for'' 'SCIM'' 'on'' 'your'' 'IdP.'' 'Store'' 'the'' 'token'' 'securely'' 'in'' 'a'' 'password'' 'manager'' 'until'' 'you'' 'need'' 'the'' 'token'' 'again'' 'later'' 'in'' 'these'' 'instructions.'' ''' '{%'' 'endnote'' '%}
'' ''' '{%'' 'warning'' '%}'' ''' '**Warning**:'' 'If'' 'the'' 'user'' 'account'' 'for'' 'the'' 'enterprise'' 'owner'' 'who'' 'creates'' 'the'' 'personal'' 'access'' 'token'' 'is'' 'deactivated'' 'or'' 'deprovisioned,'' 'your'' 'IdP'' 'will'' 'no'' 'longer'' 'provision'' 'and'' 'deprovision'' 'user'' 'accounts'' 'for'' 'your'' 'enterprise'' 'automatically.'' 'Another'' 'enterprise'' 'owner'' 'must'' 'create'' 'a'' 'new'' 'personal'' 'access'' 'token'' 'and'' 'reconfigure'' 'provisioning'' 'on'' 'the'' 'IdP.
'' ''' '**Warning**:'' 'If'' 'the'' 'user'' 'account'' 'for'' 'the'' 'enterprise'' 'owner'' 'who'' 'creates'' 'the'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'is'' 'deactivated'' 'or'' 'deprovisioned,'' 'your'' 'IdP'' 'will'' 'no'' 'longer'' 'provision'' 'and'' 'deprovision'' 'user'' 'accounts'' 'for'' 'your'' 'enterprise'' 'automatically.'' 'Another'' 'enterprise'' 'owner'' 'must'' 'create'' 'a'' 'new'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'and'' 'reconfigure'' 'provisioning'' 'on'' 'the'' 'IdP.'' ''' '{%'' 'endwarning'' '%}
{%'' 'data'' 'reusables.enterprise''
'-accounts.access''
'-enterprise'' '%}
'@'@'' '''
'-82,4'' '+82,4'' ''@'@'' 'You'' 'must'' 'have'' 'administrative'' 'access'' 'on'' 'your'' 'IdP'' 'to'' 'configure'' 'the'' 'application'' 'for
'' ''' '|'' 'Value'' '|'' 'Other'' 'names'' '|'' 'Description'' '|'' 'Example'' '|
'' ''' '|'' ':'' '|'' ':'' '|'' ':'' '|'' ':'' '|
'' ''' '|'' 'URL'' '|'' 'Tenant'' 'URL'' '|'' 'URL'' 'to'' 'the'' 'SCIM'' 'provisioning'' 'API'' 'for'' 'your'' 'enterprise'' 'on'' '{%'' 'data'' 'variables.product.prodname_ghe_managed'' '%}'' '|'' '<nobr><code>{%'' 'data'' 'variables.product.api_url_pre'' '%}/scim/v2</nobr></code>'' '|
'' ''' '|'' 'Shared'' 'secret'' '|'' 'Personal'' 'access'' 'token,'' 'secret'' 'token'' '|'' 'Token'' 'for'' 'application'' 'on'' 'your'' 'IdP'' 'to'' 'perform'' 'provisioning'' 'tasks'' 'on'' 'behalf'' 'of'' 'an'' 'enterprise'' 'owner'' '|'' 'Personal'' 'access'' 'token'' 'you'' 'created'' 'in'' 'step'' '1'' '|
'' ''' '|'' 'Shared'' 'secret'' '|'' '{%'' 'data'' 'variables.product.pat_generic_caps'' '%},'' 'secret'' 'token'' '|'' 'Token'' 'for'' 'application'' 'on'' 'your'' 'IdP'' 'to'' 'perform'' 'provisioning'' 'tasks'' 'on'' 'behalf'' 'of'' 'an'' 'enterprise'' 'owner'' '|'' '{%'' 'data'' 'variables.product.pat_generic_caps'' '%}'' 'you'' 'created'' 'in'' 'step'' '1'' '|
'' ''' '4'' ''' '
...tching''
'-your''
'-saml''
'-configuration''
'-from''
'-an''
'-organization''
'-to''
'-an''
'-enterprise''
'-account.md
'@'@'' '''
'-28,7'' '+28,7'' ''@'@'' 'After'' 'you'' 'configure'' 'SAML'' 'SSO'' 'for'' 'your'' 'enterprise'' 'account,'' 'the'' 'new'' 'configurationEnterprise'' 'members'' 'will'' 'not'' 'be'' 'notified'' 'when'' 'an'' 'enterprise'' 'owner'' 'enables'' 'SAML'' 'for'' 'the'' 'enterprise'' 'account.'' 'If'' 'SAML'' 'SSO'' 'was'' 'previously'' 'enforced'' 'at'' 'the'' 'organization'' 'level,'' 'members'' 'should'' 'not'' 'see'' 'a'' 'major'' 'difference'' 'when'' 'navigating'' 'directly'' 'to'' 'organization'' 'resources.'' 'The'' 'members'' 'will'' 'continue'' 'to'' 'be'' 'prompted'' 'to'' 'authenticate'' 'via'' 'SAML.'' 'If'' 'members'' 'navigate'' 'to'' 'organization'' 'resources'' 'via'' 'their'' 'IdP'' 'dashboard,'' 'they'' 'will'' 'need'' 'to'' 'click'' 'the'' 'new'' 'tile'' 'for'' 'the'' 'enterprise''
'-level'' 'app,'' 'instead'' 'of'' 'the'' 'old'' 'tile'' 'for'' 'the'' 'organization''
'-level'' 'app.'' 'The'' 'members'' 'will'' 'then'' 'be'' 'able'' 'to'' 'choose'' 'the'' 'organization'' 'to'' 'navigate'' 'to.'' 'Any'' 'personal'' 'access'' 'tokens'' '(PATs),'' 'SSH'' 'keys,'' '{%'' 'data'' 'variables.product.prodname_oauth_apps'' '%},'' 'and'' '{%'' 'data'' 'variables.product.prodname_github_apps'' '%}'' 'that'' 'were'' 'previously'' 'authorized'' 'for'' 'the'' 'organization'' 'will'' 'continue'' 'to'' 'be'' 'authorized'' 'for'' 'the'' 'organization.'' 'However,'' 'members'' 'will'' 'need'' 'to'' 'authorize'' 'any'' 'PATs,'' 'SSH'' 'keys,'' '{%'' 'data'' 'variables.product.prodname_oauth_apps'' '%},'' 'and'' '{%'' 'data'' 'variables.product.prodname_github_apps'' '%}'' 'that'' 'were'' 'never'' 'authorized'' 'for'' 'use'' 'with'' 'SAML'' 'SSO'' 'for'' 'the'' 'organization.
Any'' '{%'' 'data'' 'variables.product.pat_generic'' '%}s,'' 'SSH'' 'keys,'' '{%'' 'data'' 'variables.product.prodname_oauth_apps'' '%},'' 'and'' '{%'' 'data'' 'variables.product.prodname_github_apps'' '%}'' 'that'' 'were'' 'previously'' 'authorized'' 'for'' 'the'' 'organization'' 'will'' 'continue'' 'to'' 'be'' 'authorized'' 'for'' 'the'' 'organization.'' 'However,'' 'members'' 'will'' 'need'' 'to'' 'authorize'' 'any'' 'PATs,'' 'SSH'' 'keys,'' '{%'' 'data'' 'variables.product.prodname_oauth_apps'' '%},'' 'and'' '{%'' 'data'' 'variables.product.prodname_github_apps'' '%}'' 'that'' 'were'' 'never'' 'authorized'' 'for'' 'use'' 'with'' 'SAML'' 'SSO'' 'for'' 'the'' 'organization.SCIM'' 'provisioning'' 'is'' 'not'' 'currently'' 'supported'' 'when'' 'SAML'' 'SSO'' 'is'' 'configured'' 'for'' 'an'' 'enterprise'' 'account.'' 'If'' 'you'' 'are'' 'currently'' 'using'' 'SCIM'' 'for'' 'an'' 'organization'' 'owned'' 'by'' 'your'' 'enterprise'' 'account,'' 'you'' 'will'' 'lose'' 'this'' 'functionality'' 'when'' 'switching'' 'to'' 'an'' 'enterprise''
'-level'' 'configuration.'@'@'' '''
'-41,5'' '+41,5'' ''@'@'' 'You'' 'are'' 'not'' 'required'' 'to'' 'remove'' 'any'' 'organization''
'-level'' 'SAML'' 'configurations'' 'before
1.'' 'If'' 'you'' 'kept'' 'any'' 'organization''
'-level'' 'SAML'' 'configurations'' 'in'' 'place,'' 'to'' 'prevent'' 'confusion,'' 'consider'' 'hiding'' 'the'' 'tile'' 'for'' 'the'' 'organization''
'-level'' 'apps'' 'in'' 'your'' 'IdP.
1.'' 'Advise'' 'your'' 'enterprise'' 'members'' 'about'' 'the'' 'change.
'' ''' ''' ''' ''' 'Members'' 'will'' 'no'' 'longer'' 'be'' 'able'' 'to'' 'access'' 'their'' 'organizations'' 'by'' 'clicking'' 'the'' 'SAML'' 'app'' 'for'' 'the'' 'organization'' 'in'' 'the'' 'IdP'' 'dashboard.'' 'They'' 'will'' 'need'' 'to'' 'use'' 'the'' 'new'' 'app'' 'configured'' 'for'' 'the'' 'enterprise'' 'account.
'' ''' ''' ''' 'Members'' 'will'' 'need'' 'to'' 'authorize'' 'any'' 'PATs'' 'or'' 'SSH'' 'keys'' 'that'' 'were'' 'not'' 'previously'' 'authorized'' 'for'' 'use'' 'with'' 'SAML'' 'SSO'' 'for'' 'their'' 'organization.'' 'For'' 'more'' 'information,'' 'see'' '"[Authorizing'' 'a'' 'personal'' 'access'' 'token'' 'for'' 'use'' 'with'' 'SAML'' 'single'' 'sign''
'-on](/github/authenticating''
'-to''
'-github/authenticating''
'-with''
'-saml''
'-single''
'-sign''
'-on/authorizing''
'-a''
'-personal''
'-access''
'-token''
'-for''
'-use''
'-with''
'-saml''
'-single''
'-sign''
'-on)"'' 'and'' '"[Authorizing'' 'an'' 'SSH'' 'key'' 'for'' 'use'' 'with'' 'SAML'' 'single'' 'sign''
'-on](/github/authenticating''
'-to''
'-github/authenticating''
'-with''
'-saml''
'-single''
'-sign''
'-on/authorizing''
'-an''
'-ssh''
'-key''
'-for''
'-use''
'-with''
'-saml''
'-single''
'-sign''
'-on)."
'' ''' ''' ''' 'Members'' 'will'' 'need'' 'to'' 'authorize'' 'any'' 'PATs'' 'or'' 'SSH'' 'keys'' 'that'' 'were'' 'not'' 'previously'' 'authorized'' 'for'' 'use'' 'with'' 'SAML'' 'SSO'' 'for'' 'their'' 'organization.'' 'For'' 'more'' 'information,'' 'see'' '"[Authorizing'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'for'' 'use'' 'with'' 'SAML'' 'single'' 'sign''
'-on](/github/authenticating''
'-to''
'-github/authenticating''
'-with''
'-saml''
'-single''
'-sign''
'-on/authorizing''
'-a''
'-personal''
'-access''
'-token''
'-for''
'-use''
'-with''
'-saml''
'-single''
'-sign''
'-on)"'' 'and'' '"[Authorizing'' 'an'' 'SSH'' 'key'' 'for'' 'use'' 'with'' 'SAML'' 'single'' 'sign''
'-on](/github/authenticating''
'-to''
'-github/authenticating''
'-with''
'-saml''
'-single''
'-sign''
'-on/authorizing''
'-an''
'-ssh''
'-key''
'-for''
'-use''
'-with''
'-saml''
'-single''
'-sign''
'-on)."
'' ''' ''' ''' 'Members'' 'may'' 'need'' 'to'' 'reauthorize'' '{%'' 'data'' 'variables.product.prodname_oauth_apps'' '%}'' 'that'' 'were'' 'previously'' 'authorized'' 'for'' 'the'' 'organization.'' 'For'' 'more'' 'information,'' 'see'' '"[About'' 'authentication'' 'with'' 'SAML'' 'single'' 'sign''
'-on](/github/authenticating''
'-to''
'-github/authenticating''
'-with''
'-saml''
'-single''
'-sign''
'-on/about''
'-authentication''
'-with''
'-saml''
'-single''
'-sign''
'-on#about''
'-oauth''
'-apps''
'-github''
'-apps''
'-and''
'-saml''
'-sso)."
'' ''' '2'' ''' '
...eviewing''
'-audit''
'-logs''
'-for''
'-your''
'-enterprise/audit''
'-log''
'-events''
'-for''
'-your''
'-enterprise.md
'@'@'' '''
'-573,7'' '+573,7'' ''@'@'' 'Before'' 'you'll'' 'see'' '`git`'' 'category'' 'actions,'' 'you'' 'must'' 'enable'' 'Git'' 'events'' 'in'' 'the'' 'audi|'' 'Action'' '|'' 'Description
|''
'-|''
'-
`oauth_access.create`'' ''' ''' '|'' 'An'' '[OAuth'' 'access'' 'token][]'' 'was'' 'generated'' 'for'' 'a'' 'user'' 'account.'' 'For'' 'more'' 'information,'' 'see'' '"[Creating'' 'a'' 'personal'' 'access'' 'token](/authentication/keeping''
'-your''
'-account''
'-and''
'-data''
'-secure/creating''
'-a''
'-personal''
'-access''
'-token)."
`oauth_access.create`'' ''' ''' '|'' 'An'' '[OAuth'' 'access'' 'token][]'' 'was'' 'generated'' 'for'' 'a'' 'user'' 'account.'' 'For'' 'more'' 'information,'' 'see'' '"[Creating'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}](/authentication/keeping''
'-your''
'-account''
'-and''
'-data''
'-secure/creating''
'-a''
'-personal''
'-access''
'-token)."
`oauth_access.destroy`'' ''' '|'' 'An'' '[OAuth'' 'access'' 'token][]'' 'was'' 'deleted'' 'from'' 'a'' 'user'' 'account.'' ''' '[OAuth'' 'access'' 'token]:'' '/developers/apps/building''
'-oauth''
'-apps/authorizing''
'-oauth''
'-apps
'' ''' '2'' ''' '
content/admin/overview/system''
'-overview.md
'@'@'' '''
'-129,7'' '+129,7'' ''@'@'' 'For'' 'more'' 'information'' 'about'' '{%'' 'data'' 'variables.product.product_name'' '%}'s'' 'user'' 'perm
'' 'SSH'' 'public'' 'key'' 'authentication'' 'provides'' 'both'' 'repository'' 'access'' 'using'' 'Git'' 'and'' 'administrative'' 'shell'' 'access.'' 'For'' 'more'' 'information,'' 'see'' '"[About'' 'SSH](/authentication/connecting''
'-to''
'-github''
'-with''
'-ssh/about''
'-ssh)"'' 'and'' '"[Accessing'' 'the'' 'administrative'' 'shell'' '(SSH)](/admin/configuration/configuring''
'-your''
'-enterprise/accessing''
'-the''
'-administrative''
'-shell''
'-ssh)."
'' 'Username'' 'and'' 'password'' 'authentication'' 'with'' 'HTTP'' 'cookies'' 'provides'' 'web'' 'application'' 'access'' 'and'' 'session'' 'management,'' 'with'' 'optional'' 'two''
'-factor'' 'authentication'' '(2FA).'' 'For'' 'more'' 'information,'' 'see'' '"[Using'' 'built''
'-in'' 'authentication](/admin/identity''
'-and''
'-access''
'-management/authenticating''
'-users''
'-for''
'-your''
'-github''
'-enterprise''
'-server''
'-instance/using''
'-built''
'-in''
'-authentication)."
'' 'External'' 'LDAP,'' 'SAML,'' 'or'' 'CAS'' 'authentication'' 'using'' 'an'' 'LDAP'' 'service,'' 'SAML'' 'Identity'' 'Provider'' '(IdP),'' 'or'' 'other'' 'compatible'' 'service'' 'provides'' 'access'' 'to'' 'the'' 'web'' 'application.'' 'For'' 'more'' 'information,'' 'see'' '"[Managing'' 'IAM'' 'for'' 'your'' 'enterprise](/admin/identity''
'-and''
'-access''
'-management/managing''
'-iam''
'-for''
'-your''
'-enterprise)."
'' 'OAuth'' 'and'' 'Personal'' 'Access'' 'Tokens'' 'provide'' 'access'' 'to'' 'Git'' 'repository'' 'data'' 'and'' 'APIs'' 'for'' 'both'' 'external'' 'clients'' 'and'' 'services.'' 'For'' 'more'' 'information,'' 'see'' '"[Creating'' 'a'' 'personal'' 'access'' 'token](/github/authenticating''
'-to''
'-github/creating''
'-a''
'-personal''
'-access''
'-token)."
'' 'OAuth'' 'and'' '{%'' 'data'' 'variables.product.pat_generic'' '%}s'' 'provide'' 'access'' 'to'' 'Git'' 'repository'' 'data'' 'and'' 'APIs'' 'for'' 'both'' 'external'' 'clients'' 'and'' 'services.'' 'For'' 'more'' 'information,'' 'see'' '"[Creating'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}](/github/authenticating''
'-to''
'-github/creating''
'-a''
'-personal''
'-access''
'-token)."###'' 'Audit'' 'and'' 'access'' 'logging'' '62'' ''' '
...''
'-enterprise/enforcing''
'-policies''
'-for''
'-personal''
'-access''
'-tokens''
'-in''
'-your''
'-enterprise.md
'@'@'' '''
'-0,0'' '+1,62'' ''@'@
''
'-
title:'' 'Enforcing'' 'policies'' 'for'' 'personal'' 'access'' 'tokens'' 'in'' 'your'' 'enterprise
intro:'' 'Enterprise'' 'owners'' 'can'' 'control'' 'whether'' 'to'' 'allow'' '{%'' 'data'' 'variables.product.pat_v2'' '%}s'' 'and'' '{%'' 'data'' 'variables.product.pat_v1_plural'' '%},'' 'and'' 'can'' 'require'' 'approval'' 'for'' '{%'' 'data'' 'variables.product.pat_v2'' '%}s.
versions:
'' ''' 'feature:'' 'pat''
'-v2''
'-enterprise
shortTitle:'' '"{%'' 'data'' 'variables.product.pat_generic_caps'' '%}'' 'policies"
''
'-{%'' 'note'' '%}**Note**:'' '{%'' 'data'' 'reusables.user''
'-settings.pat''
'-v2''
'-beta'' '%}During'' 'the'' 'beta,'' 'enterprises'' 'must'' 'opt'' 'in'' 'to'' '{%'' 'data'' 'variables.product.pat_v2'' '%}s.'' 'If'' 'your'' 'enterprise'' 'has'' 'not'' 'already'' 'opted''
'-in,'' 'then'' 'you'' 'will'' 'be'' 'prompted'' 'to'' 'opt''
'-in'' 'and'' 'set'' 'policies'' 'when'' 'you'' 'follow'' 'the'' 'steps'' 'below.Even'' 'if'' 'an'' 'enterprise'' 'has'' 'not'' 'opted'' 'in'' 'to'' '{%'' 'data'' 'variables.product.pat_v2'' '%}s,'' 'organizations'' 'owned'' 'by'' 'the'' 'enterprise'' 'can'' 'still'' 'opt'' 'in.'' 'All'' 'users,'' 'including'' '{%'' 'data'' 'variables.product.prodname_emus'' '%},'' 'can'' 'create'' '{%'' 'data'' 'variables.product.pat_v2'' '%}s'' 'that'' 'can'' 'access'' 'resources'' 'owned'' 'by'' 'the'' 'user'' '(such'' 'as'' 'repositories'' 'created'' 'under'' 'their'' 'account)'' 'even'' 'if'' 'the'' 'enterprise'' 'has'' 'not'' 'opted'' 'in'' 'to'' '{%'' 'data'' 'variables.product.pat_v2'' '%}s.{%'' 'endnote'' '%}##'' 'Restricting'' 'access'' 'by'' '{%'' 'data'' 'variables.product.pat_v2'' '%}sEnterprise'' 'owners'' 'can'' 'prevent'' '{%'' 'data'' 'variables.product.pat_v2'' '%}s'' 'from'' 'accessing'' 'private'' 'and'' 'internal'' 'resources'' 'owned'' 'by'' 'the'' 'enterprise.'' '{%'' 'data'' 'variables.product.pat_v2_caps'' '%}s'' 'will'' 'still'' 'be'' 'able'' 'to'' 'access'' 'public'' 'resources'' 'within'' 'the'' 'organizations.'' 'This'' 'setting'' 'only'' 'controls'' 'access'' 'by'' '{%'' 'data'' 'variables.product.pat_v2'' '%}s,'' 'not'' '{%'' 'data'' 'variables.product.pat_v1_plural'' '%}.'' 'For'' 'more'' 'information'' 'about'' 'restricting'' 'access'' 'by'' '{%'' 'data'' 'variables.product.pat_v1_plural'' '%},'' 'see'' '"[Restricting'' 'access'' 'by'' '{%'' 'data'' 'variables.product.pat_v1_plural'' '%}](#restricting''
'-access''
'-by''
'-personal''
'-access''
'-tokens''
'-classic)"'' 'on'' 'this'' 'page.{%'' 'data'' 'reusables.enterprise''
'-accounts.access''
'-enterprise'' '%}
{%'' 'data'' 'reusables.enterprise''
'-accounts.policies''
'-tab'' '%}
1.'' 'Under'' '{%'' 'octicon'' '"law"'' 'aria''
'-label="The'' 'law'' 'icon"'' '%}'' '**Policies**,'' 'click'' '**Organizations**.
1.'' 'Under'' '**Restrict'' 'access'' 'via'' '{%'' 'data'' 'variables.product.pat_v2'' '%}s**,'' 'select'' 'the'' 'option'' 'that'' 'meets'' 'your'' 'needs:
'' ''' ''' ''' '**Allow'' 'organizations'' 'to'' 'configure'' 'access'' 'requirements**:'' 'Each'' 'organization'' 'owned'' 'by'' 'the'' 'enterprise'' 'can'' 'decide'' 'whether'' 'to'' 'restrict'' 'access'' 'by'' '{%'' 'data'' 'variables.product.pat_v2'' '%}s.
'' ''' ''' ''' '**Restrict'' 'access'' 'via'' '{%'' 'data'' 'variables.product.pat_v2'' '%}s**:'' '{%'' 'data'' 'variables.product.pat_v2_caps'' '%}s'' 'cannot'' 'access'' 'organizations'' 'owned'' 'by'' 'the'' 'enterprise.'' 'SSH'' 'keys'' 'created'' 'by'' '{%'' 'data'' 'variables.product.pat_v2'' '%}s'' 'will'' 'continue'' 'to'' 'work.'' 'Organizations'' 'cannot'' 'override'' 'this'' 'setting.
'' ''' ''' ''' '**Allow'' 'access'' 'via'' '{%'' 'data'' 'variables.product.pat_v2'' '%}s**:'' '{%'' 'data'' 'variables.product.pat_v2_caps'' '%}s'' 'can'' 'access'' 'organizations'' 'owned'' 'by'' 'the'' 'enterprise.'' 'Organizations'' 'cannot'' 'override'' 'this'' 'setting.
1.'' 'Click'' '**Save**.##'' 'Enforcing'' 'an'' 'approval'' 'policy'' 'for'' '{%'' 'data'' 'variables.product.pat_v2'' '%}sEnterprise'' 'owners'' 'can'' 'require'' 'that'' 'all'' 'organizations'' 'owned'' 'by'' 'the'' 'enterprise'' 'must'' 'approve'' 'each'' '{%'' 'data'' 'variables.product.pat_v2'' '%}'' 'that'' 'can'' 'access'' 'the'' 'organization.'' '{%'' 'data'' 'variables.product.pat_v2_caps'' '%}s'' 'will'' 'still'' 'be'' 'able'' 'to'' 'read'' 'public'' 'resources'' 'within'' 'the'' 'organization'' 'without'' 'approval.'' 'Conversely,'' 'enterprise'' 'owners'' 'can'' 'allow'' '{%'' 'data'' 'variables.product.pat_v2'' '%}s'' 'to'' 'access'' 'organizations'' 'in'' 'the'' 'enterprise'' 'without'' 'prior'' 'approval.'' 'Enterprise'' 'owners'' 'can'' 'also'' 'let'' 'each'' 'organization'' 'in'' 'the'' 'enterprise'' 'choose'' 'their'' 'own'' 'approval'' 'settings.{%'' 'note'' '%}**Note**:'' 'Only'' '{%'' 'data'' 'variables.product.pat_v2'' '%}s,'' 'not'' '{%'' 'data'' 'variables.product.pat_v1_plural'' '%},'' 'are'' 'subject'' 'to'' 'approval.'' 'Unless'' 'the'' 'organization'' 'or'' 'enterprise'' 'has'' 'restricted'' 'access'' 'by'' '{%'' 'data'' 'variables.product.pat_v1_plural'' '%},'' 'any'' '{%'' 'data'' 'variables.product.pat_v1'' '%}'' 'can'' 'access'' 'organization'' 'resources'' 'without'' 'prior'' 'approval.'' 'For'' 'more'' 'information'' 'about'' 'restricting'' '{%'' 'data'' 'variables.product.pat_v1_plural'' '%},'' 'see'' '"[Restricting'' 'access'' 'by'' '{%'' 'data'' 'variables.product.pat_v1_plural'' '%}](#restricting''
'-access''
'-by''
'-personal''
'-access''
'-tokens''
'-classic)"'' 'on'' 'this'' 'page'' 'and'' '"[Setting'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'policy'' 'for'' 'your'' 'organization](/organizations/managing''
'-programmatic''
'-access''
'-to''
'-your''
'-organization/setting''
'-a''
'-personal''
'-access''
'-token''
'-policy''
'-for''
'-your''
'-organization)."{%'' 'endnote'' '%}{%'' 'data'' 'reusables.enterprise''
'-accounts.access''
'-enterprise'' '%}
{%'' 'data'' 'reusables.enterprise''
'-accounts.policies''
'-tab'' '%}
1.'' 'Under'' '{%'' 'octicon'' '"law"'' 'aria''
'-label="The'' 'law'' 'icon"'' '%}'' '**Policies**,'' 'click'' '**Organizations**.
1.'' 'Under'' '**Require'' 'approval'' 'of'' '{%'' 'data'' 'variables.product.pat_v2'' '%}s**,'' 'select'' 'the'' 'option'' 'that'' 'meets'' 'your'' 'needs:
'' ''' ''' ''' '**Allow'' 'organizations'' 'to'' 'configure'' 'approval'' 'requirements**:'' 'Each'' 'organization'' 'owned'' 'by'' 'the'' 'enterprise'' 'can'' 'decide'' 'whether'' 'to'' 'require'' 'approval'' 'of'' '{%'' 'data'' 'variables.product.pat_v2'' '%}'' 'that'' 'can'' 'access'' 'the'' 'organization.
'' ''' ''' ''' '**Require'' 'organizations'' 'to'' 'use'' 'the'' 'approval'' 'flow**:'' 'All'' 'organizations'' 'owned'' 'by'' 'the'' 'enterprise'' 'must'' 'approve'' 'each'' '{%'' 'data'' 'variables.product.pat_v2'' '%}'' 'that'' 'can'' 'access'' 'the'' 'organization.'' '{%'' 'data'' 'variables.product.pat_v2_caps'' '%}s'' 'created'' 'by'' 'organization'' 'owners'' 'will'' 'not'' 'need'' 'approval.'' 'Organizations'' 'cannot'' 'override'' 'this'' 'setting.
'' ''' ''' ''' '**Disable'' 'the'' 'approval'' 'flow'' 'in'' 'all'' 'organizations**:'' '{%'' 'data'' 'variables.product.pat_v2_caps'' '%}s'' 'created'' 'by'' 'organization'' 'members'' 'can'' 'access'' 'organizations'' 'owned'' 'by'' 'the'' 'enterprise'' 'without'' 'prior'' 'approval.'' 'Organizations'' 'cannot'' 'override'' 'this'' 'setting.
1.'' 'Click'' '**Save**.##'' 'Restricting'' 'access'' 'by'' '{%'' 'data'' 'variables.product.pat_v1_plural'' '%}Enterprise'' 'owners'' 'can'' 'prevent'' '{%'' 'data'' 'variables.product.pat_v1_plural'' '%}'' 'from'' 'accessing'' 'the'' 'enterprise'' 'and'' 'organizations'' 'owned'' 'by'' 'the'' 'enterprise.'' '{%'' 'data'' 'variables.product.pat_v1_caps_plural'' '%}'' 'will'' 'still'' 'be'' 'able'' 'to'' 'access'' 'public'' 'resources'' 'within'' 'the'' 'organization.'' 'This'' 'setting'' 'only'' 'controls'' 'access'' 'by'' '{%'' 'data'' 'variables.product.pat_v1_plural'' '%},'' 'not'' '{%'' 'data'' 'variables.product.pat_v2'' '%}s.'' 'For'' 'more'' 'information'' 'about'' 'restricting'' 'access'' 'by'' '{%'' 'data'' 'variables.product.pat_v2'' '%}s,'' 'see'' '"[Restricting'' 'access'' 'by'' '{%'' 'data'' 'variables.product.pat_v2'' '%}s](#restricting''
'-access''
'-by''
'-fine''
'-grained''
'-personal''
'-access''
'-tokens)"'' 'on'' 'this'' 'page.{%'' 'data'' 'reusables.enterprise''
'-accounts.access''
'-enterprise'' '%}
{%'' 'data'' 'reusables.enterprise''
'-accounts.policies''
'-tab'' '%}
1.'' 'Under'' '{%'' 'octicon'' '"law"'' 'aria''
'-label="The'' 'law'' 'icon"'' '%}'' '**Policies**,'' 'click'' '**Organizations**.
1.'' 'Under'' '**Restrict'' '{%'' 'data'' 'variables.product.pat_v1_plural'' '%}'' 'from'' 'accessing'' 'your'' 'organizations**,'' 'select'' 'the'' 'option'' 'that'' 'meets'' 'your'' 'needs:
'' ''' ''' ''' '**Allow'' 'organizations'' 'to'' 'configure'' '{%'' 'data'' 'variables.product.pat_v1_plural'' '%}'' 'access'' 'requirements**:'' 'Each'' 'organization'' 'owned'' 'by'' 'the'' 'enterprise'' 'can'' 'decide'' 'whether'' 'to'' 'restrict'' 'access'' 'by'' '{%'' 'data'' 'variables.product.pat_v1_plural'' '%}.
'' ''' ''' ''' '**Restrict'' 'access'' 'via'' '{%'' 'data'' 'variables.product.pat_v1_plural'' '%}**:'' '{%'' 'data'' 'variables.product.pat_v1_caps_plural'' '%}'' 'cannot'' 'access'' 'the'' 'enterprise'' 'or'' 'organizations'' 'owned'' 'by'' 'the'' 'enterprise.'' 'SSH'' 'keys'' 'created'' 'by'' '{%'' 'data'' 'variables.product.pat_v1_plural'' '%}'' 'will'' 'continue'' 'to'' 'work.'' 'Organizations'' 'cannot'' 'override'' 'this'' 'setting.
'' ''' ''' ''' '**Allow'' 'access'' 'via'' '{%'' 'data'' 'variables.product.pat_v1_plural'' '%}**:'' '{%'' 'data'' 'variables.product.pat_v1_caps_plural'' '%}'' 'can'' 'access'' 'the'' 'enterprise'' 'and'' 'organizations'' 'owned'' 'by'' 'the'' 'enterprise.'' 'Organizations'' 'cannot'' 'override'' 'this'' 'setting.
1.'' 'Click'' '**Save**.
'' ''' '1'' ''' '
content/admin/policies/enforcing''
'-policies''
'-for''
'-your''
'-enterprise/index.md
'@'@'' '''
'-22,6'' '+22,7'' ''@'@'' 'children:
'' ''' ''' '/enforcing''
'-policies''
'-for''
'-dependency''
'-insights''
'-in''
'-your''
'-enterprise
'' ''' ''' '/enforcing''
'-policies''
'-for''
'-github''
'-actions''
'-in''
'-your''
'-enterprise
'' ''' ''' '/enforcing''
'-policies''
'-for''
'-code''
'-security''
'-and''
'-analysis''
'-for''
'-your''
'-enterprise
'' ''' ''' '/enforcing''
'-policies''
'-for''
'-personal''
'-access''
'-tokens''
'-in''
'-your''
'-enterprise
shortTitle:'' 'Enforce'' 'policies
'' ''' '2'' ''' '
...ing''
'-organizations''
'-in''
'-your''
'-enterprise/adding''
'-organizations''
'-to''
'-your''
'-enterprise.md
'@'@'' '''
'-31,7'' '+31,7'' ''@'@'' 'After'' 'you'' 'add'' 'an'' 'existing'' 'organization'' 'to'' 'your'' 'enterprise,'' 'the'' 'organization's'' 're
'' 'Enterprise'' 'owners'' 'can'' 'manage'' 'their'' 'role'' 'within'' 'the'' 'organization.'' 'For'' 'more'' 'information,'' 'see'' '"[Managing'' 'your'' 'role'' 'in'' 'an'' 'organization'' 'owned'' 'by'' 'your'' 'enterprise](/admin/user''
'-management/managing''
'-organizations''
'-in''
'-your''
'-enterprise/managing''
'-your''
'-role''
'-in''
'-an''
'-organization''
'-owned''
'-by''
'-your''
'-enterprise)."
'' 'Any'' 'policies'' 'applied'' 'to'' 'the'' 'enterprise'' 'will'' 'apply'' 'to'' 'the'' 'organization.'' 'For'' 'more'' 'information,'' 'see'' '"[About'' 'enterprise'' 'policies](/admin/policies/enforcing''
'-policies''
'-for''
'-your''
'-enterprise/about''
'-enterprise''
'-policies)."
'' 'If'' 'SAML'' 'SSO'' 'is'' 'configured'' 'for'' 'the'' 'enterprise'' 'account,'' 'the'' 'enterprise's'' 'SAML'' 'configuration'' 'will'' 'apply'' 'to'' 'the'' 'organization.'' 'If'' 'the'' 'organization'' 'used'' 'SAML'' 'SSO,'' 'the'' 'enterprise'' 'account's'' 'configuration'' 'will'' 'replace'' 'the'' 'organization's'' 'configuration.'' 'SCIM'' 'is'' 'not'' 'available'' 'for'' 'enterprise'' 'accounts,'' 'so'' 'SCIM'' 'will'' 'be'' 'disabled'' 'for'' 'the'' 'organization.'' 'For'' 'more'' 'information,'' 'see'' '"[Configuring'' 'SAML'' 'single'' 'sign''
'-on'' 'for'' 'your'' 'enterprise](/admin/identity''
'-and''
'-access''
'-management/using''
'-saml''
'-for''
'-enterprise''
'-iam/configuring''
'-saml''
'-single''
'-sign''
'-on''
'-for''
'-your''
'-enterprise)"'' 'and'' '"[Switching'' 'your'' 'SAML'' 'configuration'' 'from'' 'an'' 'organization'' 'to'' 'an'' 'enterprise'' 'account](/admin/identity''
'-and''
'-access''
'-management/using''
'-saml''
'-for''
'-enterprise''
'-iam/switching''
'-your''
'-saml''
'-configuration''
'-from''
'-an''
'-organization''
'-to''
'-an''
'-enterprise''
'-account)."
'' 'If'' 'SAML'' 'SSO'' 'was'' 'configured'' 'for'' 'the'' 'organization,'' 'members''' 'existing'' 'personal'' 'access'' 'tokens'' '(PATs)'' 'or'' 'SSH'' 'keys'' 'that'' 'were'' 'authorized'' 'to'' 'access'' 'the'' 'organization's'' 'resources'' 'will'' 'be'' 'authorized'' 'to'' 'access'' 'the'' 'same'' 'resources.'' 'To'' 'access'' 'additional'' 'organizations'' 'owned'' 'by'' 'the'' 'enterprise,'' 'members'' 'must'' 'authorize'' 'the'' 'PAT'' 'or'' 'key.'' 'For'' 'more'' 'information,'' 'see'' '"[Authorizing'' 'a'' 'personal'' 'access'' 'token'' 'for'' 'use'' 'with'' 'SAML'' 'single'' 'sign''
'-on](/authentication/authenticating''
'-with''
'-saml''
'-single''
'-sign''
'-on/authorizing''
'-a''
'-personal''
'-access''
'-token''
'-for''
'-use''
'-with''
'-saml''
'-single''
'-sign''
'-on)"'' 'and'' '"[Authorizing'' 'an'' 'SSH'' 'key'' 'for'' 'use'' 'with'' 'SAML'' 'single'' 'sign''
'-on](/authentication/authenticating''
'-with''
'-saml''
'-single''
'-sign''
'-on/authorizing''
'-an''
'-ssh''
'-key''
'-for''
'-use''
'-with''
'-saml''
'-single''
'-sign''
'-on)."
'' 'If'' 'SAML'' 'SSO'' 'was'' 'configured'' 'for'' 'the'' 'organization,'' 'members''' 'existing'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'or'' 'SSH'' 'keys'' 'that'' 'were'' 'authorized'' 'to'' 'access'' 'the'' 'organization's'' 'resources'' 'will'' 'be'' 'authorized'' 'to'' 'access'' 'the'' 'same'' 'resources.'' 'To'' 'access'' 'additional'' 'organizations'' 'owned'' 'by'' 'the'' 'enterprise,'' 'members'' 'must'' 'authorize'' 'the'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'or'' 'key.'' 'For'' 'more'' 'information,'' 'see'' '"[Authorizing'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'for'' 'use'' 'with'' 'SAML'' 'single'' 'sign''
'-on](/authentication/authenticating''
'-with''
'-saml''
'-single''
'-sign''
'-on/authorizing''
'-a''
'-personal''
'-access''
'-token''
'-for''
'-use''
'-with''
'-saml''
'-single''
'-sign''
'-on)"'' 'and'' '"[Authorizing'' 'an'' 'SSH'' 'key'' 'for'' 'use'' 'with'' 'SAML'' 'single'' 'sign''
'-on](/authentication/authenticating''
'-with''
'-saml''
'-single''
'-sign''
'-on/authorizing''
'-an''
'-ssh''
'-key''
'-for''
'-use''
'-with''
'-saml''
'-single''
'-sign''
'-on)."
'' 'If'' 'the'' 'organization'' 'was'' 'connected'' 'to'' '{%'' 'data'' 'variables.product.prodname_ghe_server'' '%}'' 'or'' '{%'' 'data'' 'variables.product.prodname_ghe_managed'' '%}'' 'using'' '{%'' 'data'' 'variables.product.prodname_github_connect'' '%},'' 'adding'' 'the'' 'organization'' 'to'' 'an'' 'enterprise'' 'will'' 'not'' 'update'' 'the'' 'connection.'' '{%'' 'data'' 'variables.product.prodname_github_connect'' '%}'' 'features'' 'will'' 'no'' 'longer'' 'function'' 'for'' 'the'' 'organization.'' 'To'' 'continue'' 'using'' '{%'' 'data'' 'variables.product.prodname_github_connect'' '%},'' 'you'' 'must'' 'disable'' 'and'' 're''
'-enable'' 'the'' 'feature.'' 'For'' 'more'' 'information,'' 'see'' 'the'' 'following'' 'articles.'' ''' ''' '"[Managing'' '{%'' 'data'' 'variables.product.prodname_github_connect'' '%}](/enterprise''
'-server'@latest/admin/configuration/configuring''
'-github''
'-connect/managing''
'-github''
'-connect)"'' 'in'' 'the'' '{%'' 'data'' 'variables.product.prodname_ghe_server'' '%}'' 'documentation
'' ''' '4'' ''' '
...ta''
'-to''
'-and''
'-from''
'-your''
'-enterprise/exporting''
'-migration''
'-data''
'-from''
'-your''
'-enterprise.md
'@'@'' '''
'-47,9'' '+47,9'' ''@'@'' 'shortTitle:'' 'Export'' 'from'' 'your'' 'enterprise
'' ''' '```shell
'' ''' 'Enter'' 'username'' 'authorized'' 'for'' 'migration:'' ''' 'admin
When'' 'prompted'' 'for'' 'a'' 'personal'' 'access'' 'token,'' 'enter'' 'the'' 'access'' 'token'' 'you'' 'created'' 'in'' '"Preparing'' 'the'' '{%'' 'data'' 'variables.product.prodname_ghe_server'' '%}'' 'source'' 'instance":
When'' 'prompted'' 'for'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%},'' 'enter'' 'the'' 'access'' 'token'' 'you'' 'created'' 'in'' '"Preparing'' 'the'' '{%'' 'data'' 'variables.product.prodname_ghe_server'' '%}'' 'source'' 'instance":
Enter'' 'personal'' 'access'' 'token:'' ''' '**************
Enter'' '{%'' 'data'' 'variables.product.pat_generic'' '%}:'' ''' '**************
When'' 'ghe''
'-migrator'' 'add'' 'has'' 'finished'' 'it'' 'will'' 'print'' 'the'' 'unique'' '"Migration'' 'GUID"'' 'that'' 'it'' 'generated'' 'to'' 'identify'' 'this'' 'export'' 'as'' 'well'' 'as'' 'a'' 'list'' 'of'' 'the'' 'resources'' 'that'' 'were'' 'added'' 'to'' 'the'' 'export.'' 'You'' 'will'' 'use'' 'the'' 'Migration'' 'GUID'' 'that'' 'it'' 'generated'' 'in'' 'subsequent'' 'ghe''
'-migrator'' 'add'' 'and'' 'ghe''
'-migrator'' 'export'' 'steps'' 'to'' 'tell'' 'ghe''
'-migrator'' 'to'' 'continue'' 'operating'' 'on'' 'the'' 'same'' 'export.
2'' ''' '
...migrating''
'-data''
'-to''
'-and''
'-from''
'-your''
'-enterprise/migrating''
'-data''
'-to''
'-your''
'-enterprise.md
'@'@'' '''
'-30,7'' '+30,7'' ''@'@'' 'After'' 'you'' 'prepare'' 'the'' 'data'' 'and'' 'resolve'' 'conflicts,'' 'you'' 'can'' 'apply'' 'the'' 'imported'' 'dat2.'' 'Using'' 'the'' '`ghe''
'-migrator'' 'import`'' 'command,'' 'start'' 'the'' 'import'' 'process.'' 'You'll'' 'need:
'' ''' '*'' 'Your'' 'Migration'' 'GUID.'' 'For'' 'more'' 'information,'' 'see'' '"[Preparing'' 'to'' 'migrate'' 'data'' 'to'' 'your'' 'enterprise](/admin/user''
'-management/preparing''
'-to''
'-migrate''
'-data''
'-to''
'-your''
'-enterprise)."
'' ''' '*'' 'Your'' 'personal'' 'access'' 'token'' 'for'' 'authentication.'' 'The'' 'personal'' 'access'' 'token'' 'that'' 'you'' 'use'' 'is'' 'only'' 'for'' 'authentication'' 'as'' 'a'' 'site'' 'administrator,'' 'and'' 'does'' 'not'' 'require'' 'any'' 'specific'' 'scope.'' 'For'' 'more'' 'information,'' 'see'' '"[Creating'' 'a'' 'personal'' 'access'' 'token](/github/authenticating''
'-to''
'-github/creating''
'-a''
'-personal''
'-access''
'-token)."
'' ''' '*'' 'Your'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'for'' 'authentication.'' 'The'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'that'' 'you'' 'use'' 'is'' 'only'' 'for'' 'authentication'' 'as'' 'a'' 'site'' 'administrator,'' 'and'' 'does'' 'not'' 'require'' 'any'' 'specific'' 'scope{%'' 'ifversion'' 'pat''
'-v2'' '%}'' 'or'' 'permissions{%'' 'endif'' '%}.'' 'For'' 'more'' 'information,'' 'see'' '"[Creating'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}](/github/authenticating''
'-to''
'-github/creating''
'-a''
'-personal''
'-access''
'-token)."'' ''' '```shell
'' ''' '$'' 'ghe''
'-migrator'' 'import'' '/home/admin/MIGRATION''
'-GUID.tar.gz'' '''
'-g'' 'MIGRATION''
'-GUID'' '''
'-u'' 'USERNAME'' '''
'-p'' 'TOKEN
8'' ''' '
...ating''
'-with''
'-saml''
'-single''
'-sign''
'-on/about''
'-authentication''
'-with''
'-saml''
'-single''
'-sign''
'-on.md
'@'@'' '''
'-46,13'' '+46,13'' ''@'@'' 'If'' 'you'' 'sign'' 'in'' 'with'' 'a'' 'SAML'' 'identity'' 'that'' 'is'' 'already'' 'linked'' 'to'' 'another'' '{%'' 'data'' 'vaIf'' 'the'' 'SAML'' 'identity'' 'you'' 'sign'' 'in'' 'with'' 'does'' 'not'' 'match'' 'the'' 'SAML'' 'identity'' 'that'' 'is'' 'currently'' 'linked'' 'to'' 'your'' '{%'' 'data'' 'variables.product.prodname_dotcom'' '%}'' 'account,'' 'you'll'' 'receive'' 'a'' 'warning'' 'that'' 'you'' 'are'' 'about'' 'to'' 'relink'' 'your'' 'account.'' 'Because'' 'your'' 'SAML'' 'identity'' 'is'' 'used'' 'to'' 'govern'' 'access'' 'and'' 'team'' 'membership,'' 'continuing'' 'with'' 'the'' 'new'' 'SAML'' 'identity'' 'can'' 'cause'' 'you'' 'to'' 'lose'' 'access'' 'to'' 'teams'' 'and'' 'organizations'' 'inside'' 'of'' '{%'' 'data'' 'variables.product.prodname_dotcom'' '%}.'' 'Only'' 'continue'' 'if'' 'you'' 'know'' 'that'' 'you're'' 'supposed'' 'to'' 'use'' 'that'' 'new'' 'SAML'' 'identity'' 'for'' 'authentication'' 'in'' 'the'' 'future.'' '##'' 'Authorizing'' 'PATs'' 'and'' 'SSH'' 'keys'' 'with'' 'SAML'' 'SSO
##'' 'Authorizing'' '{%'' 'data'' 'variables.product.pat_generic'' '%}s'' 'and'' 'SSH'' 'keys'' 'with'' 'SAML'' 'SSOTo'' 'use'' 'the'' 'API'' 'or'' 'Git'' 'on'' 'the'' 'command'' 'line'' 'to'' 'access'' 'protected'' 'content'' 'in'' 'an'' 'organization'' 'that'' 'uses'' 'SAML'' 'SSO,'' 'you'' 'will'' 'need'' 'to'' 'use'' 'an'' 'authorized'' 'personal'' 'access'' 'token'' 'over'' 'HTTPS'' 'or'' 'an'' 'authorized'' 'SSH'' 'key.
To'' 'use'' 'the'' 'API'' 'or'' 'Git'' 'on'' 'the'' 'command'' 'line'' 'to'' 'access'' 'protected'' 'content'' 'in'' 'an'' 'organization'' 'that'' 'uses'' 'SAML'' 'SSO,'' 'you'' 'will'' 'need'' 'to'' 'use'' 'an'' 'authorized'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'over'' 'HTTPS'' 'or'' 'an'' 'authorized'' 'SSH'' 'key.If'' 'you'' 'don't'' 'have'' 'a'' 'personal'' 'access'' 'token'' 'or'' 'an'' 'SSH'' 'key,'' 'you'' 'can'' 'create'' 'a'' 'personal'' 'access'' 'token'' 'for'' 'the'' 'command'' 'line'' 'or'' 'generate'' 'a'' 'new'' 'SSH'' 'key.'' 'For'' 'more'' 'information,'' 'see'' '"[Creating'' 'a'' 'personal'' 'access'' 'token](/github/authenticating''
'-to''
'-github/creating''
'-a''
'-personal''
'-access''
'-token)"'' 'or'' '"[Generating'' 'a'' 'new'' 'SSH'' 'key'' 'and'' 'adding'' 'it'' 'to'' 'the'' 'ssh''
'-agent](/articles/generating''
'-a''
'-new''
'-ssh''
'-key''
'-and''
'-adding''
'-it''
'-to''
'-the''
'-ssh''
'-agent)."
If'' 'you'' 'don't'' 'have'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'or'' 'an'' 'SSH'' 'key,'' 'you'' 'can'' 'create'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'for'' 'the'' 'command'' 'line'' 'or'' 'generate'' 'a'' 'new'' 'SSH'' 'key.'' 'For'' 'more'' 'information,'' 'see'' '"[Creating'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}](/github/authenticating''
'-to''
'-github/creating''
'-a''
'-personal''
'-access''
'-token)"'' 'or'' '"[Generating'' 'a'' 'new'' 'SSH'' 'key'' 'and'' 'adding'' 'it'' 'to'' 'the'' 'ssh''
'-agent](/articles/generating''
'-a''
'-new''
'-ssh''
'-key''
'-and''
'-adding''
'-it''
'-to''
'-the''
'-ssh''
'-agent)."To'' 'use'' 'a'' 'new'' 'or'' 'existing'' 'personal'' 'access'' 'token'' 'or'' 'SSH'' 'key'' 'with'' 'an'' 'organization'' 'that'' 'uses'' 'or'' 'enforces'' 'SAML'' 'SSO,'' 'you'' 'will'' 'need'' 'to'' 'authorize'' 'the'' 'token'' 'or'' 'authorize'' 'the'' 'SSH'' 'key'' 'for'' 'use'' 'with'' 'a'' 'SAML'' 'SSO'' 'organization.'' 'For'' 'more'' 'information,'' 'see'' '"[Authorizing'' 'a'' 'personal'' 'access'' 'token'' 'for'' 'use'' 'with'' 'SAML'' 'single'' 'sign''
'-on](/articles/authorizing''
'-a''
'-personal''
'-access''
'-token''
'-for''
'-use''
'-with''
'-saml''
'-single''
'-sign''
'-on)"'' 'or'' '"[Authorizing'' 'an'' 'SSH'' 'key'' 'for'' 'use'' 'with'' 'SAML'' 'single'' 'sign''
'-on](/articles/authorizing''
'-an''
'-ssh''
'-key''
'-for''
'-use''
'-with''
'-saml''
'-single''
'-sign''
'-on)."
To'' 'use'' 'a'' 'new'' 'or'' 'existing'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'or'' 'SSH'' 'key'' 'with'' 'an'' 'organization'' 'that'' 'uses'' 'or'' 'enforces'' 'SAML'' 'SSO,'' 'you'' 'will'' 'need'' 'to'' 'authorize'' 'the'' 'token'' 'or'' 'authorize'' 'the'' 'SSH'' 'key'' 'for'' 'use'' 'with'' 'a'' 'SAML'' 'SSO'' 'organization.'' 'For'' 'more'' 'information,'' 'see'' '"[Authorizing'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'for'' 'use'' 'with'' 'SAML'' 'single'' 'sign''
'-on](/articles/authorizing''
'-a''
'-personal''
'-access''
'-token''
'-for''
'-use''
'-with''
'-saml''
'-single''
'-sign''
'-on)"'' 'or'' '"[Authorizing'' 'an'' 'SSH'' 'key'' 'for'' 'use'' 'with'' 'SAML'' 'single'' 'sign''
'-on](/articles/authorizing''
'-an''
'-ssh''
'-key''
'-for''
'-use''
'-with''
'-saml''
'-single''
'-sign''
'-on)."##'' 'About'' '{%'' 'data'' 'variables.product.prodname_oauth_apps'' '%},'' '{%'' 'data'' 'variables.product.prodname_github_apps'' '%},'' 'and'' 'SAML'' 'SSO10'' ''' '
...sign''
'-on/authorizing''
'-a''
'-personal''
'-access''
'-token''
'-for''
'-use''
'-with''
'-saml''
'-single''
'-sign''
'-on.md
'@'@'' '''
'-1,6'' '+1,6'' ''@'@
''
'-
title:'' 'Authorizing'' 'a'' 'personal'' 'access'' 'token'' 'for'' 'use'' 'with'' 'SAML'' 'single'' 'sign''
'-on
intro:'' ''To'' 'use'' 'a'' 'personal'' 'access'' 'token'' 'with'' 'an'' 'organization'' 'that'' 'uses'' 'SAML'' 'single'' 'sign''
'-on'' '(SSO),'' 'you'' 'must'' 'first'' 'authorize'' 'the'' 'token.'
intro:'' ''To'' 'use'' 'a'' '{%'' 'data'' 'variables.product.pat_v1'' '%}'' 'with'' 'an'' 'organization'' 'that'' 'uses'' 'SAML'' 'single'' 'sign''
'-on'' '(SSO),'' 'you'' 'must'' 'first'' 'authorize'' 'the'' 'token.'
redirect_from:
'' '/articles/authorizing''
'-a''
'-personal''
'-access''
'-token''
'-for''
'-use''
'-with''
'-a''
'-saml''
'-single''
'-sign''
'-on''
'-organization
'' '/articles/authorizing''
'-a''
'-personal''
'-access''
'-token''
'-for''
'-use''
'-with''
'-saml''
'-single''
'-sign''
'-on
'@'@'' '''
'-10,9'' '+10,9'' ''@'@'' 'versions:
ghec:'' ''*'
topics:
'' 'SSO
shortTitle:'' 'PAT'' 'with'' 'SAML
shortTitle:'' ''{%'' 'data'' 'variables.product.pat_generic_caps'' '%}'' 'with'' 'SAML'
''
'-
You'' 'can'' 'authorize'' 'an'' 'existing'' 'personal'' 'access'' 'token,'' 'or'' '[create'' 'a'' 'new'' 'personal'' 'access'' 'token](/github/authenticating''
'-to''
'-github/creating''
'-a''
'-personal''
'-access''
'-token)'' 'and'' 'then'' 'authorize'' 'it.
You'' 'must'' 'authorize'' 'your'' '{%'' 'data'' 'variables.product.pat_v1'' '%}'' 'after'' 'creation'' 'before'' 'the'' 'token'' 'can'' 'access'' 'an'' 'organization'' 'that'' 'uses'' 'SAML'' 'single'' 'sign''
'-on'' '(SSO).'' 'For'' 'more'' 'information'' 'about'' 'creating'' 'a'' 'new'' '{%'' 'data'' 'variables.product.pat_v1'' '%},'' 'see'' '"[Creating'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}](/github/authenticating''
'-to''
'-github/creating''
'-a''
'-personal''
'-access''
'-token)."{%'' 'ifversion'' 'pat''
'-v2'' '%}'' '{%'' 'data'' 'variables.product.pat_v2_caps'' '%}s'' 'are'' 'authorized'' 'during'' 'token'' 'creation,'' 'before'' 'access'' 'to'' 'the'' 'organization'' 'is'' 'granted.{%'' 'endif'' '%}{%'' 'data'' 'reusables.saml.must''
'-authorize''
'-linked''
'-identity'' '%}'@'@'' '''
'-23,11'' '+23,11'' ''@'@'' 'You'' 'can'' 'authorize'' 'an'' 'existing'' 'personal'' 'access'' 'token,'' 'or'' '[create'' 'a'' 'new'' 'personal'' 'a
{%'' 'data'' 'reusables.user''
'-settings.personal_access_tokens'' '%}
3.'' 'Next'' 'to'' 'the'' 'token'' 'you'd'' 'like'' 'to'' 'authorize,'' 'click'' '**Configure'' 'SSO**.'' '{%'' 'data'' 'reusables.saml.authenticate''
'-with''
'-saml''
'-at''
'-least''
'-once'' '%}'' '![Screenshot'' 'of'' 'the'' 'dropdown'' 'menu'' 'to'' 'configure'' 'SSO'' 'for'' 'a'' 'personal'' 'access'' 'token](/assets/images/help/settings/sso''
'-allowlist''
'-button.png)
'' '![Screenshot'' 'of'' 'the'' 'dropdown'' 'menu'' 'to'' 'configure'' 'SSO'' 'for'' 'a'' '{%'' 'data'' 'variables.product.pat_v1'' '%}](/assets/images/help/settings/sso''
'-allowlist''
'-button.png)
4.'' 'To'' 'the'' 'right'' 'of'' 'the'' 'organization'' 'you'd'' 'like'' 'to'' 'authorize'' 'the'' 'token'' 'for,'' 'click'' '**Authorize**.
'' '![Token'' 'authorize'' 'button](/assets/images/help/settings/token''
'-authorize''
'-button.png)##'' 'Further'' 'reading'' '"[Creating'' 'a'' 'personal'' 'access'' 'token](/authentication/keeping''
'-your''
'-account''
'-and''
'-data''
'-secure/creating''
'-a''
'-personal''
'-access''
'-token)"
'' '"[Creating'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}](/github/authenticating''
'-to''
'-github/creating''
'-a''
'-personal''
'-access''
'-token)"
'' '"[About'' 'authentication'' 'with'' 'SAML'' 'single'' 'sign''
'-on](/articles/about''
'-authentication''
'-with''
'-saml''
'-single''
'-sign''
'-on)"
2'' ''' '
content/authentication/connecting''
'-to''
'-github''
'-with''
'-ssh/about''
'-ssh.md
'@'@'' '''
'-1,6'' '+1,6'' ''@'@
''
'-
title:'' 'About'' 'SSH
intro:'' ''Using'' 'the'' 'SSH'' 'protocol,'' 'you'' 'can'' 'connect'' 'and'' 'authenticate'' 'to'' 'remote'' 'servers'' 'and'' 'services.'' 'With'' 'SSH'' 'keys,'' 'you'' 'can'' 'connect'' 'to'' '{%'' 'data'' 'variables.product.product_name'' '%}'' 'without'' 'supplying'' 'your'' 'username'' 'and'' 'personal'' 'access'' 'token'' 'at'' 'each'' 'visit.{%'' 'ifversion'' 'ssh''
'-commit''
'-verification'' '%}'' 'You'' 'can'' 'also'' 'use'' 'an'' 'SSH'' 'key'' 'to'' 'sign'' 'commits.{%'' 'endif'' '%}'
intro:'' ''Using'' 'the'' 'SSH'' 'protocol,'' 'you'' 'can'' 'connect'' 'and'' 'authenticate'' 'to'' 'remote'' 'servers'' 'and'' 'services.'' 'With'' 'SSH'' 'keys,'' 'you'' 'can'' 'connect'' 'to'' '{%'' 'data'' 'variables.product.product_name'' '%}'' 'without'' 'supplying'' 'your'' 'username'' 'and'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'at'' 'each'' 'visit.{%'' 'ifversion'' 'ssh''
'-commit''
'-verification'' '%}'' 'You'' 'can'' 'also'' 'use'' 'an'' 'SSH'' 'key'' 'to'' 'sign'' 'commits.{%'' 'endif'' '%}'
redirect_from:
'' '/articles/about''
'-ssh
'' '/github/authenticating''
'-to''
'-github/about''
'-ssh
16'' ''' '
...tication/keeping''
'-your''
'-account''
'-and''
'-data''
'-secure/about''
'-authentication''
'-to''
'-github.md
'@'@'' '''
'-22,7'' '+22,7'' ''@'@'' 'You'' 'can'' 'access'' 'your'' 'resources'' 'in'' '{%'' 'data'' 'variables.product.product_name'' '%}'' 'in'' 'a
{%'' 'ifversion'' 'not'' 'fpt'' '%}
'' 'Your'' 'identity'' 'provider'' '(IdP){%'' 'endif'' '%}{%'' 'ifversion'' 'not'' 'ghae'' '%}
'' 'Username'' 'and'' 'password'' 'with'' 'two''
'-factor'' 'authentication{%'' 'endif'' '%}
'' 'Personal'' 'access'' 'token
'' '{%'' 'data'' 'variables.product.pat_generic_caps'' '%}
'' 'SSH'' 'key##'' 'Authenticating'' 'in'' 'your'' 'browser
'@'@'' '''
'-67,8'' '+67,8'' ''@'@'' 'You'' 'can'' 'authenticate'' 'with'' '{%'' 'data'' 'variables.product.prodname_desktop'' '%}'' 'using'' 'yoYou'' 'can'' 'authenticate'' 'with'' 'the'' 'API'' 'in'' 'different'' 'ways.'' '**Personal'' 'access'' 'tokens**
'' ''' ''' 'In'' 'limited'' 'situations,'' 'such'' 'as'' 'testing,'' 'you'' 'can'' 'use'' 'a'' 'personal'' 'access'' 'token'' 'to'' 'access'' 'the'' 'API.'' 'Using'' 'a'' 'personal'' 'access'' 'token'' 'enables'' 'you'' 'to'' 'revoke'' 'access'' 'at'' 'any'' 'time.'' 'For'' 'more'' 'information,'' 'see'' '"[Creating'' 'a'' 'personal'' 'access'' 'token](/github/authenticating''
'-to''
'-github/creating''
'-a''
'-personal''
'-access''
'-token)."
'' '**{%'' 'data'' 'variables.product.pat_generic_caps'' '%}s**
'' ''' ''' 'In'' 'limited'' 'situations,'' 'such'' 'as'' 'testing,'' 'you'' 'can'' 'use'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'to'' 'access'' 'the'' 'API.'' 'Using'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'enables'' 'you'' 'to'' 'revoke'' 'access'' 'at'' 'any'' 'time.'' 'For'' 'more'' 'information,'' 'see'' '"[Creating'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}](/github/authenticating''
'-to''
'-github/creating''
'-a''
'-personal''
'-access''
'-token)."
'' '**Web'' 'application'' 'flow**
'' ''' ''' 'For'' 'OAuth'' 'Apps'' 'in'' 'production,'' 'you'' 'should'' 'authenticate'' 'using'' 'the'' 'web'' 'application'' 'flow.'' 'For'' 'more'' 'information,'' 'see'' '"[Authorizing'' 'OAuth'' 'Apps](/apps/building''
'-oauth''
'-apps/authorizing''
'-oauth''
'-apps/#web''
'-application''
'-flow)."
'' '**GitHub'' 'Apps**
'@'@'' '''
'-82,30'' '+82,30'' ''@'@'' 'You'' 'can'' 'access'' 'repositories'' 'on'' '{%'' 'data'' 'variables.product.product_name'' '%}'' 'from'' 'thYou'' 'can'' 'work'' 'with'' 'all'' 'repositories'' 'on'' '{%'' 'data'' 'variables.product.product_name'' '%}'' 'over'' 'HTTPS,'' 'even'' 'if'' 'you'' 'are'' 'behind'' 'a'' 'firewall'' 'or'' 'proxy.If'' 'you'' 'authenticate'' 'with'' '{%'' 'data'' 'variables.product.prodname_cli'' '%},'' 'you'' 'can'' 'either'' 'authenticate'' 'with'' 'a'' 'personal'' 'access'' 'token'' 'or'' 'via'' 'the'' 'web'' 'browser.'' 'For'' 'more'' 'information'' 'about'' 'authenticating'' 'with'' '{%'' 'data'' 'variables.product.prodname_cli'' '%},'' 'see'' '[`gh'' 'auth'' 'login`](https://cli.github.com/manual/gh_auth_login).
If'' 'you'' 'authenticate'' 'with'' '{%'' 'data'' 'variables.product.prodname_cli'' '%},'' 'you'' 'can'' 'either'' 'authenticate'' 'with'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'or'' 'via'' 'the'' 'web'' 'browser.'' 'For'' 'more'' 'information'' 'about'' 'authenticating'' 'with'' '{%'' 'data'' 'variables.product.prodname_cli'' '%},'' 'see'' '[`gh'' 'auth'' 'login`](https://cli.github.com/manual/gh_auth_login).If'' 'you'' 'authenticate'' 'without'' '{%'' 'data'' 'variables.product.prodname_cli'' '%},'' 'you'' 'must'' 'authenticate'' 'with'' 'a'' 'personal'' 'access'' 'token.'' '{%'' 'data'' 'reusables.user''
'-settings.password''
'-authentication''
'-deprecation'' '%}'' 'Every'' 'time'' 'you'' 'use'' 'Git'' 'to'' 'authenticate'' 'with'' '{%'' 'data'' 'variables.product.product_name'' '%},'' 'you'll'' 'be'' 'prompted'' 'to'' 'enter'' 'your'' 'credentials'' 'to'' 'authenticate'' 'with'' '{%'' 'data'' 'variables.product.product_name'' '%},'' 'unless'' 'you'' 'cache'' 'them'' 'with'' 'a'' '[credential'' 'helper](/github/getting''
'-started''
'-with''
'-github/caching''
'-your''
'-github''
'-credentials''
'-in''
'-git).
If'' 'you'' 'authenticate'' 'without'' '{%'' 'data'' 'variables.product.prodname_cli'' '%},'' 'you'' 'must'' 'authenticate'' 'with'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}.'' '{%'' 'data'' 'reusables.user''
'-settings.password''
'-authentication''
'-deprecation'' '%}'' 'Every'' 'time'' 'you'' 'use'' 'Git'' 'to'' 'authenticate'' 'with'' '{%'' 'data'' 'variables.product.product_name'' '%},'' 'you'll'' 'be'' 'prompted'' 'to'' 'enter'' 'your'' 'credentials'' 'to'' 'authenticate'' 'with'' '{%'' 'data'' 'variables.product.product_name'' '%},'' 'unless'' 'you'' 'cache'' 'them'' 'with'' 'a'' '[credential'' 'helper](/github/getting''
'-started''
'-with''
'-github/caching''
'-your''
'-github''
'-credentials''
'-in''
'-git).###'' 'SSHYou'' 'can'' 'work'' 'with'' 'all'' 'repositories'' 'on'' '{%'' 'data'' 'variables.product.product_name'' '%}'' 'over'' 'SSH,'' 'although'' 'firewalls'' 'and'' 'proxies'' 'might'' 'refuse'' 'to'' 'allow'' 'SSH'' 'connections.If'' 'you'' 'authenticate'' 'with'' '{%'' 'data'' 'variables.product.prodname_cli'' '%},'' 'the'' 'CLI'' 'will'' 'find'' 'SSH'' 'public'' 'keys'' 'on'' 'your'' 'machine'' 'and'' 'will'' 'prompt'' 'you'' 'to'' 'select'' 'one'' 'for'' 'upload.'' 'If'' '{%'' 'data'' 'variables.product.prodname_cli'' '%}'' 'does'' 'not'' 'find'' 'a'' 'SSH'' 'public'' 'key'' 'for'' 'upload,'' 'it'' 'can'' 'generate'' 'a'' 'new'' 'SSH'' 'public/private'' 'keypair'' 'and'' 'upload'' 'the'' 'public'' 'key'' 'to'' 'your'' 'account'' 'on'' '{%'' 'ifversion'' 'ghae'' '%}{%'' 'data'' 'variables.product.product_name'' '%}{%'' 'else'' '%}{%'' 'data'' 'variables.location.product_location'' '%}{%'' 'endif'' '%}.'' 'Then,'' 'you'' 'can'' 'either'' 'authenticate'' 'with'' 'a'' 'personal'' 'access'' 'token'' 'or'' 'via'' 'the'' 'web'' 'browser.'' 'For'' 'more'' 'information'' 'about'' 'authenticating'' 'with'' '{%'' 'data'' 'variables.product.prodname_cli'' '%},'' 'see'' '[`gh'' 'auth'' 'login`](https://cli.github.com/manual/gh_auth_login).
If'' 'you'' 'authenticate'' 'with'' '{%'' 'data'' 'variables.product.prodname_cli'' '%},'' 'the'' 'CLI'' 'will'' 'find'' 'SSH'' 'public'' 'keys'' 'on'' 'your'' 'machine'' 'and'' 'will'' 'prompt'' 'you'' 'to'' 'select'' 'one'' 'for'' 'upload.'' 'If'' '{%'' 'data'' 'variables.product.prodname_cli'' '%}'' 'does'' 'not'' 'find'' 'a'' 'SSH'' 'public'' 'key'' 'for'' 'upload,'' 'it'' 'can'' 'generate'' 'a'' 'new'' 'SSH'' 'public/private'' 'keypair'' 'and'' 'upload'' 'the'' 'public'' 'key'' 'to'' 'your'' 'account'' 'on'' '{%'' 'ifversion'' 'ghae'' '%}{%'' 'data'' 'variables.product.product_name'' '%}{%'' 'else'' '%}{%'' 'data'' 'variables.location.product_location'' '%}{%'' 'endif'' '%}.'' 'Then,'' 'you'' 'can'' 'either'' 'authenticate'' 'with'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'or'' 'via'' 'the'' 'web'' 'browser.'' 'For'' 'more'' 'information'' 'about'' 'authenticating'' 'with'' '{%'' 'data'' 'variables.product.prodname_cli'' '%},'' 'see'' '[`gh'' 'auth'' 'login`](https://cli.github.com/manual/gh_auth_login).If'' 'you'' 'authenticate'' 'without'' '{%'' 'data'' 'variables.product.prodname_cli'' '%},'' 'you'' 'will'' 'need'' 'to'' 'generate'' 'an'' 'SSH'' 'public/private'' 'keypair'' 'on'' 'your'' 'local'' 'machine'' 'and'' 'add'' 'the'' 'public'' 'key'' 'to'' 'your'' 'account'' 'on'' '{%'' 'ifversion'' 'ghae'' '%}{%'' 'data'' 'variables.product.product_name'' '%}{%'' 'else'' '%}{%'' 'data'' 'variables.location.product_location'' '%}{%'' 'endif'' '%}.'' 'For'' 'more'' 'information,'' 'see'' '"[Generating'' 'a'' 'new'' 'SSH'' 'key'' 'and'' 'adding'' 'it'' 'to'' 'the'' 'ssh''
'-agent](/github/authenticating''
'-to''
'-github/generating''
'-a''
'-new''
'-ssh''
'-key''
'-and''
'-adding''
'-it''
'-to''
'-the''
'-ssh''
'-agent)."'' 'Every'' 'time'' 'you'' 'use'' 'Git'' 'to'' 'authenticate'' 'with'' '{%'' 'data'' 'variables.product.product_name'' '%},'' 'you'll'' 'be'' 'prompted'' 'to'' 'enter'' 'your'' 'SSH'' 'key'' 'passphrase,'' 'unless'' 'you've'' '[stored'' 'the'' 'key](/github/authenticating''
'-to''
'-github/generating''
'-a''
'-new''
'-ssh''
'-key''
'-and''
'-adding''
'-it''
'-to''
'-the''
'-ssh''
'-agent#adding''
'-your''
'-ssh''
'-key''
'-to''
'-the''
'-ssh''
'-agent).{%'' 'ifversion'' 'fpt'' 'or'' 'ghec'' '%}
###'' 'Authorizing'' 'for'' 'SAML'' 'single'' 'sign''
'-onTo'' 'use'' 'a'' 'personal'' 'access'' 'token'' 'or'' 'SSH'' 'key'' 'to'' 'access'' 'resources'' 'owned'' 'by'' 'an'' 'organization'' 'that'' 'uses'' 'SAML'' 'single'' 'sign''
'-on,'' 'you'' 'must'' 'also'' 'authorize'' 'the'' 'personal'' 'token'' 'or'' 'SSH'' 'key.'' 'For'' 'more'' 'information,'' 'see'' '"[Authorizing'' 'a'' 'personal'' 'access'' 'token'' 'for'' 'use'' 'with'' 'SAML'' 'single'' 'sign''
'-on](/enterprise''
'-cloud'@latest/authentication/authenticating''
'-with''
'-saml''
'-single''
'-sign''
'-on/authorizing''
'-a''
'-personal''
'-access''
'-token''
'-for''
'-use''
'-with''
'-saml''
'-single''
'-sign''
'-on)"'' 'or'' '"[Authorizing'' 'an'' 'SSH'' 'key'' 'for'' 'use'' 'with'' 'SAML'' 'single'' 'sign''
'-on](/enterprise''
'-cloud'@latest/authentication/authenticating''
'-with''
'-saml''
'-single''
'-sign''
'-on/authorizing''
'-an''
'-ssh''
'-key''
'-for''
'-use''
'-with''
'-saml''
'-single''
'-sign''
'-on){%'' 'ifversion'' 'fpt'' '%}"'' 'in'' 'the'' '{%'' 'data'' 'variables.product.prodname_ghe_cloud'' '%}'' 'documentation.{%'' 'else'' '%}."{%'' 'endif'' '%}{%'' 'endif'' '%}
To'' 'use'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'or'' 'SSH'' 'key'' 'to'' 'access'' 'resources'' 'owned'' 'by'' 'an'' 'organization'' 'that'' 'uses'' 'SAML'' 'single'' 'sign''
'-on,'' 'you'' 'must'' 'also'' 'authorize'' 'the'' 'personal'' 'token'' 'or'' 'SSH'' 'key.'' 'For'' 'more'' 'information,'' 'see'' '"[Authorizing'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'for'' 'use'' 'with'' 'SAML'' 'single'' 'sign''
'-on](/enterprise''
'-cloud'@latest/authentication/authenticating''
'-with''
'-saml''
'-single''
'-sign''
'-on/authorizing''
'-a''
'-personal''
'-access''
'-token''
'-for''
'-use''
'-with''
'-saml''
'-single''
'-sign''
'-on)"'' 'or'' '"[Authorizing'' 'an'' 'SSH'' 'key'' 'for'' 'use'' 'with'' 'SAML'' 'single'' 'sign''
'-on](/enterprise''
'-cloud'@latest/authentication/authenticating''
'-with''
'-saml''
'-single''
'-sign''
'-on/authorizing''
'-an''
'-ssh''
'-key''
'-for''
'-use''
'-with''
'-saml''
'-single''
'-sign''
'-on){%'' 'ifversion'' 'fpt'' '%}"'' 'in'' 'the'' '{%'' 'data'' 'variables.product.prodname_ghe_cloud'' '%}'' 'documentation.{%'' 'else'' '%}."{%'' 'endif'' '%}{%'' 'endif'' '%}##'' '{%'' 'data'' 'variables.product.company_short'' '%}'s'' 'token'' 'formats{%'' 'data'' 'variables.product.company_short'' '%}'' 'issues'' 'tokens'' 'that'' 'begin'' 'with'' 'a'' 'prefix'' 'to'' 'indicate'' 'the'' 'token's'' 'type.|'' 'Token'' 'type'' '|'' 'Prefix'' '|'' 'More'' 'information'' '|
|'' ':'' '|'' ':'' '|'' ':'' '|
|'' 'Personal'' 'access'' 'token'' '|'' '`ghp_`'' '|'' '"[Creating'' 'a'' 'personal'' 'access'' 'token](/github/authenticating''
'-to''
'-github/creating''
'-a''
'-personal''
'-access''
'-token)"'' '|
|'' '{%'' 'data'' 'variables.product.pat_generic_caps'' '%}'' '|'' '`ghp_`'' '|'' '"[Creating'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}](/github/authenticating''
'-to''
'-github/creating''
'-a''
'-personal''
'-access''
'-token)"'' '|
|'' 'OAuth'' 'access'' 'token'' '|'' '`gho_`'' '|'' '"[Authorizing'' '{%'' 'data'' 'variables.product.prodname_oauth_apps'' '%}](/developers/apps/authorizing''
'-oauth''
'-apps)"'' '|
|'' 'User''
'-to''
'-server'' 'token'' 'for'' 'a'' '{%'' 'data'' 'variables.product.prodname_github_app'' '%}'' '|'' '`ghu_`'' '|'' '"[Identifying'' 'and'' 'authorizing'' 'users'' 'for'' '{%'' 'data'' 'variables.product.prodname_github_apps'' '%}](/developers/apps/identifying''
'-and''
'-authorizing''
'-users''
'-for''
'-github''
'-apps)"'' '|
|'' 'Server''
'-to''
'-server'' 'token'' 'for'' 'a'' '{%'' 'data'' 'variables.product.prodname_github_app'' '%}'' '|'' '`ghs_`'' '|'' '"[Authenticating'' 'with'' '{%'' 'data'' 'variables.product.prodname_github_apps'' '%}](/developers/apps/authenticating''
'-with''
'-github''
'-apps#authenticating''
'-as''
'-an''
'-installation)"'' '|
109'' ''' '
...cation/keeping''
'-your''
'-account''
'-and''
'-data''
'-secure/creating''
'-a''
'-personal''
'-access''
'-token.md
Large'' 'diffs'' 'are'' 'not'' 'rendered'' 'by'' 'default.11'' ''' '
...ication/keeping''
'-your''
'-account''
'-and''
'-data''
'-secure/token''
'-expiration''
'-and''
'-revocation.md
'@'@'' '''
'-20,28'' '+20,29'' ''@'@'' 'This'' 'article'' 'explains'' 'the'' 'possible'' 'reasons'' 'your'' '{%'' 'data'' 'variables.product.produc{%'' 'note'' '%}**Note:**'' 'When'' 'a'' 'personal'' 'access'' 'token'' 'or'' 'OAuth'' 'token'' 'expires'' 'or'' 'is'' 'revoked,'' 'you'' 'may'' 'see'' 'an'' '`oauth_authorization.destroy`'' 'action'' 'in'' 'your'' 'security'' 'log.'' 'For'' 'more'' 'information,'' 'see'' '"[Reviewing'' 'your'' 'security'' 'log](/github/authenticating''
'-to''
'-github/keeping''
'-your''
'-account''
'-and''
'-data''
'-secure/reviewing''
'-your''
'-security''
'-log)."
**Note:**'' 'When'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'or'' 'OAuth'' 'token'' 'expires'' 'or'' 'is'' 'revoked,'' 'you'' 'may'' 'see'' 'an'' '`oauth_authorization.destroy`'' 'action'' 'in'' 'your'' 'security'' 'log.'' 'For'' 'more'' 'information,'' 'see'' '"[Reviewing'' 'your'' 'security'' 'log](/github/authenticating''
'-to''
'-github/keeping''
'-your''
'-account''
'-and''
'-data''
'-secure/reviewing''
'-your''
'-security''
'-log)."{%'' 'endnote'' '%}{%'' 'ifversion'' 'fpt'' 'or'' 'ghae'' 'or'' 'ghes'' '>'' '3.2'' 'or'' 'ghec'' '%}
##'' 'Token'' 'revoked'' 'after'' 'reaching'' 'its'' 'expiration'' 'dateWhen'' 'you'' 'create'' 'a'' 'personal'' 'access'' 'token,'' 'we'' 'recommend'' 'that'' 'you'' 'set'' 'an'' 'expiration'' 'for'' 'your'' 'token.'' 'Upon'' 'reaching'' 'your'' 'token's'' 'expiration'' 'date,'' 'the'' 'token'' 'is'' 'automatically'' 'revoked.'' 'For'' 'more'' 'information,'' 'see'' '"[Creating'' 'a'' 'personal'' 'access'' 'token](/github/authenticating''
'-to''
'-github/keeping''
'-your''
'-account''
'-and''
'-data''
'-secure/creating''
'-a''
'-personal''
'-access''
'-token)."
When'' 'you'' 'create'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%},'' 'we'' 'recommend'' 'that'' 'you'' 'set'' 'an'' 'expiration'' 'for'' 'your'' 'token.'' 'Upon'' 'reaching'' 'your'' 'token's'' 'expiration'' 'date,'' 'the'' 'token'' 'is'' 'automatically'' 'revoked.'' 'For'' 'more'' 'information,'' 'see'' '"[Creating'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}](/github/authenticating''
'-to''
'-github/keeping''
'-your''
'-account''
'-and''
'-data''
'-secure/creating''
'-a''
'-personal''
'-access''
'-token)."
{%'' 'endif'' '%}{%'' 'ifversion'' 'fpt'' 'or'' 'ghec'' '%}
##'' 'Token'' 'revoked'' 'when'' 'pushed'' 'to'' 'a'' 'public'' 'repository'' 'or'' 'public'' 'gistIf'' 'a'' 'valid'' 'OAuth'' 'token,'' '{%'' 'data'' 'variables.product.prodname_github_app'' '%}'' 'token,'' 'or'' 'personal'' 'access'' 'token'' 'is'' 'pushed'' 'to'' 'a'' 'public'' 'repository'' 'or'' 'public'' 'gist,'' 'the'' 'token'' 'will'' 'be'' 'automatically'' 'revoked.'' '
If'' 'a'' 'valid'' 'OAuth'' 'token,'' '{%'' 'data'' 'variables.product.prodname_github_app'' '%}'' 'token,'' 'or'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'is'' 'pushed'' 'to'' 'a'' 'public'' 'repository'' 'or'' 'public'' 'gist,'' 'the'' 'token'' 'will'' 'be'' 'automatically'' 'revoked.'' 'OAuth'' 'tokens'' 'and'' 'personal'' '{%'' 'data'' 'variables.product.pat_v1_plural'' '%}'' 'pushed'' 'to'' 'public'' 'repositories'' 'and'' 'public'' 'gists'' 'will'' 'only'' 'be'' 'revoked'' 'if'' 'the'' 'token'' 'has'' 'scopes.{%'' 'ifversion'' 'pat''
'-v2'' '%}'' '{%'' 'data'' 'variables.product.pat_v2_caps'' '%}s'' 'will'' 'always'' 'be'' 'revoked.{%'' 'endif'' '%}OAuth'' 'tokens'' 'and'' 'personal'' 'access'' 'tokens'' 'pushed'' 'to'' 'public'' 'repositories'' 'and'' 'public'' 'gists'' 'will'' 'only'' 'be'' 'revoked'' 'if'' 'the'' 'token'' 'has'' 'scopes.
{%'' 'endif'' '%}{%'' 'ifversion'' 'fpt'' 'or'' 'ghec'' '%}
##'' 'Token'' 'expired'' 'due'' 'to'' 'lack'' 'of'' 'use{%'' 'data'' 'variables.product.product_name'' '%}'' 'will'' 'automatically'' 'revoke'' 'an'' 'OAuth'' 'token'' 'or'' 'personal'' 'access'' 'token'' 'when'' 'the'' 'token'' 'hasn't'' 'been'' 'used'' 'in'' 'one'' 'year.
{%'' 'data'' 'variables.product.product_name'' '%}'' 'will'' 'automatically'' 'revoke'' 'an'' 'OAuth'' 'token'' 'or'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'when'' 'the'' 'token'' 'hasn't'' 'been'' 'used'' 'in'' 'one'' 'year.
{%'' 'endif'' '%}##'' 'Token'' 'revoked'' 'by'' 'the'' 'user
2'' ''' '
...keeping''
'-your''
'-account''
'-and''
'-data''
'-secure/updating''
'-your''
'-github''
'-access''
'-credentials.md
'@'@'' '''
'-65,7'' '+65,7'' ''@'@'' 'For'' 'greater'' 'security,'' 'enable'' 'two''
'-factor'' 'authentication'' 'in'' 'addition'' 'to'' 'changing'' 'y
{%'' 'endif'' '%}
##'' 'Updating'' 'your'' 'access'' 'tokensSee'' '"[Reviewing'' 'your'' 'authorized'' 'integrations](/articles/reviewing''
'-your''
'-authorized''
'-integrations)"'' 'for'' 'instructions'' 'on'' 'reviewing'' 'and'' 'deleting'' 'access'' 'tokens.'' 'To'' 'generate'' 'new'' 'access'' 'tokens,'' 'see'' '"[Creating'' 'a'' 'personal'' 'access'' 'token](/github/authenticating''
'-to''
'-github/creating''
'-a''
'-personal''
'-access''
'-token)."
See'' '"[Reviewing'' 'your'' 'authorized'' 'integrations](/articles/reviewing''
'-your''
'-authorized''
'-integrations)"'' 'for'' 'instructions'' 'on'' 'reviewing'' 'and'' 'deleting'' 'access'' 'tokens.'' 'To'' 'generate'' 'new'' 'access'' 'tokens,'' 'see'' '"[Creating'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}](/github/authenticating''
'-to''
'-github/creating''
'-a''
'-personal''
'-access''
'-token)."{%'' 'ifversion'' 'not'' 'ghae'' '%}10'' ''' '
...o''
'-factor''
'-authentication''
'-2fa/accessing''
'-github''
'-using''
'-two''
'-factor''
'-authentication.md
'@'@'' '''
'-59,7'' '+59,7'' ''@'@'' 'If'' 'you'' 'have'' 'installed'' 'and'' 'signed'' 'in'' 'to'' '{%'' 'data'' 'variables.product.prodname_mobile##'' 'Using'' 'two''
'-factor'' 'authentication'' 'with'' 'the'' 'command'' 'lineAfter'' 'you've'' 'enabled'' '2FA,'' 'you'' 'will'' 'no'' 'longer'' 'use'' 'your'' 'password'' 'to'' 'access'' '{%'' 'data'' 'variables.product.product_name'' '%}'' 'on'' 'the'' 'command'' 'line.'' 'Instead,'' 'use'' 'Git'' 'Credential'' 'Manager,'' 'a'' 'personal'' 'access'' 'token,'' 'or'' 'an'' 'SSH'' 'key.
After'' 'you've'' 'enabled'' '2FA,'' 'you'' 'will'' 'no'' 'longer'' 'use'' 'your'' 'password'' 'to'' 'access'' '{%'' 'data'' 'variables.product.product_name'' '%}'' 'on'' 'the'' 'command'' 'line.'' 'Instead,'' 'use'' 'Git'' 'Credential'' 'Manager,'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%},'' 'or'' 'an'' 'SSH'' 'key.###'' 'Authenticating'' 'on'' 'the'' 'command'' 'line'' 'using'' 'Git'' 'Credential'' 'Manager'@'@'' '''
'-69,19'' '+69,19'' ''@'@'' 'Setup'' 'instructions'' 'vary'' 'based'' 'on'' 'your'' 'computer's'' 'operating'' 'system.'' 'For'' 'more'' 'info###'' 'Authenticating'' 'on'' 'the'' 'command'' 'line'' 'using'' 'HTTPSAfter'' 'you've'' 'enabled'' '2FA,'' 'you'' 'must'' 'create'' 'a'' 'personal'' 'access'' 'token'' 'to'' 'use'' 'as'' 'a'' 'password'' 'when'' 'authenticating'' 'to'' '{%'' 'data'' 'variables.product.product_name'' '%}'' 'on'' 'the'' 'command'' 'line'' 'using'' 'HTTPS'' 'URLs.
After'' 'you've'' 'enabled'' '2FA,'' 'you'' 'must'' 'create'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'to'' 'use'' 'as'' 'a'' 'password'' 'when'' 'authenticating'' 'to'' '{%'' 'data'' 'variables.product.product_name'' '%}'' 'on'' 'the'' 'command'' 'line'' 'using'' 'HTTPS'' 'URLs.When'' 'prompted'' 'for'' 'a'' 'username'' 'and'' 'password'' 'on'' 'the'' 'command'' 'line,'' 'use'' 'your'' '{%'' 'data'' 'variables.product.product_name'' '%}'' 'username'' 'and'' 'personal'' 'access'' 'token.'' 'The'' 'command'' 'line'' 'prompt'' 'won't'' 'specify'' 'that'' 'you'' 'should'' 'enter'' 'your'' 'personal'' 'access'' 'token'' 'when'' 'it'' 'asks'' 'for'' 'your'' 'password.
When'' 'prompted'' 'for'' 'a'' 'username'' 'and'' 'password'' 'on'' 'the'' 'command'' 'line,'' 'use'' 'your'' '{%'' 'data'' 'variables.product.product_name'' '%}'' 'username'' 'and'' '{%'' 'data'' 'variables.product.pat_generic'' '%}.'' 'The'' 'command'' 'line'' 'prompt'' 'won't'' 'specify'' 'that'' 'you'' 'should'' 'enter'' 'your'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'when'' 'it'' 'asks'' 'for'' 'your'' 'password.For'' 'more'' 'information,'' 'see'' '"[Creating'' 'a'' 'personal'' 'access'' 'token](/github/authenticating''
'-to''
'-github/creating''
'-a''
'-personal''
'-access''
'-token)."
For'' 'more'' 'information,'' 'see'' '"[Creating'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}](/github/authenticating''
'-to''
'-github/creating''
'-a''
'-personal''
'-access''
'-token)."###'' 'Authenticating'' 'on'' 'the'' 'command'' 'line'' 'using'' 'SSHEnabling'' '2FA'' 'doesn't'' 'change'' 'how'' 'you'' 'authenticate'' 'to'' '{%'' 'data'' 'variables.product.product_name'' '%}'' 'on'' 'the'' 'command'' 'line'' 'using'' 'SSH'' 'URLs.'' 'For'' 'more'' 'information'' 'about'' 'setting'' 'up'' 'and'' 'using'' 'an'' 'SSH'' 'key,'' 'see'' '"[Connecting'' 'to'' '{%'' 'data'' 'variables.product.prodname_dotcom'' '%}'' 'with'' 'SSH](/articles/connecting''
'-to''
'-github''
'-with''
'-ssh/)."##'' 'Using'' 'two''
'-factor'' 'authentication'' 'to'' 'access'' 'a'' 'repository'' 'using'' 'SubversionWhen'' 'you'' 'access'' 'a'' 'repository'' 'via'' 'Subversion,'' 'you'' 'must'' 'provide'' 'a'' 'personal'' 'access'' 'token'' 'instead'' 'of'' 'entering'' 'your'' 'password.'' 'For'' 'more'' 'information,'' 'see'' '"[Creating'' 'a'' 'personal'' 'access'' 'token](/github/authenticating''
'-to''
'-github/creating''
'-a''
'-personal''
'-access''
'-token)."
When'' 'you'' 'access'' 'a'' 'repository'' 'via'' 'Subversion,'' 'you'' 'must'' 'provide'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'instead'' 'of'' 'entering'' 'your'' 'password.'' 'For'' 'more'' 'information,'' 'see'' '"[Creating'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}](/github/authenticating''
'-to''
'-github/creating''
'-a''
'-personal''
'-access''
'-token)."##'' 'Troubleshooting2'' ''' '
...unt''
'-with''
'-two''
'-factor''
'-authentication''
'-2fa/configuring''
'-two''
'-factor''
'-authentication.md
'@'@'' '''
'-152,4'' '+152,4'' ''@'@'' 'After'' 'signing'' 'in,'' 'you'' 'can'' 'now'' 'use'' 'your'' 'device'' 'for'' '2FA.
'' '"[Configuring'' 'two''
'-factor'' 'authentication'' 'recovery'' 'methods](/articles/configuring''
'-two''
'-factor''
'-authentication''
'-recovery''
'-methods)"
'' '"[Accessing'' '{%'' 'data'' 'variables.product.prodname_dotcom'' '%}'' 'using'' 'two''
'-factor'' 'authentication](/articles/accessing''
'-github''
'-using''
'-two''
'-factor''
'-authentication)"
'' '"[Recovering'' 'your'' 'account'' 'if'' 'you'' 'lose'' 'your'' '2FA'' 'credentials](/articles/recovering''
'-your''
'-account''
'-if''
'-you''
'-lose''
'-your''
'-2fa''
'-credentials)"
'' '"[Creating'' 'a'' 'personal'' 'access'' 'token](/github/authenticating''
'-to''
'-github/creating''
'-a''
'-personal''
'-access''
'-token)"
'' '"[Creating'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}](/github/authenticating''
'-to''
'-github/creating''
'-a''
'-personal''
'-access''
'-token)"
4'' ''' '
...''
'-authentication''
'-2fa/recovering''
'-your''
'-account''
'-if''
'-you''
'-lose''
'-your''
'-2fa''
'-credentials.md
'@'@'' '''
'-62,7'' '+62,7'' ''@'@'' 'If'' 'you'' 'lose'' 'access'' 'to'' 'your'' 'primary'' 'TOTP'' 'app'' 'or'' 'phone'' 'number,'' 'you'' 'can'' 'provide'' 'a'' 't
If'' 'you'' 'configured'' 'two''
'-factor'' 'authentication'' 'using'' 'a'' 'security'' 'key,'' 'you'' 'can'' 'use'' 'your'' 'security'' 'key'' 'as'' 'a'' 'secondary'' 'authentication'' 'method'' 'to'' 'automatically'' 'regain'' 'access'' 'to'' 'your'' 'account.'' 'For'' 'more'' 'information,'' 'see'' '"[Configuring'' 'two''
'-factor'' 'authentication](/authentication/securing''
'-your''
'-account''
'-with''
'-two''
'-factor''
'-authentication''
'-2fa/configuring''
'-two''
'-factor''
'-authentication#configuring''
'-two''
'-factor''
'-authentication''
'-using''
'-a''
'-security''
'-key)."{%'' 'ifversion'' 'fpt'' 'or'' 'ghec'' '%}
##'' 'Authenticating'' 'with'' 'a'' 'verified'' 'device,'' 'SSH'' 'token,'' 'or'' 'personal'' 'access'' 'token
##'' 'Authenticating'' 'with'' 'a'' 'verified'' 'device,'' 'SSH'' 'token,'' 'or'' '{%'' 'data'' 'variables.product.pat_generic'' '%}If'' 'you'' 'know'' 'your'' 'password'' 'for'' '{%'' 'data'' 'variables.location.product_location'' '%}'' 'but'' 'don't'' 'have'' 'the'' 'two''
'-factor'' 'authentication'' 'credentials'' 'or'' 'your'' 'two''
'-factor'' 'authentication'' 'recovery'' 'codes,'' 'you'' 'can'' 'have'' 'a'' 'one''
'-time'' 'password'' 'sent'' 'to'' 'your'' 'verified'' 'email'' 'address'' 'to'' 'begin'' 'the'' 'verification'' 'process'' 'and'' 'regain'' 'access'' 'to'' 'your'' 'account.'@'@'' '''
'-102,7'' '+102,7'' ''@'@'' 'You'' 'can'' 'use'' 'your'' 'two''
'-factor'' 'authentication'' 'credentials'' 'or'' 'two''
'-factor'' 'authenticat
1.'' 'Choose'' 'an'' 'alternative'' 'verification'' 'factor.
'' ''' ''' 'If'' 'you've'' 'used'' 'your'' 'current'' 'device'' 'to'' 'log'' 'into'' 'this'' 'account'' 'before'' 'and'' 'would'' 'like'' 'to'' 'use'' 'the'' 'device'' 'for'' 'verification,'' 'click'' '**Verify'' 'with'' 'this'' 'device**.
'' ''' ''' 'If'' 'you've'' 'previously'' 'set'' 'up'' 'an'' 'SSH'' 'key'' 'on'' 'this'' 'account'' 'and'' 'would'' 'like'' 'to'' 'use'' 'the'' 'SSH'' 'key'' 'for'' 'verification,'' 'click'' '**SSH'' 'key**.
'' ''' ''' 'If'' 'you've'' 'previously'' 'set'' 'up'' 'a'' 'personal'' 'access'' 'token'' 'and'' 'would'' 'like'' 'to'' 'use'' 'the'' 'personal'' 'access'' 'token'' 'for'' 'verification,'' 'click'' '**Personal'' 'access'' 'token**.
'' ''' ''' 'If'' 'you've'' 'previously'' 'set'' 'up'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'and'' 'would'' 'like'' 'to'' 'use'' 'the'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'for'' 'verification,'' 'click'' '**{%'' 'data'' 'variables.product.pat_generic_caps'' '%}**.'' '![Screenshot'' 'of'' 'buttons'' 'for'' 'alternative'' 'verification](/assets/images/help/2fa/alt''
'-verifications.png)
1.'' 'A'' 'member'' 'of'' '{%'' 'data'' 'variables.contact.github_support'' '%}'' 'will'' 'review'' 'your'' 'request'' 'and'' 'email'' 'you'' 'within'' 'three'' 'business'' 'days.'' 'If'' 'your'' 'request'' 'is'' 'approved,'' 'you'll'' 'receive'' 'a'' 'link'' 'to'' 'complete'' 'your'' 'account'' 'recovery'' 'process.'' 'If'' 'your'' 'request'' 'is'' 'denied,'' 'the'' 'email'' 'will'' 'include'' 'a'' 'way'' 'to'' 'contact'' 'support'' 'with'' 'any'' 'additional'' 'questions.
2'' ''' '
...lling/managing''
'-billing''
'-for''
'-github''
'-packages/about''
'-billing''
'-for''
'-github''
'-packages.md
'@'@'' '''
'-45,7'' '+45,7'' ''@'@'' 'All'' 'data'' 'transferred'' 'out,'' 'when'' 'triggered'' 'by'' '{%'' 'data'' 'variables.product.prodname_a
||Hosted|Self''
'-Hosted|
|''
'-|''
'-|''
'-|
|Access'' 'using'' 'a'' '`GITHUB_TOKEN`|Free|Free|
|Access'' 'using'' 'a'' 'personal'' 'access'' 'token|Free|$|
|Access'' 'using'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}|Free|$|Storage'' 'usage'' 'is'' 'shared'' 'with'' 'build'' 'artifacts'' 'produced'' 'by'' '{%'' 'data'' 'variables.product.prodname_actions'' '%}'' 'for'' 'repositories'' 'owned'' 'by'' 'your'' 'account.'' 'For'' 'more'' 'information,'' 'see'' '"[About'' 'billing'' 'for'' '{%'' 'data'' 'variables.product.prodname_actions'' '%}](/billing/managing''
'-billing''
'-for''
'-github''
'-actions/about''
'-billing''
'-for''
'-github''
'-actions)."2'' ''' '
...''
'-scanning''
'-your''
'-code''
'-for''
'-vulnerabilities''
'-and''
'-errors/configuring''
'-code''
'-scanning.md
'@'@'' '''
'-351,7'' '+351,7'' ''@'@'' 'If'' 'your'' 'workflow'' 'uses'' 'packs'' 'that'' 'are'' 'published'' 'on'' 'a'' '{%'' 'data'' 'variables.product.pr
'' ''' '{%'' 'endraw'' '%}
The'' 'package'' 'patterns'' 'in'' 'the'' 'registries'' 'list'' 'are'' 'examined'' 'in'' 'order,'' 'so'' 'you'' 'should'' 'generally'' 'place'' 'the'' 'most'' 'specific'' 'package'' 'patterns'' 'first.'' 'The'' 'values'' 'for'' 'token'' 'must'' 'be'' 'a'' 'personal'' 'access'' 'token'' 'generated'' 'by'' 'the'' 'GitHub'' 'instance'' 'you'' 'are'' 'downloading'' 'from'' 'with'' 'the'' 'read:packages'' 'permission.'' 'The'' 'package'' 'patterns'' 'in'' 'the'' 'registries'' 'list'' 'are'' 'examined'' 'in'' 'order,'' 'so'' 'you'' 'should'' 'generally'' 'place'' 'the'' 'most'' 'specific'' 'package'' 'patterns'' 'first.'' 'The'' 'values'' 'for'' 'token'' 'must'' 'be'' 'a'' '{%'' 'data'' 'variables.product.pat_v1'' '%}'' 'generated'' 'by'' 'the'' 'GitHub'' 'instance'' 'you'' 'are'' 'downloading'' 'from'' 'with'' 'the'' 'read:packages'' 'permission.Notice'' 'the'' '|'' 'after'' 'the'' 'registries'' 'property'' 'name.'' 'This'' 'is'' 'important'' 'since'' '{%'' 'data'' 'variables.product.prodname_actions'' '%}'' 'inputs'' 'can'' 'only'' 'accept'' 'strings.'' 'Using'' 'the'' '|'' 'converts'' 'the'' 'subsequent'' 'text'' 'to'' 'a'' 'string,'' 'which'' 'is'' 'parsed'' 'later'' 'by'' 'the'' '{%'' 'data'' 'reusables.actions.action''
'-codeql''
'-action''
'-init'' '%}'' 'action.8
...anning''
'-with''
'-your''
'-existing''
'-ci''
'-system/configuring''
'-codeql''
'-cli''
'-in''
'-your''
'-ci''
'-system.md'' ''@'@'' '''
'-187,7'' '+187,7'' ''@'@'' '$'' 'codeql'' 'database'' 'analyze'' '/codeql''
'-dbs/example''
'-repo'' '\{%'' 'data'' 'reusables.code''
'-scanning.upload''
'-sarif''
'-alert''
'-limit'' '%}Before'' 'you'' 'can'' 'upload'' 'results'' 'to'' '{%'' 'data'' 'variables.product.product_name'' '%},'' 'you'' 'must'' 'determine'' 'the'' 'best'' 'way'' 'to'' 'pass'' 'the'' '{%'' 'data'' 'variables.product.prodname_github_app'' '%}'' 'or'' 'personal'' 'access'' 'token'' 'you'' 'created'' 'earlier'' 'to'' 'the'' '{%'' 'data'' 'variables.product.prodname_codeql_cli'' '%}'' '(see'' 'Installing'' '{%'' 'data'' 'variables.product.prodname_codeql_cli'' '%}'' 'in'' 'your'' 'CI'' 'system).'' 'We'' 'recommend'' 'that'' 'you'' 'review'' 'your'' 'CI'' 'system's'' 'guidance'' 'on'' 'the'' 'secure'' 'use'' 'of'' 'a'' 'secret'' 'store.'' 'The'' '{%'' 'data'' 'variables.product.prodname_codeql_cli'' '%}'' 'supports:'' 'Before'' 'you'' 'can'' 'upload'' 'results'' 'to'' '{%'' 'data'' 'variables.product.product_name'' '%},'' 'you'' 'must'' 'determine'' 'the'' 'best'' 'way'' 'to'' 'pass'' 'the'' '{%'' 'data'' 'variables.product.prodname_github_app'' '%}'' 'or'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'you'' 'created'' 'earlier'' 'to'' 'the'' '{%'' 'data'' 'variables.product.prodname_codeql_cli'' '%}'' '(see'' 'Installing'' '{%'' 'data'' 'variables.product.prodname_codeql_cli'' '%}'' 'in'' 'your'' 'CI'' 'system).'' 'We'' 'recommend'' 'that'' 'you'' 'review'' 'your'' 'CI'' 'system's'' 'guidance'' 'on'' 'the'' 'secure'' 'use'' 'of'' 'a'' 'secret'' 'store.'' 'The'' '{%'' 'data'' 'variables.product.prodname_codeql_cli'' '%}'' 'supports:Passing'' 'the'' 'token'' 'to'' 'the'' 'CLI'' 'via'' 'standard'' 'input'' 'using'' 'the'' '''
'-github''
'-auth''
'-stdin'' 'option'' '(recommended).
Saving'' 'the'' 'secret'' 'in'' 'the'' 'environment'' 'variable'' 'GITHUB_TOKEN'' 'and'' 'running'' 'the'' 'CLI'' 'without'' 'including'' 'the'' '''
'-github''
'-auth''
'-stdin'' 'option.'' ''@'@'' '''
'-207,7'' '+207,7'' ''@'@'' 'When'' 'you'' 'have'' 'decided'' 'on'' 'the'' 'most'' 'secure'' 'and'' 'reliable'' 'method'' 'for'' 'your'' 'CI'' 'server,'' '|'' '''
'-commit'' '|'' '{%'' 'octicon'' '"check''
'-circle''
'-fill"'' 'aria''
'-label="Required"'' '%}'' '|'' 'Specify'' 'the'' 'full'' 'SHA'' 'of'' 'the'' 'commit'' 'you'' 'analyzed.'' '|'' '''
'-sarif'' '|'' '{%'' 'octicon'' '"check''
'-circle''
'-fill"'' 'aria''
'-label="Required"'' '%}'' '|'' 'Specify'' 'the'' 'SARIF'' 'file'' 'to'' 'load.{%'' 'ifversion'' 'ghes'' 'or'' 'ghae'' '%}'' '|'' '''
'-github''
'-url'' '|'' '{%'' 'octicon'' '"check''
'-circle''
'-fill"'' 'aria''
'-label="Required"'' '%}'' '|'' 'Specify'' 'the'' 'URL'' 'for'' '{%'' 'data'' 'variables.product.product_name'' '%}.{%'' 'endif'' '%}'' '|'' '''
'-github''
'-auth''
'-stdin'' '|'' '|'' 'Optional.'' 'Use'' 'to'' 'pass'' 'the'' 'CLI'' 'the'' '{%'' 'data'' 'variables.product.prodname_github_app'' '%}'' 'or'' 'personal'' 'access'' 'token'' 'created'' 'for'' 'authentication'' 'with'' '{%'' 'data'' 'variables.product.company_short'' '%}'s'' 'REST'' 'API'' 'via'' 'standard'' 'input.'' 'This'' 'is'' 'not'' 'needed'' 'if'' 'the'' 'command'' 'has'' 'access'' 'to'' 'a'' 'GITHUB_TOKEN'' 'environment'' 'variable'' 'set'' 'with'' 'this'' 'token.'' '|'' '''
'-github''
'-auth''
'-stdin'' '|'' '|'' 'Optional.'' 'Use'' 'to'' 'pass'' 'the'' 'CLI'' 'the'' '{%'' 'data'' 'variables.product.prodname_github_app'' '%}'' 'or'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'created'' 'for'' 'authentication'' 'with'' '{%'' 'data'' 'variables.product.company_short'' '%}'s'' 'REST'' 'API'' 'via'' 'standard'' 'input.'' 'This'' 'is'' 'not'' 'needed'' 'if'' 'the'' 'command'' 'has'' 'access'' 'to'' 'a'' 'GITHUB_TOKEN'' 'environment'' 'variable'' 'set'' 'with'' 'this'' 'token.
For'' 'more'' 'information,'' 'see'' 'github'' 'upload''
'-results'' 'in'' 'the'' 'documentation'' 'for'' 'the'' '{%'' 'data'' 'variables.product.prodname_codeql_cli'' '%}.'@'@'' '''
'-231,12'' '+231,12'' ''@'@'' 'There'' 'is'' 'no'' 'output'' 'from'' 'this'' 'command'' 'unless'' 'the'' 'upload'' 'was'' 'unsuccessful.'' 'The'' 'comThe'' '{%'' 'data'' 'variables.product.prodname_codeql_cli'' '%}'' 'bundle'' 'includes'' 'queries'' 'that'' 'are'' 'maintained'' 'by'' '{%'' 'data'' 'variables.product.company_short'' '%}'' 'experts,'' 'security'' 'researchers,'' 'and'' 'community'' 'contributors.'' 'If'' 'you'' 'want'' 'to'' 'run'' 'queries'' 'developed'' 'by'' 'other'' 'organizations,'' '{%'' 'data'' 'variables.product.prodname_codeql'' '%}'' 'query'' 'packs'' 'provide'' 'an'' 'efficient'' 'and'' 'reliable'' 'way'' 'to'' 'download'' 'and'' 'run'' 'queries.'' 'For'' 'more'' 'information,'' 'see'' '"About'' 'code'' 'scanning'' 'with'' 'CodeQL."Before'' 'you'' 'can'' 'use'' 'a'' '{%'' 'data'' 'variables.product.prodname_codeql'' '%}'' 'pack'' 'to'' 'analyze'' 'a'' 'database,'' 'you'' 'must'' 'download'' 'any'' 'packages'' 'you'' 'require'' 'from'' 'the'' '{%'' 'data'' 'variables.product.company_short'' '%}'' '{%'' 'data'' 'variables.product.prodname_container_registry'' '%}.'' 'This'' 'can'' 'be'' 'done'' 'either'' 'by'' 'using'' 'the'' '''
'-download'' 'flag'' 'as'' 'part'' 'of'' 'the'' 'codeql'' 'database'' 'analyze'' 'command.'' 'If'' 'a'' 'package'' 'is'' 'not'' 'publicly'' 'available,'' 'you'' 'will'' 'need'' 'to'' 'use'' 'a'' '{%'' 'data'' 'variables.product.prodname_github_app'' '%}'' 'or'' 'personal'' 'access'' 'token'' 'to'' 'authenticate.'' 'For'' 'more'' 'information'' 'and'' 'an'' 'example,'' 'see'' '"Uploading'' 'results'' 'to'' '{%'' 'data'' 'variables.product.product_name'' '%}"'' 'above.'' 'Before'' 'you'' 'can'' 'use'' 'a'' '{%'' 'data'' 'variables.product.prodname_codeql'' '%}'' 'pack'' 'to'' 'analyze'' 'a'' 'database,'' 'you'' 'must'' 'download'' 'any'' 'packages'' 'you'' 'require'' 'from'' 'the'' '{%'' 'data'' 'variables.product.company_short'' '%}'' '{%'' 'data'' 'variables.product.prodname_container_registry'' '%}.'' 'This'' 'can'' 'be'' 'done'' 'either'' 'by'' 'using'' 'the'' '''
'-download'' 'flag'' 'as'' 'part'' 'of'' 'the'' 'codeql'' 'database'' 'analyze'' 'command.'' 'If'' 'a'' 'package'' 'is'' 'not'' 'publicly'' 'available,'' 'you'' 'will'' 'need'' 'to'' 'use'' 'a'' '{%'' 'data'' 'variables.product.prodname_github_app'' '%}'' 'or'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'to'' 'authenticate.'' 'For'' 'more'' 'information'' 'and'' 'an'' 'example,'' 'see'' '"Uploading'' 'results'' 'to'' '{%'' 'data'' 'variables.product.product_name'' '%}"'' 'above.Option	Required	Usage
<scope/name'@version:path>	{%'' 'octicon'' '"check''
'-circle''
'-fill"'' 'aria''
'-label="Required"'' '%}	Specify'' 'the'' 'scope'' 'and'' 'name'' 'of'' 'one'' 'or'' 'more'' 'CodeQL'' 'query'' 'packs'' 'to'' 'download'' 'using'' 'a'' 'comma''
'-separated'' 'list.'' 'Optionally,'' 'include'' 'the'' 'version'' 'to'' 'download'' 'and'' 'unzip.'' 'By'' 'default'' 'the'' 'latest'' 'version'' 'of'' 'this'' 'pack'' 'is'' 'downloaded.'' 'Optionally,'' 'include'' 'a'' 'path'' 'to'' 'a'' 'query,'' 'directory,'' 'or'' 'query'' 'suite'' 'to'' 'run.'' 'If'' 'no'' 'path'' 'is'' 'included,'' 'then'' 'run'' 'the'' 'default'' 'queries'' 'of'' 'this'' 'pack.
''
'-github''
'-auth''
'-stdin		Optional.'' 'Pass'' 'the'' '{%'' 'data'' 'variables.product.prodname_github_app'' '%}'' 'or'' 'personal'' 'access'' 'token'' 'created'' 'for'' 'authentication'' 'with'' '{%'' 'data'' 'variables.product.company_short'' '%}'s'' 'REST'' 'API'' 'to'' 'the'' 'CLI'' 'via'' 'standard'' 'input.'' 'This'' 'is'' 'not'' 'needed'' 'if'' 'the'' 'command'' 'has'' 'access'' 'to'' 'a'' 'GITHUB_TOKEN'' 'environment'' 'variable'' 'set'' 'with'' 'this'' 'token.
''
'-github''
'-auth''
'-stdin		Optional.'' 'Pass'' 'the'' '{%'' 'data'' 'variables.product.prodname_github_app'' '%}'' 'or'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'created'' 'for'' 'authentication'' 'with'' '{%'' 'data'' 'variables.product.company_short'' '%}'s'' 'REST'' 'API'' 'to'' 'the'' 'CLI'' 'via'' 'standard'' 'input.'' 'This'' 'is'' 'not'' 'needed'' 'if'' 'the'' 'command'' 'has'' 'access'' 'to'' 'a'' 'GITHUB_TOKEN'' 'environment'' 'variable'' 'set'' 'with'' 'this'' 'token.
Basic'' 'example
6
...ing''
'-with''
'-your''
'-existing''
'-ci''
'-system/configuring''
'-codeql''
'-runner''
'-in''
'-your''
'-ci''
'-system.md'' ''@'@'' '''
'-147,7'' '+147,7'' ''@'@'' 'Initializes'' 'the'' '{%'' 'data'' 'variables.product.prodname_codeql_runner'' '%}'' 'and'' 'creates'' '|'' ''' '|:''
'-:|'' ''' '|'' '|'' '''
'-repository'' '|'' '???'' '|'' 'Name'' 'of'' 'the'' 'repository'' 'to'' 'initialize.'' '|'' '|'' '''
'-github''
'-url'' '|'' '???'' '|'' 'URL'' 'of'' 'the'' '{%'' 'data'' 'variables.product.prodname_dotcom'' '%}'' 'instance'' 'where'' 'your'' 'repository'' 'is'' 'hosted.'' '|'' '|'' '''
'-github''
'-auth''
'-stdin'' '|'' '???'' '|'' 'Read'' 'the'' '{%'' 'data'' 'variables.product.prodname_github_apps'' '%}'' 'token'' 'or'' 'personal'' 'access'' 'token'' 'from'' 'standard'' 'input.'' '|'' '|'' '''
'-github''
'-auth''
'-stdin'' '|'' '???'' '|'' 'Read'' 'the'' '{%'' 'data'' 'variables.product.prodname_github_apps'' '%}'' 'token'' 'or'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'from'' 'standard'' 'input.'' '|'' '|'' '''
'-languages'' '|'' '|'' 'Comma''
'-separated'' 'list'' 'of'' 'languages'' 'to'' 'analyze.'' 'By'' 'default,'' 'the'' '{%'' 'data'' 'variables.product.prodname_codeql_runner'' '%}'' 'detects'' 'and'' 'analyzes'' 'all'' 'supported'' 'languages'' 'in'' 'the'' 'repository.'' '|'' '|'' '''
'-queries'' '|'' '|'' 'Comma''
'-separated'' 'list'' 'of'' 'additional'' 'queries'' 'to'' 'run,'' 'in'' 'addition'' 'to'' 'the'' 'default'' 'suite'' 'of'' 'security'' 'queries.'' 'This'' 'overrides'' 'the'' 'queries'' 'setting'' 'in'' 'the'' 'custom'' 'configuration'' 'file.'' '|'' '|'' '''
'-config''
'-file'' '|'' '|'' 'Path'' 'to'' 'custom'' 'configuration'' 'file.'' '|'' ''@'@'' '''
'-181,7'' '+181,7'' ''@'@'' 'Analyzes'' 'the'' 'code'' 'in'' 'the'' '{%'' 'data'' 'variables.product.prodname_codeql'' '%}'' 'databases'' '|'' '''
'-commit'' '|'' '???'' '|'' 'SHA'' 'of'' 'the'' 'commit'' 'to'' 'analyze.'' 'In'' 'Git'' 'and'' 'in'' 'Azure'' 'DevOps,'' 'this'' 'corresponds'' 'to'' 'the'' 'value'' 'of'' 'git'' 'rev''
'-parse'' 'HEAD.'' 'In'' 'Jenkins,'' 'this'' 'corresponds'' 'to'' '$GIT_COMMIT.'' '|'' '|'' '''
'-ref'' '|'' '???'' '|'' 'Name'' 'of'' 'the'' 'reference'' 'to'' 'analyze,'' 'for'' 'example'' 'refs/heads/main'' 'or'' 'refs/pull/42/merge.'' 'In'' 'Git'' 'or'' 'in'' 'Jenkins,'' 'this'' 'corresponds'' 'to'' 'the'' 'value'' 'of'' 'git'' 'symbolic''
'-ref'' 'HEAD.'' 'In'' 'Azure'' 'DevOps,'' 'this'' 'corresponds'' 'to'' '$(Build.SourceBranch).'' '|'' '|'' '''
'-github''
'-url'' '|'' '???'' '|'' 'URL'' 'of'' 'the'' '{%'' 'data'' 'variables.product.prodname_dotcom'' '%}'' 'instance'' 'where'' 'your'' 'repository'' 'is'' 'hosted.'' '|'' '|'' '''
'-github''
'-auth''
'-stdin'' '|'' '???'' '|'' 'Read'' 'the'' '{%'' 'data'' 'variables.product.prodname_github_apps'' '%}'' 'token'' 'or'' 'personal'' 'access'' 'token'' 'from'' 'standard'' 'input.'' '|'' '|'' '''
'-github''
'-auth''
'-stdin'' '|'' '???'' '|'' 'Read'' 'the'' '{%'' 'data'' 'variables.product.prodname_github_apps'' '%}'' 'token'' 'or'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'from'' 'standard'' 'input.'' '|'' '|'' '''
'-checkout''
'-path'' '|'' '|'' 'The'' 'path'' 'to'' 'the'' 'checkout'' 'of'' 'your'' 'repository.'' 'The'' 'default'' 'is'' 'the'' 'current'' 'working'' 'directory.'' '|'' '|'' '''
'-no''
'-upload'' '|'' '|'' 'None.'' 'Stops'' 'the'' '{%'' 'data'' 'variables.product.prodname_codeql_runner'' '%}'' 'from'' 'uploading'' 'the'' 'results'' 'to'' '{%'' 'data'' 'variables.product.product_name'' '%}.'' '|'' '|'' '''
'-output''
'-dir'' '|'' '|'' 'Directory'' 'where'' 'the'' 'output'' 'SARIF'' 'files'' 'are'' 'stored.'' 'The'' 'default'' 'is'' 'in'' 'the'' 'directory'' 'of'' 'temporary'' 'files.'' '|'' ''@'@'' '''
'-210,7'' '+210,7'' ''@'@'' 'Uploads'' 'SARIF'' 'files'' 'to'' '{%'' 'data'' 'variables.product.product_name'' '%}.'' '|'' '''
'-commit'' '|'' '???'' '|'' 'SHA'' 'of'' 'the'' 'commit'' 'that'' 'was'' 'analyzed.'' 'In'' 'Git'' 'and'' 'in'' 'Azure'' 'DevOps,'' 'this'' 'corresponds'' 'to'' 'the'' 'value'' 'of'' 'git'' 'rev''
'-parse'' 'HEAD.'' 'In'' 'Jenkins,'' 'this'' 'corresponds'' 'to'' '$GIT_COMMIT.'' '|'' '|'' '''
'-ref'' '|'' '???'' '|'' 'Name'' 'of'' 'the'' 'reference'' 'that'' 'was'' 'analyzed,'' 'for'' 'example'' 'refs/heads/main'' 'or'' 'refs/pull/42/merge.'' 'In'' 'Git'' 'or'' 'in'' 'Jenkins,'' 'this'' 'corresponds'' 'to'' 'the'' 'value'' 'of'' 'git'' 'symbolic''
'-ref'' 'HEAD.'' 'In'' 'Azure'' 'DevOps,'' 'this'' 'corresponds'' 'to'' '$(Build.SourceBranch).'' '|'' '|'' '''
'-github''
'-url'' '|'' '???'' '|'' 'URL'' 'of'' 'the'' '{%'' 'data'' 'variables.product.prodname_dotcom'' '%}'' 'instance'' 'where'' 'your'' 'repository'' 'is'' 'hosted.'' '|'' '|'' '''
'-github''
'-auth''
'-stdin'' '|'' '???'' '|'' 'Read'' 'the'' '{%'' 'data'' 'variables.product.prodname_github_apps'' '%}'' 'token'' 'or'' 'personal'' 'access'' 'token'' 'from'' 'standard'' 'input.'' '|'' '|'' '''
'-github''
'-auth''
'-stdin'' '|'' '???'' '|'' 'Read'' 'the'' '{%'' 'data'' 'variables.product.prodname_github_apps'' '%}'' 'token'' 'or'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'from'' 'standard'' 'input.'' '|'' '|'' '''
'-checkout''
'-path'' '|'' '|'' 'The'' 'path'' 'to'' 'the'' 'checkout'' 'of'' 'your'' 'repository.'' 'The'' 'default'' 'is'' 'the'' 'current'' 'working'' 'directory.'' '|'' '|'' '''
'-debug'' '|'' '|'' 'None.'' 'Prints'' 'more'' 'verbose'' 'output.'' '|'' '|'' '''
'-h,'' '''
'-help'' '|'' '|'' 'None.'' 'Displays'' 'help'' 'for'' 'the'' 'command.'' '|'' '2
...canning''
'-with''
'-your''
'-existing''
'-ci''
'-system/installing''
'-codeql''
'-cli''
'-in''
'-your''
'-ci''
'-system.md'' ''@'@'' '''
'-112,7'' '+112,7'' ''@'@'' 'You'' 'should'' 'check'' 'that'' 'the'' 'output'' 'contains'' 'the'' 'expected'' 'languages'' 'and'' 'also'' 'that'' 'tGenerating'' 'a'' 'token'' 'for'' 'authentication'' 'with'' '{%'' 'data'' 'variables.product.product_name'' '%}
Each'' 'CI'' 'server'' 'needs'' 'a'' '{%'' 'data'' 'variables.product.prodname_github_app'' '%}'' 'or'' 'personal'' 'access'' 'token'' 'for'' 'the'' '{%'' 'data'' 'variables.product.prodname_codeql_cli'' '%}'' 'to'' 'use'' 'to'' 'upload'' 'results'' 'to'' '{%'' 'data'' 'variables.product.product_name'' '%}.'' 'You'' 'must'' 'use'' 'an'' 'access'' 'token'' 'or'' 'a'' '{%'' 'data'' 'variables.product.prodname_github_app'' '%}'' 'with'' 'the'' 'security_events'' 'write'' 'permission.'' 'If'' 'CI'' 'servers'' 'already'' 'use'' 'a'' 'token'' 'with'' 'this'' 'scope'' 'to'' 'checkout'' 'repositories'' 'from'' '{%'' 'data'' 'variables.product.product_name'' '%},'' 'you'' 'could'' 'potentially'' 'allow'' 'the'' '{%'' 'data'' 'variables.product.prodname_codeql_cli'' '%}'' 'to'' 'use'' 'the'' 'same'' 'token.'' 'Otherwise,'' 'you'' 'should'' 'create'' 'a'' 'new'' 'token'' 'with'' 'the'' 'security_events'' 'write'' 'permission'' 'and'' 'add'' 'this'' 'to'' 'the'' 'CI'' 'system's'' 'secret'' 'store.'' 'For'' 'information,'' 'see'' '"Building'' '{%'' 'data'' 'variables.product.prodname_github_apps'' '%}"'' 'and'' '"Creating'' 'a'' 'personal'' 'access'' 'token."'' 'Each'' 'CI'' 'server'' 'needs'' 'a'' '{%'' 'data'' 'variables.product.prodname_github_app'' '%}'' 'or'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'for'' 'the'' '{%'' 'data'' 'variables.product.prodname_codeql_cli'' '%}'' 'to'' 'use'' 'to'' 'upload'' 'results'' 'to'' '{%'' 'data'' 'variables.product.product_name'' '%}.'' 'You'' 'must'' 'use'' 'an'' 'access'' 'token'' 'or'' 'a'' '{%'' 'data'' 'variables.product.prodname_github_app'' '%}'' 'with'' 'the'' 'security_events'' 'write'' 'permission.'' 'If'' 'CI'' 'servers'' 'already'' 'use'' 'a'' 'token'' 'with'' 'this'' 'scope'' 'to'' 'checkout'' 'repositories'' 'from'' '{%'' 'data'' 'variables.product.product_name'' '%},'' 'you'' 'could'' 'potentially'' 'allow'' 'the'' '{%'' 'data'' 'variables.product.prodname_codeql_cli'' '%}'' 'to'' 'use'' 'the'' 'same'' 'token.'' 'Otherwise,'' 'you'' 'should'' 'create'' 'a'' 'new'' 'token'' 'with'' 'the'' 'security_events'' 'write'' 'permission'' 'and'' 'add'' 'this'' 'to'' 'the'' 'CI'' 'system's'' 'secret'' 'store.'' 'For'' 'information,'' 'see'' '"Building'' '{%'' 'data'' 'variables.product.prodname_github_apps'' '%}"'' 'and'' '"Creating'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}."Next'' 'steps
4
...canning''
'-with''
'-your''
'-existing''
'-ci''
'-system/running''
'-codeql''
'-runner''
'-in''
'-your''
'-ci''
'-system.md'' ''@'@'' '''
'-88,7'' '+88,7'' ''@'@'' 'chmod'' '+x'' 'codeql''
'-runner''
'-linuxIn'' 'addition'' 'to'' 'this,'' 'each'' 'CI'' 'server'' 'also'' 'needs:A'' '{%'' 'data'' 'variables.product.prodname_github_app'' '%}'' 'or'' 'personal'' 'access'' 'token'' 'for'' 'the'' '{%'' 'data'' 'variables.product.prodname_codeql_runner'' '%}'' 'to'' 'use.'' 'You'' 'must'' 'use'' 'an'' 'access'' 'token'' 'with'' 'the'' 'repo'' 'scope,'' 'or'' 'a'' '{%'' 'data'' 'variables.product.prodname_github_app'' '%}'' 'with'' 'the'' 'security_events'' 'write'' 'permission,'' 'and'' 'metadata'' 'and'' 'contents'' 'read'' 'permissions.'' 'For'' 'information,'' 'see'' '"Building'' '{%'' 'data'' 'variables.product.prodname_github_apps'' '%}"'' 'and'' '"Creating'' 'a'' 'personal'' 'access'' 'token."
A'' '{%'' 'data'' 'variables.product.prodname_github_app'' '%}'' 'or'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'for'' 'the'' '{%'' 'data'' 'variables.product.prodname_codeql_runner'' '%}'' 'to'' 'use.'' 'You'' 'must'' 'use'' 'an'' 'access'' 'token'' 'with'' 'the'' 'repo'' 'scope,'' 'or'' 'a'' '{%'' 'data'' 'variables.product.prodname_github_app'' '%}'' 'with'' 'the'' 'security_events'' 'write'' 'permission,'' 'and'' 'metadata'' 'and'' 'contents'' 'read'' 'permissions.'' 'For'' 'information,'' 'see'' '"Building'' '{%'' 'data'' 'variables.product.prodname_github_apps'' '%}"'' 'and'' '"Creating'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}."
Access'' 'to'' 'the'' '{%'' 'data'' 'variables.product.prodname_codeql'' '%}'' 'bundle'' 'associated'' 'with'' 'this'' 'release'' 'of'' 'the'' '{%'' 'data'' 'variables.product.prodname_codeql_runner'' '%}.'' 'This'' 'package'' 'contains'' 'queries'' 'and'' 'libraries'' 'needed'' 'for'' '{%'' 'data'' 'variables.product.prodname_codeql'' '%}'' 'analysis,'' 'plus'' 'the'' '{%'' 'data'' 'variables.product.prodname_codeql'' '%}'' 'CLI,'' 'which'' 'is'' 'used'' 'internally'' 'by'' 'the'' 'runner.'' 'For'' 'information,'' 'see'' '"{%'' 'data'' 'variables.product.prodname_codeql'' '%}'' 'CLI."
The'' 'options'' 'for'' 'providing'' 'access'' 'to'' 'the'' '{%'' 'data'' 'variables.product.prodname_codeql'' '%}'' 'bundle'' 'are:'' ''@'@'' '''
'-103,7'' '+103,7'' ''@'@'' 'You'' 'should'' 'call'' 'the'' '{%'' 'data'' 'variables.product.prodname_codeql_runner'' '%}'' 'from'' 'theinit'' 'required'' 'to'' 'initialize'' 'the'' 'runner'' 'and'' 'create'' 'a'' '{%'' 'data'' 'variables.product.prodname_codeql'' '%}'' 'database'' 'for'' 'each'' 'language'' 'to'' 'be'' 'analyzed.'' 'These'' 'databases'' 'are'' 'populated'' 'and'' 'analyzed'' 'by'' 'subsequent'' 'commands.
analyze'' 'required'' 'to'' 'populate'' 'the'' '{%'' 'data'' 'variables.product.prodname_codeql'' '%}'' 'databases,'' 'analyze'' 'them,'' 'and'' 'upload'' 'results'' 'to'' '{%'' 'data'' 'variables.product.product_name'' '%}.
For'' 'both'' 'commands,'' 'you'' 'must'' 'specify'' 'the'' 'URL'' 'of'' '{%'' 'data'' 'variables.product.product_name'' '%},'' 'the'' 'repository'' 'OWNER/NAME,'' 'and'' 'the'' '{%'' 'data'' 'variables.product.prodname_github_apps'' '%}'' 'or'' 'personal'' 'access'' 'token'' 'to'' 'use'' 'for'' 'authentication.'' 'You'' 'also'' 'need'' 'to'' 'specify'' 'the'' 'location'' 'of'' 'the'' 'CodeQL'' 'bundle,'' 'unless'' 'the'' 'CI'' 'server'' 'has'' 'access'' 'to'' 'download'' 'it'' 'directly'' 'from'' 'the'' 'github/codeql''
'-action'' 'repository.'' 'For'' 'both'' 'commands,'' 'you'' 'must'' 'specify'' 'the'' 'URL'' 'of'' '{%'' 'data'' 'variables.product.product_name'' '%},'' 'the'' 'repository'' 'OWNER/NAME,'' 'and'' 'the'' '{%'' 'data'' 'variables.product.prodname_github_apps'' '%}'' 'or'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'to'' 'use'' 'for'' 'authentication.'' 'You'' 'also'' 'need'' 'to'' 'specify'' 'the'' 'location'' 'of'' 'the'' 'CodeQL'' 'bundle,'' 'unless'' 'the'' 'CI'' 'server'' 'has'' 'access'' 'to'' 'download'' 'it'' 'directly'' 'from'' 'the'' 'github/codeql''
'-action'' 'repository.You'' 'can'' 'configure'' 'where'' 'the'' '{%'' 'data'' 'variables.product.prodname_codeql_runner'' '%}'' 'stores'' 'the'' 'CodeQL'' 'bundle'' 'for'' 'future'' 'analysis'' 'on'' 'a'' 'server'' 'using'' 'the'' '''
'-tools''
'-dir'' 'flag'' 'and'' 'where'' 'it'' 'stores'' 'temporary'' 'files'' 'during'' 'analysis'' 'using'' '''
'-temp''
'-dir.2
content/code''
'-security/secret''
'-scanning/managing''
'-alerts''
'-from''
'-secret''
'-scanning.md'' ''@'@'' '''
'-68,7'' '+68,7'' ''@'@'' 'shortTitle:'' 'Manage'' 'secret'' 'alertsOnce'' 'a'' 'secret'' 'has'' 'been'' 'committed'' 'to'' 'a'' 'repository,'' 'you'' 'should'' 'consider'' 'the'' 'secret'' 'compromised.'' '{%'' 'data'' 'variables.product.prodname_dotcom'' '%}'' 'recommends'' 'the'' 'following'' 'actions'' 'for'' 'compromised'' 'secrets:For'' 'a'' 'compromised'' '{%'' 'data'' 'variables.product.prodname_dotcom'' '%}'' 'personal'' 'access'' 'token,'' 'delete'' 'the'' 'compromised'' 'token,'' 'create'' 'a'' 'new'' 'token,'' 'and'' 'update'' 'any'' 'services'' 'that'' 'use'' 'the'' 'old'' 'token.'' 'For'' 'more'' 'information,'' 'see'' '"Creating'' 'a'' 'personal'' 'access'' 'token'' 'for'' 'the'' 'command'' 'line."
For'' 'a'' 'compromised'' '{%'' 'data'' 'variables.product.prodname_dotcom'' '%}'' '{%'' 'data'' 'variables.product.pat_generic'' '%},'' 'delete'' 'the'' 'compromised'' 'token,'' 'create'' 'a'' 'new'' 'token,'' 'and'' 'update'' 'any'' 'services'' 'that'' 'use'' 'the'' 'old'' 'token.'' 'For'' 'more'' 'information,'' 'see'' '"Creating'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'for'' 'the'' 'command'' 'line."
For'' 'all'' 'other'' 'secrets,'' 'first'' 'verify'' 'that'' 'the'' 'secret'' 'committed'' 'to'' '{%'' 'data'' 'variables.product.product_name'' '%}'' 'is'' 'valid.'' 'If'' 'so,'' 'create'' 'a'' 'new'' 'secret,'' 'update'' 'any'' 'services'' 'that'' 'use'' 'the'' 'old'' 'secret,'' 'and'' 'then'' 'delete'' 'the'' 'old'' 'secret.
{%'' 'ifversion'' 'ghec'' '%}'' '2
content/code''
'-security/security''
'-overview/about''
'-the''
'-security''
'-overview.md'' ''@'@'' '''
'-43,7'' '+43,7'' ''@'@'' 'In'' 'the'' 'security'' 'overview,'' 'you'' 'can'' 'view,'' 'sort,'' 'and'' 'filter'' 'alerts'' 'to'' 'understand'' 'th{%'' 'ifversion'' 'security''
'-overview''
'-views'' '%}In'' 'the'' 'security'' 'overview,'' 'there'' 'are'' 'dedicated'' 'views'' 'for'' 'each'' 'type'' 'of'' 'security'' 'alert,'' 'such'' 'as'' 'Dependabot,'' 'code'' 'scanning,'' 'and'' 'secret'' 'scanning'' 'alerts.'' 'You'' 'can'' 'use'' 'these'' 'views'' 'to'' 'limit'' 'your'' 'analysis'' 'to'' 'a'' 'specific'' 'set'' 'of'' 'alerts,'' 'and'' 'narrow'' 'the'' 'results'' 'further'' 'with'' 'a'' 'range'' 'of'' 'filters'' 'specific'' 'to'' 'each'' 'view.'' 'For'' 'example,'' 'in'' 'the'' 'secret'' 'scanning'' 'alert'' 'view,'' 'you'' 'can'' 'use'' 'the'' 'Secret'' 'type'' 'filter'' 'to'' 'view'' 'only'' 'secret'' 'scanning'' 'alerts'' 'for'' 'a'' 'specific'' 'secret,'' 'like'' 'a'' 'GitHub'' 'Personal'' 'Access'' 'Token.'' 'At'' 'the'' 'repository'' 'level,'' 'you'' 'can'' 'use'' 'the'' 'security'' 'overview'' 'to'' 'assess'' 'the'' 'specific'' 'repository's'' 'current'' 'security'' 'status,'' 'and'' 'configure'' 'any'' 'additional'' 'security'' 'features'' 'not'' 'yet'' 'in'' 'use'' 'on'' 'the'' 'repository.'' 'In'' 'the'' 'security'' 'overview,'' 'there'' 'are'' 'dedicated'' 'views'' 'for'' 'each'' 'type'' 'of'' 'security'' 'alert,'' 'such'' 'as'' 'Dependabot,'' 'code'' 'scanning,'' 'and'' 'secret'' 'scanning'' 'alerts.'' 'You'' 'can'' 'use'' 'these'' 'views'' 'to'' 'limit'' 'your'' 'analysis'' 'to'' 'a'' 'specific'' 'set'' 'of'' 'alerts,'' 'and'' 'narrow'' 'the'' 'results'' 'further'' 'with'' 'a'' 'range'' 'of'' 'filters'' 'specific'' 'to'' 'each'' 'view.'' 'For'' 'example,'' 'in'' 'the'' 'secret'' 'scanning'' 'alert'' 'view,'' 'you'' 'can'' 'use'' 'the'' 'Secret'' 'type'' 'filter'' 'to'' 'view'' 'only'' 'secret'' 'scanning'' 'alerts'' 'for'' 'a'' 'specific'' 'secret,'' 'like'' 'a'' 'GitHub'' '{%'' 'data'' 'variables.product.pat_generic'' '%}.'' 'At'' 'the'' 'repository'' 'level,'' 'you'' 'can'' 'use'' 'the'' 'security'' 'overview'' 'to'' 'assess'' 'the'' 'specific'' 'repository's'' 'current'' 'security'' 'status,'' 'and'' 'configure'' 'any'' 'additional'' 'security'' 'features'' 'not'' 'yet'' 'in'' 'use'' 'on'' 'the'' 'repository.{%'' 'endif'' '%}8
...espaces''
'-reference/allowing''
'-your''
'-codespace''
'-to''
'-access''
'-a''
'-private''
'-image''
'-registry.md'' ''@'@'' '''
'-30,7'' '+30,7'' ''@'@'' 'If'' 'you'' 'publish'' 'a'' 'container'' 'image'' 'to'' '{%'' 'data'' 'variables.packages.prodname_ghcr_or_By'' 'default,'' 'when'' 'you'' 'publish'' 'a'' 'container'' 'image'' 'to'' '{%'' 'data'' 'variables.packages.prodname_ghcr_or_npm_registry'' '%},'' 'the'' 'image'' 'inherits'' 'the'' 'access'' 'setting'' 'of'' 'the'' 'repository'' 'from'' 'which'' 'the'' 'image'' 'was'' 'published.'' 'For'' 'example,'' 'if'' 'the'' 'repository'' 'is'' 'public,'' 'the'' 'image'' 'is'' 'also'' 'public.'' 'If'' 'the'' 'repository'' 'is'' 'private,'' 'the'' 'image'' 'is'' 'also'' 'private,'' 'but'' 'is'' 'accessible'' 'from'' 'the'' 'repository.This'' 'behavior'' 'is'' 'controlled'' 'by'' 'the'' 'Inherit'' 'access'' 'from'' 'repo'' 'option.'' 'Inherit'' 'access'' 'from'' 'repo'' 'is'' 'selected'' 'by'' 'default'' 'when'' 'publishing'' 'via'' '{%'' 'data'' 'variables.product.prodname_actions'' '%},'' 'but'' 'not'' 'when'' 'publishing'' 'directly'' 'to'' '{%'' 'data'' 'variables.packages.prodname_ghcr_or_npm_registry'' '%}'' 'using'' 'a'' 'Personal'' 'Access'' 'Token'' '(PAT).'' 'This'' 'behavior'' 'is'' 'controlled'' 'by'' 'the'' 'Inherit'' 'access'' 'from'' 'repo'' 'option.'' 'Inherit'' 'access'' 'from'' 'repo'' 'is'' 'selected'' 'by'' 'default'' 'when'' 'publishing'' 'via'' '{%'' 'data'' 'variables.product.prodname_actions'' '%},'' 'but'' 'not'' 'when'' 'publishing'' 'directly'' 'to'' '{%'' 'data'' 'variables.packages.prodname_ghcr_or_npm_registry'' '%}'' 'using'' 'a'' '%'' 'data'' 'variables.product.pat_generic'' '%}.If'' 'the'' 'Inherit'' 'access'' 'from'' 'repo'' 'option'' 'was'' 'not'' 'selected'' 'when'' 'the'' 'image'' 'was'' 'published,'' 'you'' 'can'' 'manually'' 'add'' 'the'' 'repository'' 'to'' 'the'' 'published'' 'container'' 'image's'' 'access'' 'controls.'' 'For'' 'more'' 'information,'' 'see'' '"Configuring'' 'a'' 'package's'' 'access'' 'control'' 'and'' 'visibility."'@'@'' '''
'-46,13'' '+46,13'' ''@'@'' 'If'' 'you'' 'want'' 'to'' 'allow'' 'a'' 'subset'' 'of'' 'an'' 'organization's'' 'repositories'' 'to'' 'access'' 'a'' 'contPublishing'' 'a'' 'container'' 'image'' 'from'' 'a'' 'codespace
Seamless'' 'access'' 'from'' 'a'' 'codespace'' 'to'' '{%'' 'data'' 'variables.packages.prodname_ghcr_or_npm_registry'' '%}'' 'is'' 'limited'' 'to'' 'pulling'' 'container'' 'images.'' 'If'' 'you'' 'want'' 'to'' 'publish'' 'a'' 'container'' 'image'' 'from'' 'inside'' 'a'' 'codespace,'' 'you'' 'must'' 'use'' 'a'' 'personal'' 'access'' 'token'' '(PAT)'' 'with'' 'the'' 'write:packages'' 'scope.'' 'Seamless'' 'access'' 'from'' 'a'' 'codespace'' 'to'' '{%'' 'data'' 'variables.packages.prodname_ghcr_or_npm_registry'' '%}'' 'is'' 'limited'' 'to'' 'pulling'' 'container'' 'images.'' 'If'' 'you'' 'want'' 'to'' 'publish'' 'a'' 'container'' 'image'' 'from'' 'inside'' 'a'' 'codespace,'' 'you'' 'must'' 'use'' 'a'' '{%'' 'data'' 'variables.product.pat_v1'' '%}'' 'with'' 'the'' 'write:packages'' 'scope.We'' 'recommend'' 'publishing'' 'images'' 'via'' '{%'' 'data'' 'variables.product.prodname_actions'' '%}.'' 'For'' 'more'' 'information,'' 'see'' '"Publishing'' 'Docker'' 'images"'' 'and'' '"Publishing'' 'Node.js'' 'packages."Accessing'' 'images'' 'stored'' 'in'' 'other'' 'container'' 'registries
If'' 'you'' 'are'' 'accessing'' 'a'' 'container'' 'image'' 'from'' 'a'' 'registry'' 'that'' 'isn't'' '{%'' 'data'' 'variables.packages.prodname_ghcr_or_npm_registry'' '%},'' '{%'' 'data'' 'variables.product.prodname_github_codespaces'' '%}'' 'checks'' 'for'' 'the'' 'presence'' 'of'' 'three'' 'secrets,'' 'which'' 'define'' 'the'' 'server'' 'name,'' 'username,'' 'and'' 'personal'' 'access'' 'token'' '(PAT)'' 'for'' 'a'' 'container'' 'registry.'' 'If'' 'these'' 'secrets'' 'are'' 'found,'' '{%'' 'data'' 'variables.product.prodname_github_codespaces'' '%}'' 'will'' 'make'' 'the'' 'registry'' 'available'' 'inside'' 'your'' 'codespace.'' 'If'' 'you'' 'are'' 'accessing'' 'a'' 'container'' 'image'' 'from'' 'a'' 'registry'' 'that'' 'isn't'' '{%'' 'data'' 'variables.packages.prodname_ghcr_or_npm_registry'' '%},'' '{%'' 'data'' 'variables.product.prodname_github_codespaces'' '%}'' 'checks'' 'for'' 'the'' 'presence'' 'of'' 'three'' 'secrets,'' 'which'' 'define'' 'the'' 'server'' 'name,'' 'username,'' 'and'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'for'' 'a'' 'container'' 'registry.'' 'If'' 'these'' 'secrets'' 'are'' 'found,'' '{%'' 'data'' 'variables.product.prodname_github_codespaces'' '%}'' 'will'' 'make'' 'the'' 'registry'' 'available'' 'inside'' 'your'' 'codespace.<*>_CONTAINER_REGISTRY_SERVER
<*>_CONTAINER_REGISTRY_USER'' ''@'@'' '''
'-71,7'' '+71,7'' ''@'@'' 'For'' 'a'' 'private'' 'image'' 'registry'' 'in'' 'Azure,'' 'you'' 'could'' 'create'' 'the'' 'following'' 'secrets:
ACR_CONTAINER_REGISTRY_SERVER'' '='' 'mycompany.azurecr.io
ACR_CONTAINER_REGISTRY_USER'' '='' 'acr''
'-user''
'-here
ACR_CONTAINER_REGISTRY_PASSWORD'' '='' '<PAT>
ACR_CONTAINER_REGISTRY_PASSWORD'' '='' '<PERSONAL_ACCESS_TOKEN>
For'' 'information'' 'on'' 'common'' 'image'' 'registries,'' 'see'' '"Common'' 'image'' 'registry'' 'servers."'' 'Note'' 'that'' 'accessing'' 'AWS'' 'Elastic'' 'Container'' 'Registry'' '(ECR)'' 'is'' 'different.'' '2
...aces/managing''
'-your''
'-codespaces/managing''
'-encrypted''
'-secrets''
'-for''
'-your''
'-codespaces.md'' ''@'@'' '''
'-24,7'' '+24,7'' ''@'@'' 'shortTitle:'' 'Encrypted'' 'secretsYou'' 'can'' 'add'' 'encrypted'' 'secrets'' 'to'' 'your'' 'personal'' 'account'' 'that'' 'you'' 'want'' 'to'' 'use'' 'in'' 'your'' 'codespaces.'' 'For'' 'example,'' 'you'' 'may'' 'want'' 'to'' 'store'' 'and'' 'access'' 'the'' 'following'' 'sensitive'' 'information'' 'as'' 'encrypted'' 'secrets.Personal'' 'access'' 'tokens'' 'to'' 'cloud'' 'services
{%'' 'data'' 'variables.product.pat_generic'' '%}s'' 'to'' 'cloud'' 'services
Service'' 'principals
Subscription'' 'identifiers
Credentials'' 'for'' 'a'' 'private'' 'image'' 'registry'' '16
...prebuilding''
'-your''
'-codespaces/allowing''
'-a''
'-prebuild''
'-to''
'-access''
'-other''
'-repositories.md'' ''@'@'' '''
'-29,33'' '+29,33'' ''@'@'' 'When'' 'you'' 'create'' 'or'' 'edit'' 'a'' 'prebuild'' 'configuration'' 'for'' 'a'' 'devcontainer.json'' 'file
Allowing'' 'a'' 'prebuild'' 'write'' 'access'' 'external'' 'resources
If'' 'your'' 'project'' 'requires'' 'write'' 'access'' 'to'' 'resources,'' 'or'' 'if'' 'the'' 'external'' 'resources'' 'reside'' 'in'' 'a'' 'repository'' 'with'' 'a'' 'different'' 'owner'' 'to'' 'the'' 'repository'' 'for'' 'which'' 'you'' 'are'' 'creating'' 'a'' 'prebuild'' 'configuration,'' 'you'' 'can'' 'use'' 'a'' 'personal'' 'access'' 'token'' '(PAT)'' 'to'' 'grant'' 'this'' 'access.'' 'If'' 'your'' 'project'' 'requires'' 'write'' 'access'' 'to'' 'resources,'' 'or'' 'if'' 'the'' 'external'' 'resources'' 'reside'' 'in'' 'a'' 'repository'' 'with'' 'a'' 'different'' 'owner'' 'to'' 'the'' 'repository'' 'for'' 'which'' 'you'' 'are'' 'creating'' 'a'' 'prebuild'' 'configuration,'' 'you'' 'can'' 'use'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'to'' 'grant'' 'this'' 'access.You'' 'will'' 'need'' 'to'' 'create'' 'a'' 'new'' 'personal'' 'account'' 'and'' 'then'' 'use'' 'this'' 'account'' 'to'' 'create'' 'a'' 'PAT'' 'with'' 'the'' 'appropriate'' 'scopes.'' 'You'' 'will'' 'need'' 'to'' 'create'' 'a'' 'new'' 'personal'' 'account'' 'and'' 'then'' 'use'' 'this'' 'account'' 'to'' 'create'' 'a'' '{%'' 'data'' 'variables.product.pat_v1'' '%}'' 'with'' 'the'' 'appropriate'' 'scopes.Create'' 'a'' 'new'' 'personal'' 'account'' 'on'' '{%'' 'data'' 'variables.product.prodname_dotcom'' '%}.{%'' 'warning'' '%}Warning:'' 'Although'' 'you'' 'can'' 'generate'' 'the'' 'PAT'' 'using'' 'your'' 'existing'' 'personal'' 'account,'' 'we'' 'strongly'' 'recommend'' 'creating'' 'a'' 'new'' 'account'' 'with'' 'access'' 'only'' 'to'' 'the'' 'target'' 'repositories'' 'required'' 'for'' 'your'' 'scenario.'' 'This'' 'is'' 'because'' 'the'' 'access'' 'token's'' 'repository'' 'permission'' 'grants'' 'access'' 'to'' 'all'' 'of'' 'the'' 'repositories'' 'that'' 'the'' 'account'' 'has'' 'access'' 'to.'' 'For'' 'more'' 'information,'' 'see'' '"Signing'' 'up'' 'for'' 'a'' 'new'' 'GitHub'' 'account"'' 'and'' '"Security'' 'hardening'' 'for'' '{%'' 'data'' 'variables.product.prodname_actions'' '%}."'' 'Warning:'' 'Although'' 'you'' 'can'' 'generate'' 'the'' '{%'' 'data'' 'variables.product.pat_v1'' '%}'' 'using'' 'your'' 'existing'' 'personal'' 'account,'' 'we'' 'strongly'' 'recommend'' 'creating'' 'a'' 'new'' 'account'' 'with'' 'access'' 'only'' 'to'' 'the'' 'target'' 'repositories'' 'required'' 'for'' 'your'' 'scenario.'' 'This'' 'is'' 'because'' 'the'' 'access'' 'token's'' 'repository'' 'permission'' 'grants'' 'access'' 'to'' 'all'' 'of'' 'the'' 'repositories'' 'that'' 'the'' 'account'' 'has'' 'access'' 'to.'' 'For'' 'more'' 'information,'' 'see'' '"Signing'' 'up'' 'for'' 'a'' 'new'' 'GitHub'' 'account"'' 'and'' '"Security'' 'hardening'' 'for'' '{%'' 'data'' 'variables.product.prodname_actions'' '%}."{%'' 'endwarning'' '%}Give'' 'the'' 'new'' 'account'' 'read'' 'access'' 'to'' 'the'' 'required'' 'repositories.'' 'For'' 'more'' 'information,'' 'see'' '"Managing'' 'an'' 'individual's'' 'access'' 'to'' 'an'' 'organization'' 'repository."While'' 'signed'' 'into'' 'the'' 'new'' 'account,'' 'create'' 'a'' 'PAT'' 'with'' 'the'' 'repo'' 'scope.'' 'Optionally,'' 'if'' 'the'' 'prebuild'' 'will'' 'need'' 'to'' 'download'' 'packages'' 'from'' 'the'' '{%'' 'data'' 'variables.product.company_short'' '%}'' '{%'' 'data'' 'variables.product.prodname_container_registry'' '%},'' 'also'' 'select'' 'the'' 'read:packages'' 'scope.'' 'For'' 'more'' 'information,'' 'see'' '"Creating'' 'a'' 'personal'' 'access'' 'token."While'' 'signed'' 'into'' 'the'' 'new'' 'account,'' 'create'' 'a'' '{%'' 'data'' 'variables.product.pat_v1'' '%}'' 'with'' 'the'' 'repo'' 'scope.'' 'Optionally,'' 'if'' 'the'' 'prebuild'' 'will'' 'need'' 'to'' 'download'' 'packages'' 'from'' 'the'' '{%'' 'data'' 'variables.product.company_short'' '%}'' '{%'' 'data'' 'variables.product.prodname_container_registry'' '%},'' 'also'' 'select'' 'the'' 'read:packages'' 'scope.'' 'For'' 'more'' 'information,'' 'see'' '"Creating'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}."'repo''' 'and'' ''packages''' 'scopes'' 'selected'' 'for'' 'a'' 'PAT'' ''repo''' 'and'' ''packages''' 'scopes'' 'selected'' 'for'' 'a'' '{%'' 'data'' 'variables.product.pat_v1'' '%}If'' 'the'' 'prebuild'' 'will'' 'use'' 'a'' 'package'' 'from'' 'the'' '{%'' 'data'' 'variables.product.company_short'' '%}'' '{%'' 'data'' 'variables.product.prodname_container_registry'' '%},'' 'you'' 'will'' 'need'' 'to'' 'either'' 'grant'' 'the'' 'new'' 'account'' 'access'' 'to'' 'the'' 'package'' 'or'' 'configure'' 'the'' 'package'' 'to'' 'inherit'' 'the'' 'access'' 'permissions'' 'of'' 'the'' 'repository'' 'you'' 'are'' 'prebuilding.'' 'For'' 'more'' 'information,'' 'see'' '"Configuring'' 'a'' 'package's'' 'access'' 'control'' 'and'' 'visibility."
{%'' 'ifversion'' 'ghec'' '%}1.'' 'Authorize'' 'the'' 'token'' 'for'' 'use'' 'with'' 'SAML'' 'single'' 'sign''
'-on'' '(SSO),'' 'so'' 'that'' 'it'' 'can'' 'access'' 'repositories'' 'that'' 'are'' 'owned'' 'by'' 'organizations'' 'with'' 'SSO'' 'enabled.'' 'For'' 'more'' 'information,'' 'see'' '"Authorizing'' 'a'' 'personal'' 'access'' 'token'' 'for'' 'use'' 'with'' 'SAML'' 'single'' 'sign''
'-on."'' '{%'' 'ifversion'' 'ghec'' '%}1.'' 'Authorize'' 'the'' 'token'' 'for'' 'use'' 'with'' 'SAML'' 'single'' 'sign''
'-on'' '(SSO),'' 'so'' 'that'' 'it'' 'can'' 'access'' 'repositories'' 'that'' 'are'' 'owned'' 'by'' 'organizations'' 'with'' 'SSO'' 'enabled.'' 'For'' 'more'' 'information,'' 'see'' '"Authorizing'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'for'' 'use'' 'with'' 'SAML'' 'single'' 'sign''
'-on."The'' 'button'' 'to'' 'configure'' 'SSO'' 'for'' 'a'' 'PAT'' 'The'' 'button'' 'to'' 'configure'' 'SSO'' 'for'' 'a'' '{%'' 'data'' 'variables.product.pat_v1'' '%}{%'' 'endif'' '%}Copy'' 'the'' 'token'' 'string.'' 'You'' 'will'' 'assign'' 'this'' 'to'' 'a'' '{%'' 'data'' 'variables.product.prodname_codespaces'' '%}'' 'repository'' 'secret.
Sign'' 'back'' 'into'' 'the'' 'account'' 'that'' 'has'' 'admin'' 'access'' 'to'' 'the'' 'repository.
In'' 'the'' 'repository'' 'for'' 'which'' 'you'' 'want'' 'to'' 'create'' '{%'' 'data'' 'variables.product.prodname_github_codespaces'' '%}'' 'prebuilds,'' 'create'' 'a'' 'new'' '{%'' 'data'' 'variables.product.prodname_codespaces'' '%}'' 'repository'' 'secret'' 'called'' 'CODESPACES_PREBUILD_TOKEN,'' 'giving'' 'it'' 'the'' 'value'' 'of'' 'the'' 'token'' 'you'' 'created'' 'and'' 'copied.'' 'For'' 'more'' 'information,'' 'see'' '"Managing'' 'encrypted'' 'secrets'' 'for'' 'your'' 'repository'' 'and'' 'organization'' 'for'' '{%'' 'data'' 'variables.product.prodname_github_codespaces'' '%}."
The'' 'PAT'' 'will'' 'be'' 'used'' 'for'' 'all'' 'subsequent'' 'prebuilds'' 'created'' 'for'' 'your'' 'repository.'' 'Unlike'' 'other'' '{%'' 'data'' 'variables.product.prodname_codespaces'' '%}'' 'repository'' 'secrets,'' 'the'' 'CODESPACES_PREBUILD_TOKEN'' 'secret'' 'is'' 'only'' 'used'' 'for'' 'prebuilding'' 'and'' 'will'' 'not'' 'be'' 'available'' 'to'' 'use'' 'in'' 'codespaces'' 'created'' 'from'' 'your'' 'repository.'' 'The'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'will'' 'be'' 'used'' 'for'' 'all'' 'subsequent'' 'prebuilds'' 'created'' 'for'' 'your'' 'repository.'' 'Unlike'' 'other'' '{%'' 'data'' 'variables.product.prodname_codespaces'' '%}'' 'repository'' 'secrets,'' 'the'' 'CODESPACES_PREBUILD_TOKEN'' 'secret'' 'is'' 'only'' 'used'' 'for'' 'prebuilding'' 'and'' 'will'' 'not'' 'be'' 'available'' 'to'' 'use'' 'in'' 'codespaces'' 'created'' 'from'' 'your'' 'repository.Further'' 'reading
2
.../installing''
'-and''
'-authenticating''
'-to''
'-github''
'-desktop/about''
'-connections''
'-to''
'-github.md'' ''@'@'' '''
'-10,7'' '+10,7'' ''@'@'' 'shortTitle:'' 'About'' 'connections
{%'' 'data'' 'variables.product.prodname_desktop'' '%}'' 'connects'' 'to'' '{%'' 'data'' 'variables.product.prodname_dotcom'' '%}'' 'when'' 'you'' 'pull'' 'from,'' 'push'' 'to,'' 'clone,'' 'and'' 'fork'' 'remote'' 'repositories.'' 'To'' 'connect'' 'to'' '{%'' 'data'' 'variables.product.prodname_dotcom'' '%}'' 'from'' '{%'' 'data'' 'variables.product.prodname_desktop'' '%},'' 'you'' 'must'' 'authenticate'' 'your'' 'account.'' 'For'' 'more'' 'information,'' 'see'' '"Authenticating'' 'to'' '{%'' 'data'' 'variables.product.prodname_dotcom'' '%}."After'' 'you'' 'authenticate'' 'to'' '{%'' 'data'' 'variables.product.prodname_dotcom'' '%},'' 'you'' 'can'' 'connect'' 'to'' 'remote'' 'repositories'' 'with'' '{%'' 'data'' 'variables.product.prodname_desktop'' '%}.'' '{%'' 'data'' 'variables.product.prodname_desktop'' '%}'' 'caches'' 'your'' 'credentials'' '(username'' 'and'' 'password'' 'or'' 'personal'' 'access'' 'token)'' 'and'' 'uses'' 'the'' 'credentials'' 'to'' 'authenticate'' 'for'' 'each'' 'connection'' 'to'' 'the'' 'remote'' 'repository.'' 'After'' 'you'' 'authenticate'' 'to'' '{%'' 'data'' 'variables.product.prodname_dotcom'' '%},'' 'you'' 'can'' 'connect'' 'to'' 'remote'' 'repositories'' 'with'' '{%'' 'data'' 'variables.product.prodname_desktop'' '%}.'' '{%'' 'data'' 'variables.product.prodname_desktop'' '%}'' 'caches'' 'your'' 'credentials'' '(username'' 'and'' 'password'' 'or'' '{%'' 'data'' 'variables.product.pat_generic'' '%})'' 'and'' 'uses'' 'the'' 'credentials'' 'to'' 'authenticate'' 'for'' 'each'' 'connection'' 'to'' 'the'' 'remote'' 'repository.{%'' 'data'' 'variables.product.prodname_desktop'' '%}'' 'connects'' 'to'' '{%'' 'data'' 'variables.product.prodname_dotcom'' '%}'' 'using'' 'HTTPS.'' 'If'' 'you'' 'use'' '{%'' 'data'' 'variables.product.prodname_desktop'' '%}'' 'to'' 'access'' 'repositories'' 'that'' 'were'' 'cloned'' 'using'' 'SSH,'' 'you'' 'may'' 'encounter'' 'errors.'' 'To'' 'connect'' 'to'' 'a'' 'repository'' 'that'' 'was'' 'cloned'' 'using'' 'SSH,'' 'change'' 'the'' 'remote's'' 'URLs.'' 'For'' 'more'' 'information,'' 'see'' '"Managing'' 'remote'' 'repositories."2
content/developers/apps/building''
'-oauth''
'-apps/authorizing''
'-oauth''
'-apps.md'' ''@'@'' '''
'-267,7'' '+267,7'' ''@'@'' 'For'' 'more'' 'information,'' 'see'' 'the'' '"[OAuth'' '2.0'' 'Device'' 'Authorization'' 'Grant](https://toNon''
'-Web'' 'application'' 'flow
Non''
'-web'' 'authentication'' 'is'' 'available'' 'for'' 'limited'' 'situations'' 'like'' 'testing.'' 'If'' 'you'' 'need'' 'to,'' 'you'' 'can'' 'use'' 'Basic'' 'Authentication'' 'to'' 'create'' 'a'' 'personal'' 'access'' 'token'' 'using'' 'your'' 'Personal'' 'access'' 'tokens'' 'settings'' 'page.'' 'This'' 'technique'' 'enables'' 'the'' 'user'' 'to'' 'revoke'' 'access'' 'at'' 'any'' 'time.'' 'Non''
'-web'' 'authentication'' 'is'' 'available'' 'for'' 'limited'' 'situations'' 'like'' 'testing.'' 'If'' 'you'' 'need'' 'to,'' 'you'' 'can'' 'use'' 'Basic'' 'Authentication'' 'to'' 'create'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'using'' 'your'' '{%'' 'data'' 'variables.product.pat_generic'' '%}s'' 'settings'' 'page.'' 'This'' 'technique'' 'enables'' 'the'' 'user'' 'to'' 'revoke'' 'access'' 'at'' 'any'' 'time.{%'' 'ifversion'' 'fpt'' 'or'' 'ghes'' 'or'' 'ghec'' '%}'' '{%'' 'note'' '%}'' '2
content/developers/apps/building''
'-oauth''
'-apps/scopes''
'-for''
'-oauth''
'-apps.md'' ''@'@'' '''
'-57,7'' '+57,7'' ''@'@'' 'Name'' '|'' 'Description'' 'admin:public_key'' '|'' 'Fully'' 'manage'' 'public'' 'keys.'' '???write:public_key|'' 'Create,'' 'list,'' 'and'' 'view'' 'details'' 'for'' 'public'' 'keys.'' '???read:public_key|'' 'List'' 'and'' 'view'' 'details'' 'for'' 'public'' 'keys.'' 'admin:org_hook'' '|'' 'Grants'' 'read,'' 'write,'' 'ping,'' 'and'' 'delete'' 'access'' 'to'' 'organization'' 'hooks.'' 'Note:'' 'OAuth'' 'tokens'' 'will'' 'only'' 'be'' 'able'' 'to'' 'perform'' 'these'' 'actions'' 'on'' 'organization'' 'hooks'' 'which'' 'were'' 'created'' 'by'' 'the'' 'OAuth'' 'App.'' 'Personal'' 'access'' 'tokens'' 'will'' 'only'' 'be'' 'able'' 'to'' 'perform'' 'these'' 'actions'' 'on'' 'organization'' 'hooks'' 'created'' 'by'' 'a'' 'user.'' 'admin:org_hook'' '|'' 'Grants'' 'read,'' 'write,'' 'ping,'' 'and'' 'delete'' 'access'' 'to'' 'organization'' 'hooks.'' 'Note:'' 'OAuth'' 'tokens'' 'will'' 'only'' 'be'' 'able'' 'to'' 'perform'' 'these'' 'actions'' 'on'' 'organization'' 'hooks'' 'which'' 'were'' 'created'' 'by'' 'the'' 'OAuth'' 'App.'' '{%'' 'data'' 'variables.product.pat_generic_caps'' '%}s'' 'will'' 'only'' 'be'' 'able'' 'to'' 'perform'' 'these'' 'actions'' 'on'' 'organization'' 'hooks'' 'created'' 'by'' 'a'' 'user.'' 'gist'' '|'' 'Grants'' 'write'' 'access'' 'to'' 'gists.'' 'notifications'' '|'' 'Grants:
*'' 'read'' 'access'' 'to'' 'a'' 'user's'' 'notifications
*'' 'mark'' 'as'' 'read'' 'access'' 'to'' 'threads
*'' 'watch'' 'and'' 'unwatch'' 'access'' 'to'' 'a'' 'repository,'' 'and
*'' 'read,'' 'write,'' 'and'' 'delete'' 'access'' 'to'' 'thread'' 'subscriptions.'' 'user'' '|'' 'Grants'' 'read/write'' 'access'' 'to'' 'profile'' 'info'' 'only.'' 'Note'' 'that'' 'this'' 'scope'' 'includes'' 'user:email'' 'and'' 'user:follow.'' '15
content/developers/apps/getting''
'-started''
'-with''
'-apps/about''
'-apps.md'' ''@'@'' '''
'-72,24'' '+72,25'' ''@'@'' 'Keep'' 'these'' 'ideas'' 'in'' 'mind'' 'when'' 'creating'' '{%'' 'data'' 'variables.product.prodname_oauth_For'' 'more'' 'on'' '{%'' 'data'' 'variables.product.prodname_oauth_apps'' '%},'' 'see'' '"Creating'' 'an'' '{%'' 'data'' 'variables.product.prodname_oauth_app'' '%}"'' 'and'' '"Registering'' 'your'' 'app."Personal'' 'access'' 'tokens
{%'' 'data'' 'variables.product.pat_generic_caps'' '%}s
A'' 'personal'' 'access'' 'token'' 'is'' 'a'' 'string'' 'of'' 'characters'' 'that'' 'functions'' 'similarly'' 'to'' 'an'' 'OAuth'' 'token'' 'in'' 'that'' 'you'' 'can'' 'specify'' 'its'' 'permissions'' 'via'' 'scopes.'' 'A'' 'personal'' 'access'' 'token'' 'is'' 'also'' 'similar'' 'to'' 'a'' 'password,'' 'but'' 'you'' 'can'' 'have'' 'many'' 'of'' 'them'' 'and'' 'you'' 'can'' 'revoke'' 'access'' 'to'' 'each'' 'one'' 'at'' 'any'' 'time.'' 'A'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'is'' 'a'' 'string'' 'of'' 'characters'' 'that'' 'functions'' 'similarly'' 'to'' 'an'' 'OAuth'' 'token'' 'in'' 'that'' 'you'' 'can'' 'specify'' 'its'' 'permissions'' 'via'' 'scopes.'' 'A'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'is'' 'also'' 'similar'' 'to'' 'a'' 'password,'' 'but'' 'you'' 'can'' 'have'' 'many'' 'of'' 'them'' 'and'' 'you'' 'can'' 'revoke'' 'access'' 'to'' 'each'' 'one'' 'at'' 'any'' 'time.As'' 'an'' 'example,'' 'you'' 'can'' 'enable'' 'a'' 'personal'' 'access'' 'token'' 'to'' 'write'' 'to'' 'your'' 'repositories.'' 'If'' 'then'' 'you'' 'run'' 'a'' 'cURL'' 'command'' 'or'' 'write'' 'a'' 'script'' 'that'' 'creates'' 'an'' 'issue'' 'in'' 'your'' 'repository,'' 'you'' 'would'' 'pass'' 'the'' 'personal'' 'access'' 'token'' 'to'' 'authenticate.'' 'You'' 'can'' 'store'' 'the'' 'personal'' 'access'' 'token'' 'as'' 'an'' 'environment'' 'variable'' 'to'' 'avoid'' 'typing'' 'it'' 'every'' 'time'' 'you'' 'use'' 'it.'' 'As'' 'an'' 'example,'' 'you'' 'can'' 'enable'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'to'' 'write'' 'to'' 'your'' 'repositories.'' 'If'' 'then'' 'you'' 'run'' 'a'' 'cURL'' 'command'' 'or'' 'write'' 'a'' 'script'' 'that'' 'creates'' 'an'' 'issue'' 'in'' 'your'' 'repository,'' 'you'' 'would'' 'pass'' 'the'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'to'' 'authenticate.'' 'You'' 'can'' 'store'' 'the'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'as'' 'an'' 'environment'' 'variable'' 'to'' 'avoid'' 'typing'' 'it'' 'every'' 'time'' 'you'' 'use'' 'it.Keep'' 'these'' 'ideas'' 'in'' 'mind'' 'when'' 'using'' 'personal'' 'access'' 'tokens:'' 'Keep'' 'these'' 'ideas'' 'in'' 'mind'' 'when'' 'using'' '{%'' 'data'' 'variables.product.pat_generic'' '%}s:Remember'' 'to'' 'use'' 'this'' 'token'' 'to'' 'represent'' 'yourself'' 'only.
You'' 'can'' 'perform'' 'one''
'-off'' 'cURL'' 'requests.
You'' 'can'' 'run'' 'personal'' 'build_script.
Don't'' 'set'' 'up'' 'a'' 'script'' 'for'' 'your'' 'whole'' 'team'' 'or'' 'company'' 'to'' 'use.
Don't'' 'set'' 'up'' 'a'' 'shared'' 'personal'' 'account'' 'to'' 'act'' 'as'' 'a'' 'bot'' 'user.{%'' 'ifversion'' 'fpt'' 'or'' 'ghes'' '>'' '3.2'' 'or'' 'ghae'' 'or'' 'ghec'' '%}
Do'' 'set'' 'an'' 'expiration'' 'for'' 'your'' 'personal'' 'access'' 'tokens,'' 'to'' 'help'' 'keep'' 'your'' 'information'' 'secure.{%'' 'endif'' '%}
Grant'' 'your'' 'token'' 'the'' 'minimal'' 'privileges'' 'it'' 'needs.
Set'' 'an'' 'expiration'' 'for'' 'your'' '{%'' 'data'' 'variables.product.pat_generic'' '%}s,'' 'to'' 'help'' 'keep'' 'your'' 'information'' 'secure.{%'' 'endif'' '%}
Determining'' 'which'' 'integration'' 'to'' 'build
Before'' 'you'' 'get'' 'started'' 'creating'' 'integrations,'' 'you'' 'need'' 'to'' 'determine'' 'the'' 'best'' 'way'' 'to'' 'access,'' 'authenticate,'' 'and'' 'interact'' 'with'' 'the'' '{%'' 'ifversion'' 'fpt'' 'or'' 'ghec'' '%}{%'' 'data'' 'variables.product.prodname_dotcom'' '%}{%'' 'else'' '%}{%'' 'data'' 'variables.product.product_name'' '%}{%'' 'endif'' '%}'' 'APIs.'' 'The'' 'following'' 'image'' 'offers'' 'some'' 'questions'' 'to'' 'ask'' 'yourself'' 'when'' 'deciding'' 'whether'' 'to'' 'use'' 'personal'' 'access'' 'tokens,'' '{%'' 'data'' 'variables.product.prodname_github_apps'' '%},'' 'or'' '{%'' 'data'' 'variables.product.prodname_oauth_apps'' '%}'' 'for'' 'your'' 'integration.'' 'Before'' 'you'' 'get'' 'started'' 'creating'' 'integrations,'' 'you'' 'need'' 'to'' 'determine'' 'the'' 'best'' 'way'' 'to'' 'access,'' 'authenticate,'' 'and'' 'interact'' 'with'' 'the'' '{%'' 'ifversion'' 'fpt'' 'or'' 'ghec'' '%}{%'' 'data'' 'variables.product.prodname_dotcom'' '%}{%'' 'else'' '%}{%'' 'data'' 'variables.product.product_name'' '%}{%'' 'endif'' '%}'' 'APIs.'' 'The'' 'following'' 'image'' 'offers'' 'some'' 'questions'' 'to'' 'ask'' 'yourself'' 'when'' 'deciding'' 'whether'' 'to'' 'use'' '{%'' 'data'' 'variables.product.pat_generic'' '%}s,'' '{%'' 'data'' 'variables.product.prodname_github_apps'' '%},'' 'or'' '{%'' 'data'' 'variables.product.prodname_oauth_apps'' '%}'' 'for'' 'your'' 'integration.Intro'' 'to'' 'apps'' 'question'' 'flow'@'@'' '''
'-98,7'' '+99,7'' ''@'@'' 'Consider'' 'these'' 'questions'' 'about'' 'how'' 'your'' 'integration'' 'needs'' 'to'' 'behave'' 'and'' 'what'' 'itWill'' 'my'' 'integration'' 'act'' 'only'' 'as'' 'me,'' 'or'' 'will'' 'it'' 'act'' 'more'' 'like'' 'an'' 'application?
Do'' 'I'' 'want'' 'it'' 'to'' 'act'' 'independently'' 'of'' 'me'' 'as'' 'its'' 'own'' 'entity?
Will'' 'it'' 'access'' 'everything'' 'that'' 'I'' 'can'' 'access,'' 'or'' 'do'' 'I'' 'want'' 'to'' 'limit'' 'its'' 'access?
Is'' 'it'' 'simple'' 'or'' 'complex?'' 'For'' 'example,'' 'personal'' 'access'' 'tokens'' 'are'' 'good'' 'for'' 'simple'' 'build_script'' 'and'' 'cURLs,'' 'whereas'' 'an'' '{%'' 'data'' 'variables.product.prodname_oauth_app'' '%}'' 'can'' 'handle'' 'more'' 'complex'' 'scripting.
Is'' 'it'' 'simple'' 'or'' 'complex?'' 'For'' 'example,'' '{%'' 'data'' 'variables.product.pat_generic'' '%}s'' 'are'' 'good'' 'for'' 'simple'' 'build_script'' 'and'' 'cURLs,'' 'whereas'' 'an'' '{%'' 'data'' 'variables.product.prodname_oauth_app'' '%}'' 'can'' 'handle'' 'more'' 'complex'' 'scripting.
Requesting'' 'support
2
...tplace/creating''
'-apps''
'-for''
'-github''
'-marketplace/security''
'-best''
'-practices''
'-for''
'-apps.md'' ''@'@'' '''
'-25,7'' '+25,7'' ''@'@'' 'We'' 'recommend'' 'creating'' 'a'' 'GitHub'' 'App'' 'rather'' 'than'' 'an'' 'OAuth'' 'App.'' '{%'' 'data'' 'reusables.mApps'' 'should'' 'not'' 'share'' 'service'' 'accounts'' 'such'' 'as'' 'email'' 'or'' 'database'' 'services'' 'to'' 'manage'' 'your'' 'SaaS'' 'service.All'' 'services'' 'used'' 'in'' 'your'' 'app'' 'should'' 'have'' 'unique'' 'login'' 'and'' 'password'' 'credentials.Admin'' 'privilege'' 'access'' 'to'' 'the'' 'production'' 'hosting'' 'infrastructure'' 'should'' 'only'' 'be'' 'given'' 'to'' 'engineers'' 'and'' 'employees'' 'with'' 'administrative'' 'duties.Apps'' 'should'' 'not'' 'use'' 'personal'' 'access'' 'tokens'' 'to'' 'authenticate'' 'and'' 'should'' 'authenticate'' 'as'' 'an'' 'OAuth'' 'App'' 'or'' 'a'' 'GitHub'' 'App:Apps'' 'should'' 'not'' 'use'' '{%'' 'data'' 'variables.product.pat_generic'' '%}s'' 'to'' 'authenticate'' 'and'' 'should'' 'authenticate'' 'as'' 'an'' 'OAuth'' 'App'' 'or'' 'a'' 'GitHub'' 'App:OAuth'' 'Apps'' 'should'' 'authenticate'' 'using'' 'an'' 'OAuth'' 'token.
GitHub'' 'Apps'' 'should'' 'authenticate'' 'using'' 'either'' 'a'' 'JSON'' 'Web'' 'Token'' '(JWT),'' 'OAuth'' 'token,'' 'or'' 'installation'' 'access'' 'token.
2
content/developers/overview/managing''
'-deploy''
'-keys.md'' ''@'@'' '''
'-61,7'' '+61,7'' ''@'@'' 'If'' 'you'' 'don't'' 'want'' 'to'' 'use'' 'SSH'' 'keys,'' 'you'' 'can'' 'use'' 'HTTPS'' 'with'' 'OAuth'' 'tokens.Setup
See'' 'our'' 'guide'' 'on'' 'creating'' 'a'' 'personal'' 'access'' 'token.'' 'See'' 'our'' 'guide'' 'on'' 'creating'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}.Deploy'' 'keys
4
content/developers/overview/secret''
'-scanning''
'-partner''
'-program.md'' ''@'@'' '''
'-110,7'' '+110,7'' ''@'@'' 'key'' 'to'' 'use'' 'based'' 'on'' 'the'' 'value'' 'of'' 'GITHUB''
'-PUBLIC''
'-KEY''
'-IDENTIFIER.{%'' 'note'' '%}Note:'' 'When'' 'you'' 'send'' 'a'' 'request'' 'to'' 'the'' 'public'' 'key'' 'endpoint'' 'above,'' 'you'' 'may'' 'hit'' 'rate'' 'limits.'' 'To'' 'avoid'' 'hitting'' 'rate'' 'limits,'' 'you'' 'can'' 'use'' 'a'' 'personal'' 'access'' 'token'' '(no'' 'scopes'' 'required)'' 'as'' 'suggested'' 'in'' 'the'' 'samples'' 'below,'' 'or'' 'use'' 'a'' 'conditional'' 'request.'' 'For'' 'more'' 'information,'' 'see'' '"Getting'' 'started'' 'with'' 'the'' 'REST'' 'API."'' 'Note:'' 'When'' 'you'' 'send'' 'a'' 'request'' 'to'' 'the'' 'public'' 'key'' 'endpoint'' 'above,'' 'you'' 'may'' 'hit'' 'rate'' 'limits.'' 'To'' 'avoid'' 'hitting'' 'rate'' 'limits,'' 'you'' 'can'' 'use'' 'a'' '{%'' 'data'' 'variables.product.pat_v1'' '%}'' '(no'' 'scopes'' 'required){%'' 'ifversion'' 'pat''
'-v2'' '%}'' 'or'' 'a'' '{%'' 'data'' 'variables.product.pat_v2'' '%}'' '(only'' 'the'' 'automatic'' 'public'' 'repositories'' 'read'' 'access'' 'required){%'' 'endif'' '%}'' 'as'' 'suggested'' 'in'' 'the'' 'samples'' 'below,'' 'or'' 'use'' 'a'' 'conditional'' 'request.'' 'For'' 'more'' 'information,'' 'see'' '"Getting'' 'started'' 'with'' 'the'' 'REST'' 'API."{%'' 'endnote'' '%}'@'@'' '''
'-149,7'' '+149,7'' ''@'@'' 'HzZFI03Exwz8Lh/tCfL3YxwMdLjB+bMznsanlhK0RwcGP3IDb34kQDIo3Q=='' '{%'' 'endnote'' '%}The'' 'following'' 'code'' 'snippets'' 'demonstrate'' 'how'' 'you'' 'could'' 'perform'' 'signature'' 'validation.'' 'The'' 'code'' 'examples'' 'assume'' 'you've'' 'set'' 'an'' 'environment'' 'variable'' 'called'' 'GITHUB_PRODUCTION_TOKEN'' 'with'' 'a'' 'generated'' 'personal'' 'access'' 'token'' '(PAT)'' 'to'' 'avoid'' 'hitting'' 'rate'' 'limits.'' 'The'' 'PAT'' 'does'' 'not'' 'need'' 'any'' 'scopes/permissions.'' 'The'' 'code'' 'examples'' 'assume'' 'you've'' 'set'' 'an'' 'environment'' 'variable'' 'called'' 'GITHUB_PRODUCTION_TOKEN'' 'with'' 'a'' 'generated'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'to'' 'avoid'' 'hitting'' 'rate'' 'limits.'' 'The'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'does'' 'not'' 'need'' 'any'' 'scopes/permissions.Validation'' 'sample'' 'in'' 'Go'' ''' '2'' ''' '
.../get''
'-started/getting''
'-started''
'-with''
'-git/caching''
'-your''
'-github''
'-credentials''
'-in''
'-git.md
'@'@'' '''
'-35,7'' '+35,7'' ''@'@'' 'For'' 'more'' 'information'' 'about'' 'authenticating'' 'with'' '{%'' 'data'' 'variables.product.prodnam##'' 'Git'' 'Credential'' 'Manager[Git'' 'Credential'' 'Manager](https://github.com/GitCredentialManager/git''
'-credential''
'-manager)'' '(GCM)'' 'is'' 'another'' 'way'' 'to'' 'store'' 'your'' 'credentials'' 'securely'' 'and'' 'connect'' 'to'' 'GitHub'' 'over'' 'HTTPS.'' 'With'' 'GCM,'' 'you'' 'don't'' 'have'' 'to'' 'manually'' '[create'' 'and'' 'store'' 'a'' 'PAT](/github/authenticating''
'-to''
'-github/creating''
'-a''
'-personal''
'-access''
'-token),'' 'as'' 'GCM'' 'manages'' 'authentication'' 'on'' 'your'' 'behalf,'' 'including'' '2FA'' '(two''
'-factor'' 'authentication).
[Git'' 'Credential'' 'Manager](https://github.com/GitCredentialManager/git''
'-credential''
'-manager)'' '(GCM)'' 'is'' 'another'' 'way'' 'to'' 'store'' 'your'' 'credentials'' 'securely'' 'and'' 'connect'' 'to'' 'GitHub'' 'over'' 'HTTPS.'' 'With'' 'GCM,'' 'you'' 'don't'' 'have'' 'to'' 'manually'' '[create'' 'and'' 'store'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}](/github/authenticating''
'-to''
'-github/creating''
'-a''
'-personal''
'-access''
'-token),'' 'as'' 'GCM'' 'manages'' 'authentication'' 'on'' 'your'' 'behalf,'' 'including'' '2FA'' '(two''
'-factor'' 'authentication).{%'' 'mac'' '%}'' ''' '2'' ''' '
content/get''
'-started/getting''
'-started''
'-with''
'-git/managing''
'-remote''
'-repositories.md
'@'@'' '''
'-108,7'' '+108,7'' ''@'@'' 'git'@{%'' 'data'' 'variables.command_line.codeblock'' '%}:USERNAME/REPOSITORY.gitThe'' 'next'' 'time'' 'you'' '`git'' 'fetch`,'' '`git'' 'pull`,'' 'or'' '`git'' 'push`'' 'to'' 'the'' 'remote'' 'repository,'' 'you'll'' 'be'' 'asked'' 'for'' 'your'' 'GitHub'' 'username'' 'and'' 'password.'' '{%'' 'data'' 'reusables.user''
'-settings.password''
'-authentication''
'-deprecation'' '%}You'' 'can'' '[use'' 'a'' 'credential'' 'helper](/github/getting''
'-started''
'-with''
'-github/caching''
'-your''
'-github''
'-credentials''
'-in''
'-git)'' 'so'' 'Git'' 'will'' 'remember'' 'your'' 'GitHub'' 'username'' 'and'' 'personal'' 'access'' 'token'' 'every'' 'time'' 'it'' 'talks'' 'to'' 'GitHub.
You'' 'can'' '[use'' 'a'' 'credential'' 'helper](/github/getting''
'-started''
'-with''
'-github/caching''
'-your''
'-github''
'-credentials''
'-in''
'-git)'' 'so'' 'Git'' 'will'' 'remember'' 'your'' 'GitHub'' 'username'' 'and'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'every'' 'time'' 'it'' 'talks'' 'to'' 'GitHub.###'' 'Switching'' 'remote'' 'URLs'' 'from'' 'HTTPS'' 'to'' 'SSH'' ''' '6'' ''' '
...tarted/getting''
'-started''
'-with''
'-git/updating''
'-credentials''
'-from''
'-the''
'-macos''
'-keychain.md
'@'@'' '''
'-1,6'' '+1,6'' ''@'@
''
'-
title:'' 'Updating'' 'credentials'' 'from'' 'the'' 'macOS'' 'Keychain
intro:'' ''You''ll'' 'need'' 'to'' 'update'' 'your'' 'saved'' 'credentials'' 'in'' 'the'' '`git''
'-credential''
'-osxkeychain`'' 'helper'' 'if'' 'you'' 'change'' 'your{%'' 'ifversion'' 'not'' 'ghae'' '%}'' 'username,'' 'password,'' 'or{%'' 'endif'' '%}'' 'personal'' 'access'' 'token'' 'on'' '{%'' 'data'' 'variables.product.product_name'' '%}.'
intro:'' ''You''ll'' 'need'' 'to'' 'update'' 'your'' 'saved'' 'credentials'' 'in'' 'the'' '`git''
'-credential''
'-osxkeychain`'' 'helper'' 'if'' 'you'' 'change'' 'your{%'' 'ifversion'' 'not'' 'ghae'' '%}'' 'username,'' 'password,'' 'or{%'' 'endif'' '%}'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'on'' '{%'' 'data'' 'variables.product.product_name'' '%}.'
redirect_from:
'' ''' ''' '/articles/updating''
'-credentials''
'-from''
'-the''
'-osx''
'-keychain
'' ''' ''' '/github/using''
'-git/updating''
'-credentials''
'-from''
'-the''
'-osx''
'-keychain
'@'@'' '''
'-16,9'' '+16,9'' ''@'@'' 'shortTitle:'' 'macOS'' 'Keychain'' 'credentials
''
'-
{%'' 'tip'' '%}**Note:**'' 'Updating'' 'credentials'' 'from'' 'the'' 'macOS'' 'Keychain'' 'only'' 'applies'' 'to'' 'users'' 'who'' 'manually'' 'configured'' 'a'' 'PAT'' 'using'' 'the'' ''' '`osxkeychain`'' 'helper'' 'that'' 'is'' 'built''
'-in'' 'to'' 'macOS.'' '
**Note:**'' 'Updating'' 'credentials'' 'from'' 'the'' 'macOS'' 'Keychain'' 'only'' 'applies'' 'to'' 'users'' 'who'' 'manually'' 'configured'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'using'' 'the'' ''' '`osxkeychain`'' 'helper'' 'that'' 'is'' 'built''
'-in'' 'to'' 'macOS.'' 'We'' 'recommend'' 'you'' 'either'' '[configure'' 'SSH](/articles/generating''
'-an''
'-ssh''
'-key)'' 'or'' 'upgrade'' 'to'' 'the'' '[Git'' 'Credential'' 'Manager](/get''
'-started/getting''
'-started''
'-with''
'-git/caching''
'-your''
'-github''
'-credentials''
'-in''
'-git)'' '(GCM)'' 'instead.'' 'GCM'' 'can'' 'manage'' 'authentication'' 'on'' 'your'' 'behalf'' '(no'' 'more'' 'manual'' 'PATs)'' 'including'' '2FA'' '(two''
'-factor'' 'auth).
We'' 'recommend'' 'you'' 'either'' '[configure'' 'SSH](/articles/generating''
'-an''
'-ssh''
'-key)'' 'or'' 'upgrade'' 'to'' 'the'' '[Git'' 'Credential'' 'Manager](/get''
'-started/getting''
'-started''
'-with''
'-git/caching''
'-your''
'-github''
'-credentials''
'-in''
'-git)'' '(GCM)'' 'instead.'' 'GCM'' 'can'' 'manage'' 'authentication'' 'on'' 'your'' 'behalf'' '(no'' 'more'' 'manual'' '{%'' 'data'' 'variables.product.pat_generic'' '%}s)'' 'including'' '2FA'' '(two''
'-factor'' 'auth).{%'' 'endtip'' '%}'' ''' '2'' ''' '
...et''
'-started/getting''
'-started''
'-with''
'-git/why''
'-is''
'-git''
'-always''
'-asking''
'-for''
'-my''
'-password.md
'@'@'' '''
'-17,7'' '+17,7'' ''@'@'' 'Using'' 'an'' 'HTTPS'' 'remote'' 'URL'' 'has'' 'some'' 'advantages'' 'compared'' 'with'' 'using'' 'SSH.'' 'It's'' 'easi{%'' 'data'' 'reusables.user''
'-settings.password''
'-authentication''
'-deprecation'' '%}You'' 'can'' 'avoid'' 'being'' 'prompted'' 'for'' 'your'' 'password'' 'by'' 'configuring'' 'Git'' 'to'' '[cache'' 'your'' 'credentials](/github/getting''
'-started''
'-with''
'-github/caching''
'-your''
'-github''
'-credentials''
'-in''
'-git)'' 'for'' 'you.'' 'Once'' 'you've'' 'configured'' 'credential'' 'caching,'' 'Git'' 'automatically'' 'uses'' 'your'' 'cached'' 'personal'' 'access'' 'token'' 'when'' 'you'' 'pull'' 'or'' 'push'' 'a'' 'repository'' 'using'' 'HTTPS.
You'' 'can'' 'avoid'' 'being'' 'prompted'' 'for'' 'your'' 'password'' 'by'' 'configuring'' 'Git'' 'to'' '[cache'' 'your'' 'credentials](/github/getting''
'-started''
'-with''
'-github/caching''
'-your''
'-github''
'-credentials''
'-in''
'-git)'' 'for'' 'you.'' 'Once'' 'you've'' 'configured'' 'credential'' 'caching,'' 'Git'' 'automatically'' 'uses'' 'your'' 'cached'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'when'' 'you'' 'pull'' 'or'' 'push'' 'a'' 'repository'' 'using'' 'HTTPS.##'' 'Further'' 'reading'' ''' '2'' ''' '
.../importing''
'-source''
'-code''
'-to''
'-github/importing''
'-a''
'-repository''
'-with''
'-github''
'-importer.md
'@'@'' '''
'-32,7'' '+32,7'' ''@'@'' 'If'' 'you'd'' 'like'' 'to'' 'match'' 'the'' 'commits'' 'in'' 'your'' 'repository'' 'to'' 'the'' 'authors''' 'GitHub'' 'per
5.'' 'Review'' 'the'' 'information'' 'you'' 'entered,'' 'then'' 'click'' '**Begin'' 'import**.
![Begin'' 'import'' 'button](/assets/images/help/importer/begin''
'-import''
'-button.png)
6.'' 'If'' 'your'' 'old'' 'project'' 'requires'' 'credentials,'' 'type'' 'your'' 'login'' 'information'' 'for'' 'that'' 'project,'' 'then'' 'click'' '**Submit**.'' '
If'' 'SAML'' 'SSO'' 'or'' '2FA'' 'are'' 'enabled'' 'for'' 'your'' 'user'' 'account'' 'on'' 'the'' 'old'' 'project,'' 'enter'' 'a'' 'personal'' 'access'' 'token'' 'with'' 'repository'' 'read'' 'permissions'' 'in'' 'the'' '"Password"'' 'field'' 'instead'' 'of'' 'your'' 'password.
If'' 'SAML'' 'SSO'' 'or'' '2FA'' 'are'' 'enabled'' 'for'' 'your'' 'user'' 'account'' 'on'' 'the'' 'old'' 'project,'' 'enter'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'with'' 'repository'' 'read'' 'permissions'' 'in'' 'the'' '"Password"'' 'field'' 'instead'' 'of'' 'your'' 'password.
![Password'' 'form'' 'and'' 'Submit'' 'button'' 'for'' 'password''
'-protected'' 'project](/assets/images/help/importer/submit''
'-old''
'-credentials''
'-importer.png)
7.'' 'If'' 'there'' 'are'' 'multiple'' 'projects'' 'hosted'' 'at'' 'your'' 'old'' 'project's'' 'clone'' 'URL,'' 'choose'' 'the'' 'project'' 'you'd'' 'like'' 'to'' 'import,'' 'then'' 'click'' '**Submit**.
![List'' 'of'' 'projects'' 'to'' 'import'' 'and'' 'Submit'' 'button](/assets/images/help/importer/choose''
'-project''
'-importer.png)
'' ''' '2'' ''' '
content/get''
'-started/signing''
'-up''
'-for''
'-github/verifying''
'-your''
'-email''
'-address.md
'@'@'' '''
'-23,7'' '+23,7'' ''@'@'' 'If'' 'you'' 'do'' 'not'' 'verify'' 'your'' 'email'' 'address,'' 'you'' 'will'' 'not'' 'be'' 'able'' 'to:
'' ''' ''' 'Create'' 'issues'' 'or'' 'pull'' 'requests
'' ''' ''' 'Comment'' 'on'' 'issues,'' 'pull'' 'requests,'' 'or'' 'commits
'' ''' ''' 'Authorize'' '{%'' 'data'' 'variables.product.prodname_oauth_app'' '%}'' 'applications
'' ''' ''' 'Generate'' 'personal'' 'access'' 'tokens
'' ''' ''' 'Generate'' '{%'' 'data'' 'variables.product.pat_generic'' '%}s
'' ''' ''' 'Receive'' 'email'' 'notifications
'' ''' ''' 'Star'' 'repositories
'' ''' ''' 'Create'' 'or'' 'update'' 'project'' 'boards,'' 'including'' 'adding'' 'cards
'' ''' '6'' ''' '
content/graphql/guides/forming''
'-calls''
'-with''
'-graphql.md
'@'@'' '''
'-16,9'' '+16,11'' ''@'@'' 'shortTitle:'' 'Form'' 'calls'' 'with'' 'GraphQL##'' 'Authenticating'' 'with'' 'GraphQLTo'' 'communicate'' 'with'' 'the'' 'GraphQL'' 'server,'' 'you'll'' 'need'' 'an'' 'OAuth'' 'token'' 'with'' 'the'' 'right'' 'scopes.
{%'' 'data'' 'reusables.user''
'-settings.graphql''
'-classic''
'-pat''
'-only'' '%}Follow'' 'the'' 'steps'' 'in'' '"[Creating'' 'a'' 'personal'' 'access'' 'token](/github/authenticating''
'-to''
'-github/creating''
'-a''
'-personal''
'-access''
'-token)"'' 'to'' 'create'' 'a'' 'token.'' 'The'' 'scopes'' 'you'' 'require'' 'depends'' 'on'' 'the'' 'type'' 'of'' 'data'' 'you're'' 'trying'' 'to'' 'request.'' 'For'' 'example,'' 'select'' 'the'' '**User**'' 'scopes'' 'to'' 'request'' 'user'' 'data.'' 'If'' 'you'' 'need'' 'access'' 'to'' 'repository'' 'information,'' 'select'' 'the'' 'appropriate'' '**Repository**'' 'scopes.
To'' 'communicate'' 'with'' 'the'' 'GraphQL'' 'server,'' 'you'll'' 'need'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'with'' 'the'' 'right'' 'scopes.Follow'' 'the'' 'steps'' 'in'' '"[Creating'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}](/github/authenticating''
'-to''
'-github/creating''
'-a''
'-personal''
'-access''
'-token)"'' 'to'' 'create'' 'a'' 'token.'' 'The'' 'scopes'' 'you'' 'require'' 'depends'' 'on'' 'the'' 'type'' 'of'' 'data'' 'you're'' 'trying'' 'to'' 'request.'' 'For'' 'example,'' 'select'' 'the'' '**User**'' 'scopes'' 'to'' 'request'' 'user'' 'data.'' 'If'' 'you'' 'need'' 'access'' 'to'' 'repository'' 'information,'' 'select'' 'the'' 'appropriate'' '**Repository**'' 'scopes.{%'' 'ifversion'' 'fpt'' 'or'' 'ghec'' '%}'' ''' '2'' ''' '
content/graphql/guides/introduction''
'-to''
'-graphql.md
'@'@'' '''
'-121,7'' '+121,7'' ''@'@'' 'GraphQL'' 'is'' '[introspective](https://graphql.github.io/learn/introspection/).'' 'This'' ''' '{%'' 'note'' '%}'' ''' '**Note**:'' 'If'' 'you'' 'get'' 'the'' 'response'' '`"message":'' '"Bad'' 'credentials"`'' 'or'' '`401'' 'Unauthorized`,'' 'check'' 'that'' 'you'' 'are'' 'using'' 'a'' 'valid'' 'token.'' 'For'' 'more'' 'information,'' 'see'' '"[Creating'' 'a'' 'personal'' 'access'' 'token](/github/authenticating''
'-to''
'-github/creating''
'-a''
'-personal''
'-access''
'-token)."'' '
'' ''' '**Note**:'' 'If'' 'you'' 'get'' 'the'' 'response'' '`"message":'' '"Bad'' 'credentials"`'' 'or'' '`401'' 'Unauthorized`,'' 'check'' 'that'' 'you'' 'are'' 'using'' 'a'' 'valid'' 'token.'' 'The'' 'GraphQL'' 'API'' 'only'' 'supports'' 'authentication'' 'using'' 'a'' '{%'' 'data'' 'variables.product.pat_v1'' '%}.'' 'For'' 'more'' 'information,'' 'see'' '"[Creating'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}](/github/authenticating''
'-to''
'-github/creating''
'-a''
'-personal''
'-access''
'-token)."'' ''' ''' '{%'' 'endnote'' '%}'' ''' '18'' ''' '
content/graphql/guides/managing''
'-enterprise''
'-accounts.md
'@'@'' '''
'-41,17'' '+41,19'' ''@'@'' 'For'' 'a'' 'list'' 'of'' 'the'' 'fields'' 'available'' 'with'' 'the'' 'Enterprise'' 'Accounts'' 'API,'' 'see'' '"[Graph
##'' 'Getting'' 'started'' 'using'' 'GraphQL'' 'for'' 'enterprise'' 'accountsFollow'' 'these'' 'steps'' 'to'' 'get'' 'started'' 'using'' 'GraphQL'' 'to'' 'manage'' 'your'' 'enterprise'' 'accounts:
'' ''' 'Authenticating'' 'with'' 'a'' 'personal'' 'access'' 'token
'' ''' 'Authenticating'' 'with'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}
'' ''' 'Choosing'' 'a'' 'GraphQL'' 'client'' 'or'' 'using'' 'the'' 'GraphQL'' 'Explorer
'' ''' 'Setting'' 'up'' 'Insomnia'' 'to'' 'use'' 'the'' 'GraphQL'' 'APIFor'' 'some'' 'example'' 'queries,'' 'see'' '"[An'' 'example'' 'query'' 'using'' 'the'' 'Enterprise'' 'Accounts'' 'API](#an''
'-example''
'-query''
'-using''
'-the''
'-enterprise''
'-accounts''
'-api)."###'' '1.'' 'Authenticate'' 'with'' 'your'' 'personal'' 'access'' 'token
###'' '1.'' 'Authenticate'' 'with'' 'your'' '{%'' 'data'' 'variables.product.pat_generic'' '%}1.'' 'To'' 'authenticate'' 'with'' 'GraphQL,'' 'you'' 'need'' 'to'' 'generate'' 'a'' 'personal'' 'access'' 'token'' '(PAT)'' 'from'' 'developer'' 'settings.'' 'For'' 'more'' 'information,'' 'see'' '"[Creating'' 'a'' 'personal'' 'access'' 'token](/github/authenticating''
'-to''
'-github/creating''
'-a''
'-personal''
'-access''
'-token)."
{%'' 'data'' 'reusables.user''
'-settings.graphql''
'-classic''
'-pat''
'-only'' '%}2.'' 'Grant'' 'admin'' 'and'' 'full'' 'control'' 'permissions'' 'to'' 'your'' 'personal'' 'access'' 'token'' 'for'' 'areas'' 'of'' 'GHES'' 'you'd'' 'like'' 'to'' 'access.'' 'For'' 'full'' 'permission'' 'to'' 'private'' 'repositories,'' 'organizations,'' 'teams,'' 'user'' 'data,'' 'and'' 'access'' 'to'' 'enterprise'' 'billing'' 'and'' 'profile'' 'data,'' 'we'' 'recommend'' 'you'' 'select'' 'these'' 'scopes'' 'for'' 'your'' 'personal'' 'access'' 'token:
1.'' 'To'' 'authenticate'' 'with'' 'GraphQL,'' 'you'' 'need'' 'to'' 'generate'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'from'' 'developer'' 'settings.'' 'For'' 'more'' 'information,'' 'see'' '"[Creating'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}](/github/authenticating''
'-to''
'-github/creating''
'-a''
'-personal''
'-access''
'-token)."2.'' 'Grant'' 'admin'' 'and'' 'full'' 'control'' 'permissions'' 'to'' 'your'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'for'' 'areas'' 'of'' 'GHES'' 'you'd'' 'like'' 'to'' 'access.'' 'For'' 'full'' 'permission'' 'to'' 'private'' 'repositories,'' 'organizations,'' 'teams,'' 'user'' 'data,'' 'and'' 'access'' 'to'' 'enterprise'' 'billing'' 'and'' 'profile'' 'data,'' 'we'' 'recommend'' 'you'' 'select'' 'these'' 'scopes'' 'for'' 'your'' '{%'' 'data'' 'variables.product.pat_generic'' '%}:
'' ''' ''' ''' ''' '`repo`
'' ''' ''' ''' ''' '`admin:org`
'' ''' ''' ''' ''' '`user`
'@'@'' '''
'-63,7'' '+65,7'' ''@'@'' 'For'' 'some'' 'example'' 'queries,'' 'see'' '"[An'' 'example'' 'query'' 'using'' 'the'' 'Enterprise'' 'Accounts'' 'A
'' ''' ''' ''' ''' '`manage_runners:enterprise`:'' 'Access'' 'to'' 'manage'' 'GitHub'' 'Actions'' 'enterprise'' 'runners'' 'and'' 'runner''
'-groups.{%'' 'endif'' '%}
'' ''' ''' ''' ''' '`read:enterprise`:'' 'Read'' 'enterprise'' 'profile'' 'data.3.'' 'Copy'' 'your'' 'personal'' 'access'' 'token'' 'and'' 'keep'' 'it'' 'in'' 'a'' 'secure'' 'place'' 'until'' 'you'' 'add'' 'it'' 'to'' 'your'' 'GraphQL'' 'client.
3.'' 'Copy'' 'your'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'and'' 'keep'' 'it'' 'in'' 'a'' 'secure'' 'place'' 'until'' 'you'' 'add'' 'it'' 'to'' 'your'' 'GraphQL'' 'client.###'' '2.'' 'Choose'' 'a'' 'GraphQL'' 'client'@'@'' '''
'-82,11'' '+84,11'' ''@'@'' 'The'' 'next'' 'steps'' 'will'' 'use'' 'Insomnia.
'' ''' ''' ''' ''' 'For'' 'your'' 'enterprise'' 'instance:'' '`https://<HOST>/api/graphql`
'' ''' ''' ''' ''' 'For'' 'GitHub'' 'Enterprise'' 'Cloud:'' '`https://api.github.com/graphql`2.'' 'To'' 'authenticate,'' 'open'' 'the'' 'authentication'' 'options'' 'menu'' 'and'' 'select'' '**Bearer'' 'token**.'' 'Next,'' 'add'' 'your'' 'personal'' 'access'' 'token'' 'that'' 'you'' 'copied'' 'earlier.
2.'' 'To'' 'authenticate,'' 'open'' 'the'' 'authentication'' 'options'' 'menu'' 'and'' 'select'' '**Bearer'' 'token**.'' 'Next,'' 'add'' 'your'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'that'' 'you'' 'copied'' 'earlier.'' '![Permissions'' 'options'' 'for'' 'personal'' 'access'' 'token](/assets/images/developer/graphql/insomnia''
'-base''
'-url''
'-and''
'-pat.png)
'' '![Permissions'' 'options'' 'for'' '{%'' 'data'' 'variables.product.pat_generic'' '%}](/assets/images/developer/graphql/insomnia''
'-base''
'-url''
'-and''
'-pat.png)'' '![Permissions'' 'options'' 'for'' 'personal'' 'access'' 'token](/assets/images/developer/graphql/insomnia''
'-bearer''
'-token''
'-option.png)
'' '![Permissions'' 'options'' 'for'' '{%'' 'data'' 'variables.product.pat_generic'' '%}](/assets/images/developer/graphql/insomnia''
'-bearer''
'-token''
'-option.png)3.'' 'Include'' 'header'' 'information.
'' ''' ''' ''' 'Add'' '`Content''
'-Type`'' 'as'' 'the'' 'header'' 'and'' '`application/json`'' 'as'' 'the'' 'value.
'' ''' '16'' ''' '
...king''
'-with''
'-projects/automating''
'-your''
'-project/automating''
'-projects''
'-using''
'-actions.md
'@'@'' '''
'-30,7'' '+30,7'' ''@'@'' 'You'' 'may'' 'also'' 'want'' 'to'' 'use'' 'the'' '**actions/add''
'-to''
'-project**'' 'workflow,'' 'which'' 'is'' 'maint{%'' 'note'' '%}**Note:**'' '`GITHUB_TOKEN`'' 'is'' 'scoped'' 'to'' 'the'' 'repository'' 'level'' 'and'' 'cannot'' 'access'' '{%'' 'data'' 'variables.projects.projects_v2'' '%}.'' 'To'' 'access'' '{%'' 'data'' 'variables.projects.projects_v2'' '%}'' 'you'' 'can'' 'either'' 'create'' 'a'' '{%'' 'data'' 'variables.product.prodname_github_app'' '%}'' '(recommended'' 'for'' 'organization'' 'projects)'' 'or'' 'a'' 'personal'' 'access'' 'token'' '(recommended'' 'for'' 'user'' 'projects).'' 'Workflow'' 'examples'' 'for'' 'both'' 'approaches'' 'are'' 'shown'' 'below.
**Note:**'' '`GITHUB_TOKEN`'' 'is'' 'scoped'' 'to'' 'the'' 'repository'' 'level'' 'and'' 'cannot'' 'access'' '{%'' 'data'' 'variables.projects.projects_v2'' '%}.'' 'To'' 'access'' '{%'' 'data'' 'variables.projects.projects_v2'' '%}'' 'you'' 'can'' 'either'' 'create'' 'a'' '{%'' 'data'' 'variables.product.prodname_github_app'' '%}'' '(recommended'' 'for'' 'organization'' 'projects)'' 'or'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' '(recommended'' 'for'' 'user'' 'projects).'' 'Workflow'' 'examples'' 'for'' 'both'' 'approaches'' 'are'' 'shown'' 'below.{%'' 'endnote'' '%}'@'@'' '''
'-167,10'' '+167,10'' ''@'@'' 'jobs:
Example'' 'workflow'' 'authenticating'' 'with'' 'a'' 'personal'' 'access'' 'token
Example'' 'workflow'' 'authenticating'' 'with'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}
Create'' 'a'' 'personal'' 'access'' 'token'' 'with'' 'the'' 'project'' 'and'' 'repo'' 'scopes.'' 'For'' 'more'' 'information,'' 'see'' '"Creating'' 'a'' 'personal'' 'access'' 'token."
Save'' 'the'' 'personal'' 'access'' 'token'' 'as'' 'a'' 'secret'' 'in'' 'your'' 'repository'' 'or'' 'organization.
Create'' 'a'' '{%'' 'data'' 'variables.product.pat_v1'' '%}'' 'with'' 'the'' 'project'' 'and'' 'repo'' 'scopes.'' 'For'' 'more'' 'information,'' 'see'' '"Creating'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}."
Save'' 'the'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'as'' 'a'' 'secret'' 'in'' 'your'' 'repository'' 'or'' 'organization.
In'' 'the'' 'following'' 'workflow,'' 'replace'' 'YOUR_TOKEN'' 'with'' 'the'' 'name'' 'of'' 'the'' 'secret.'' 'Replace'' 'YOUR_ORGANIZATION'' 'with'' 'the'' 'name'' 'of'' 'your'' 'organization.'' 'For'' 'example,'' 'octo''
'-org.'' 'Replace'' 'YOUR_PROJECT_NUMBER'' 'with'' 'your'' 'project'' 'number.'' 'To'' 'find'' 'the'' 'project'' 'number,'' 'look'' 'at'' 'the'' 'project'' 'URL.'' 'For'' 'example,'' 'https://github.com/orgs/octo''
'-org/projects/5'' 'has'' 'a'' 'project'' 'number'' 'of'' '5.
'@'@'' '''
'-339,7'' '+339,7'' ''@'@'' 'env:
'' ''' 'PROJECT_NUMBER:'' 'YOUR_PROJECT_NUMBER
Personal'' 'access'' 'token:'' '{%'' 'data'' 'variables.product.pat_generic_caps'' '%}:env:
'@'@'' '''
'-353,7'' '+353,7'' ''@'@'' 'env:
Sets'' 'environment'' 'variables'' 'for'' 'this'' 'step.
<br>
<br>
If'' 'you'' 'are'' 'using'' 'a'' 'personal'' 'access'' 'token,'' 'replace'' '<code>YOUR_TOKEN</code>'' 'with'' 'the'' 'name'' 'of'' 'the'' 'secret'' 'that'' 'contains'' 'your'' 'personal'' 'access'' 'token.
If'' 'you'' 'are'' 'using'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%},'' 'replace'' '<code>YOUR_TOKEN</code>'' 'with'' 'the'' 'name'' 'of'' 'the'' 'secret'' 'that'' 'contains'' 'your'' '{%'' 'data'' 'variables.product.pat_generic'' '%}.
<br>
<br>
Replace'' '<code>YOUR_ORGANIZATION</code>'' 'with'' 'the'' 'name'' 'of'' 'your'' 'organization.'' 'For'' 'example,'' '<code>octo''
'-org</code>.
'@'@'' '''
'-433,7'' '+433,7'' ''@'@'' 'env:
'' ''' 'PR_ID:'' '{%'' 'raw'' '%}${{'' 'github.event.pull_request.node_id'' '}}{%'' 'endraw'' '%}
Personal'' 'access'' 'token:'' '{%'' 'data'' 'variables.product.pat_generic_caps'' '%}:env:
'@'@'' '''
'-504,7'' '+504,7'' ''@'@'' 'env:
'' ''' 'GITHUB_TOKEN:'' '{%'' 'raw'' '%}${{'' 'steps.generate_token.outputs.token'' '}}{%'' 'endraw'' '%}
Personal'' 'access'' 'token:'' '{%'' 'data'' 'variables.product.pat_generic_caps'' '%}:env:
'' ''' '2'' ''' '
...cking''
'-with''
'-projects/automating''
'-your''
'-project/using''
'-the''
'-api''
'-to''
'-manage''
'-projects.md
'@'@'' '''
'-21,7'' '+21,7'' ''@'@'' 'This'' 'article'' 'demonstrates'' 'how'' 'to'' 'use'' 'the'' 'GraphQL'' 'API'' 'to'' 'manage'' 'a'' 'project.'' 'For'' 'mo{%'' 'curl'' '%}In'' 'all'' 'of'' 'the'' 'following'' 'cURL'' 'examples,'' 'replace'' '`TOKEN`'' 'with'' 'a'' 'token'' 'that'' 'has'' 'the'' '`read:project`'' 'scope'' '(for'' 'queries)'' 'or'' '`project`'' 'scope'' '(for'' 'queries'' 'and'' 'mutations).'' 'The'' 'token'' 'can'' 'be'' 'a'' 'personal'' 'access'' 'token'' 'for'' 'a'' 'user'' 'or'' 'an'' 'installation'' 'access'' 'token'' 'for'' 'a'' '{%'' 'data'' 'variables.product.prodname_github_app'' '%}.'' 'For'' 'more'' 'information'' 'about'' 'creating'' 'a'' 'personal'' 'access'' 'token,'' 'see'' '"[Creating'' 'a'' 'personal'' 'access'' 'token](/github/authenticating''
'-to''
'-github/keeping''
'-your''
'-account''
'-and''
'-data''
'-secure/creating''
'-a''
'-personal''
'-access''
'-token)."'' 'For'' 'more'' 'information'' 'about'' 'creating'' 'an'' 'installation'' 'access'' 'token'' 'for'' 'a'' '{%'' 'data'' 'variables.product.prodname_github_app'' '%},'' 'see'' '"[Authenticating'' 'with'' '{%'' 'data'' 'variables.product.prodname_github_apps'' '%}](/developers/apps/building''
'-github''
'-apps/authenticating''
'-with''
'-github''
'-apps#authenticating''
'-as''
'-a''
'-github''
'-app)."
In'' 'all'' 'of'' 'the'' 'following'' 'cURL'' 'examples,'' 'replace'' '`TOKEN`'' 'with'' 'a'' 'token'' 'that'' 'has'' 'the'' '`read:project`'' 'scope'' '(for'' 'queries)'' 'or'' '`project`'' 'scope'' '(for'' 'queries'' 'and'' 'mutations).'' 'The'' 'token'' 'can'' 'be'' 'a'' '{%'' 'data'' 'variables.product.pat_v1'' '%}'' 'for'' 'a'' 'user'' 'or'' 'an'' 'installation'' 'access'' 'token'' 'for'' 'a'' '{%'' 'data'' 'variables.product.prodname_github_app'' '%}.'' 'For'' 'more'' 'information'' 'about'' 'creating'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%},'' 'see'' '"[Creating'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}](/github/authenticating''
'-to''
'-github/keeping''
'-your''
'-account''
'-and''
'-data''
'-secure/creating''
'-a''
'-personal''
'-access''
'-token)."'' 'For'' 'more'' 'information'' 'about'' 'creating'' 'an'' 'installation'' 'access'' 'token'' 'for'' 'a'' '{%'' 'data'' 'variables.product.prodname_github_app'' '%},'' 'see'' '"[Authenticating'' 'with'' '{%'' 'data'' 'variables.product.prodname_github_apps'' '%}](/developers/apps/building''
'-github''
'-apps/authenticating''
'-with''
'-github''
'-apps#authenticating''
'-as''
'-a''
'-github''
'-app)."{%'' 'endcurl'' '%}'' ''' '2'' ''' '
...ngle''
'-sign''
'-on/viewing''
'-and''
'-managing''
'-a''
'-members''
'-saml''
'-access''
'-to''
'-your''
'-organization.md
'@'@'' '''
'-16,7'' '+16,7'' ''@'@'' 'shortTitle:'' 'Manage'' 'SAML'' 'access##'' 'About'' 'SAML'' 'access'' 'to'' 'your'' 'organizationWhen'' 'you'' 'enable'' 'SAML'' 'single'' 'sign''
'-on'' 'for'' 'your'' 'organization,'' 'each'' 'organization'' 'member'' 'can'' 'link'' 'their'' 'external'' 'identity'' 'on'' 'your'' 'identity'' 'provider'' '(IdP)'' 'to'' 'their'' 'existing'' 'account'' 'on'' '{%'' 'data'' 'variables.location.product_location'' '%}.'' 'To'' 'access'' 'your'' 'organization's'' 'resources'' 'on'' '{%'' 'data'' 'variables.product.product_name'' '%},'' 'the'' 'member'' 'must'' 'have'' 'an'' 'active'' 'SAML'' 'session'' 'in'' 'their'' 'browser.'' 'To'' 'access'' 'your'' 'organization's'' 'resources'' 'using'' 'the'' 'API'' 'or'' 'Git,'' 'the'' 'member'' 'must'' 'use'' 'a'' 'personal'' 'access'' 'token'' 'or'' 'SSH'' 'key'' 'that'' 'the'' 'member'' 'has'' 'authorized'' 'for'' 'use'' 'with'' 'your'' 'organization.
When'' 'you'' 'enable'' 'SAML'' 'single'' 'sign''
'-on'' 'for'' 'your'' 'organization,'' 'each'' 'organization'' 'member'' 'can'' 'link'' 'their'' 'external'' 'identity'' 'on'' 'your'' 'identity'' 'provider'' '(IdP)'' 'to'' 'their'' 'existing'' 'account'' 'on'' '{%'' 'data'' 'variables.location.product_location'' '%}.'' 'To'' 'access'' 'your'' 'organization's'' 'resources'' 'on'' '{%'' 'data'' 'variables.product.product_name'' '%},'' 'the'' 'member'' 'must'' 'have'' 'an'' 'active'' 'SAML'' 'session'' 'in'' 'their'' 'browser.'' 'To'' 'access'' 'your'' 'organization's'' 'resources'' 'using'' 'the'' 'API'' 'or'' 'Git,'' 'the'' 'member'' 'must'' 'use'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'or'' 'SSH'' 'key'' 'that'' 'the'' 'member'' 'has'' 'authorized'' 'for'' 'use'' 'with'' 'your'' 'organization.You'' 'can'' 'view'' 'and'' 'revoke'' 'each'' 'member's'' 'linked'' 'identity,'' 'active'' 'sessions,'' 'and'' 'authorized'' 'credentials'' 'on'' 'the'' 'same'' 'page.'' ''' '6'' ''' '
content/organizations/index.md
'@'@'' '''
'-39,11'' '+39,11'' ''@'@'' 'children:
'' ''' ''' '/managing''
'-peoples''
'-access''
'-to''
'-your''
'-organization''
'-with''
'-roles
'' ''' ''' '/organizing''
'-members''
'-into''
'-teams
'' ''' ''' '/collaborating''
'-with''
'-your''
'-team
'' ''' ''' '/managing''
'-access''
'-to''
'-your''
'-organizations''
'-repositories
'' ''' ''' '/managing''
'-user''
'-access''
'-to''
'-your''
'-organizations''
'-repositories
'' ''' ''' '/managing''
'-access''
'-to''
'-your''
'-organizations''
'-project''
'-boards
'' ''' ''' '/managing''
'-access''
'-to''
'-your''
'-organizations''
'-apps
'' ''' ''' '/managing''
'-programmatic''
'-access''
'-to''
'-your''
'-organization
'' ''' ''' '/managing''
'-organization''
'-settings
'' ''' ''' '/restricting''
'-access''
'-to''
'-your''
'-organizations''
'-data
'' ''' ''' '/managing''
'-oauth''
'-access''
'-to''
'-your''
'-organizations''
'-data
'' ''' ''' '/keeping''
'-your''
'-organization''
'-secure
'' ''' ''' '/managing''
'-saml''
'-single''
'-sign''
'-on''
'-for''
'-your''
'-organization
'' ''' ''' '/granting''
'-access''
'-to''
'-your''
'-organization''
'-with''
'-saml''
'-single''
'-sign''
'-on
'' ''' '1'' ''' '
...r''
'-organization''
'-secure/managing''
'-security''
'-settings''
'-for''
'-your''
'-organization/index.md
'@'@'' '''
'-16,6'' '+16,5'' ''@'@'' 'children:
'' ''' ''' '/restricting''
'-email''
'-notifications''
'-for''
'-your''
'-organization
'' ''' ''' '/reviewing''
'-the''
'-audit''
'-log''
'-for''
'-your''
'-organization
'' ''' ''' '/accessing''
'-compliance''
'-reports''
'-for''
'-your''
'-organization
'' ''' ''' '/reviewing''
'-your''
'-organizations''
'-installed''
'-integrations
'' ''' '27'' ''' '
...settings''
'-for''
'-your''
'-organization/reviewing''
'-the''
'-audit''
'-log''
'-for''
'-your''
'-organization.md
'@'@'' '''
'-39,6'' '+39,7'' ''@'@'' 'To'' 'search'' 'for'' 'specific'' 'events,'' 'use'' 'the'' '`action`'' 'qualifier'' 'in'' 'your'' 'query.'' 'Actions
|''
'-|''
'-{%'' 'ifversion'' 'fpt'' 'or'' 'ghec'' '%}
|'' '[`account`](#account''
'-category''
'-actions)'' '|'' 'Contains'' 'all'' 'activities'' 'related'' 'to'' 'your'' 'organization'' 'account.
|'' '[`advisory_credit`](#advisory_credit''
'-category''
'-actions)'' '|'' 'Contains'' 'all'' 'activities'' 'related'' 'to'' 'crediting'' 'a'' 'contributor'' 'for'' 'a'' 'security'' 'advisory'' 'in'' 'the'' '{%'' 'data'' 'variables.product.prodname_advisory_database'' '%}.'' 'For'' 'more'' 'information,'' 'see'' '"[About'' '{%'' 'data'' 'variables.product.prodname_dotcom'' '%}'' 'Security'' 'Advisories](/github/managing''
'-security''
'-vulnerabilities/about''
'-github''
'-security''
'-advisories)."
|'' '[`auto_approve_personal_access_token_requests`](#auto_approve_personal_access_token_requests''
'-category''
'-actions)'' '|'' 'Contains'' 'activities'' 'related'' 'to'' 'your'' 'organization's'' 'approval'' 'policy'' 'for'' '{%'' 'data'' 'variables.product.pat_v2'' '%}s.'' 'For'' 'more'' 'information,'' 'see'' '"[Setting'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'policy'' 'for'' 'your'' 'organization](/organizations/managing''
'-programmatic''
'-access''
'-to''
'-your''
'-organization/setting''
'-a''
'-personal''
'-access''
'-token''
'-policy''
'-for''
'-your''
'-organization)."
|'' '[`billing`](#billing''
'-category''
'-actions)'' '|'' 'Contains'' 'all'' 'activities'' 'related'' 'to'' 'your'' 'organization's'' 'billing.
|'' '[`business`](#business''
'-category''
'-actions)'' '|'' 'Contains'' 'activities'' 'related'' 'to'' 'business'' 'settings'' 'for'' 'an'' 'enterprise.'' '|
|'' '[`codespaces`](#codespaces''
'-category''
'-actions)'' '|'' 'Contains'' 'all'' 'activities'' 'related'' 'to'' 'your'' 'organization's'' 'codespaces.'' '|{%'' 'endif'' '%}{%'' 'ifversion'' 'fpt'' 'or'' 'ghec'' 'or'' 'ghes'' '>'' '3.2'' 'or'' 'ghae'' '%}
'@'@'' '''
'-67,6'' '+68,7'' ''@'@'' 'To'' 'search'' 'for'' 'specific'' 'events,'' 'use'' 'the'' '`action`'' 'qualifier'' 'in'' 'your'' 'query.'' 'Actions
|'' '[`oauth_application`](#oauth_application''
'-category''
'-actions)'' '|'' 'Contains'' 'all'' 'activities'' 'related'' 'to'' 'OAuth'' 'Apps.
|'' '[`packages`](#packages''
'-category''
'-actions)'' '|'' 'Contains'' 'all'' 'activities'' 'related'' 'to'' '{%'' 'data'' 'variables.product.prodname_registry'' '%}.{%'' 'ifversion'' 'fpt'' 'or'' 'ghec'' '%}
|'' '[`payment_method`](#payment_method''
'-category''
'-actions)'' '|'' 'Contains'' 'all'' 'activities'' 'related'' 'to'' 'how'' 'your'' 'organization'' 'pays'' 'for'' 'GitHub.{%'' 'endif'' '%}
|'' '[`personal_access_token`](#personal_access_token''
'-category''
'-actions)'' '|'' 'Contains'' 'activities'' 'related'' 'to'' '{%'' 'data'' 'variables.product.pat_v2'' '%}s'' 'in'' 'your'' 'organization.'' 'For'' 'more'' 'information,'' 'see'' '"[Creating'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}](/authentication/keeping''
'-your''
'-account''
'-and''
'-data''
'-secure/creating''
'-a''
'-personal''
'-access''
'-token)."
|'' '[`profile_picture`](#profile_picture''
'-category''
'-actions)'' '|'' 'Contains'' 'all'' 'activities'' 'related'' 'to'' 'your'' 'organization's'' 'profile'' 'picture.
|'' '[`project`](#project''
'-category''
'-actions)'' '|'' 'Contains'' 'all'' 'activities'' 'related'' 'to'' 'project'' 'boards.
|'' '[`protected_branch`](#protected_branch''
'-category''
'-actions)'' '|'' 'Contains'' 'all'' 'activities'' 'related'' 'to'' 'protected'' 'branches.
'@'@'' '''
'-209,6'' '+211,17'' ''@'@'' 'An'' 'overview'' 'of'' 'some'' 'of'' 'the'' 'most'' 'common'' 'actions'' 'that'' 'are'' 'recorded'' 'as'' 'events'' 'in'' 'th
|'' '`destroy`'' '|'' 'Triggered'' 'when'' 'the'' 'administrator'' 'of'' 'a'' 'security'' 'advisory'' 'removes'' 'someone'' 'from'' 'the'' 'credit'' 'section.
{%'' 'endif'' '%}{%'' 'ifversion'' 'pat''
'-v2'' '%}###'' '`auto_approve_personal_access_token_requests`'' 'category'' 'actions|'' 'Action'' '|'' 'Description
|''
'-|''
'-
|'' '`disable`'' '|'' 'Triggered'' 'when'' 'the'' 'organization'' 'must'' 'approve'' '{%'' 'data'' 'variables.product.pat_v2'' '%}s'' 'before'' 'the'' 'tokens'' 'can'' 'access'' 'organization'' 'resources.'' 'For'' 'more'' 'information,'' 'see'' '"[Setting'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'policy'' 'for'' 'your'' 'organization](/organizations/managing''
'-programmatic''
'-access''
'-to''
'-your''
'-organization/setting''
'-a''
'-personal''
'-access''
'-token''
'-policy''
'-for''
'-your''
'-organization)."
|'' '`enable`'' '|'' 'Triggered'' 'when'' '{%'' 'data'' 'variables.product.pat_v2'' '%}s'' 'can'' 'access'' 'organization'' 'resources'' 'without'' 'prior'' 'approval.'' 'For'' 'more'' 'information,'' 'see'' '"[Setting'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'policy'' 'for'' 'your'' 'organization](/organizations/managing''
'-programmatic''
'-access''
'-to''
'-your''
'-organization/setting''
'-a''
'-personal''
'-access''
'-token''
'-policy''
'-for''
'-your''
'-organization)."{%'' 'endif'' '%}{%'' 'ifversion'' 'fpt'' 'or'' 'ghec'' '%}
###'' '`billing`'' 'category'' 'actions'@'@'' '''
'-555,6'' '+568,20'' ''@'@'' 'For'' 'more'' 'information,'' 'see'' '"[Managing'' 'the'' 'publication'' 'of'' '{%'' 'data'' 'variables.produc{%'' 'endif'' '%}{%'' 'ifversion'' 'pat''
'-v2'' '%}###'' '`personal_access_token`'' 'category'' 'actions|'' 'Action'' '|'' 'Description
|''
'-|''
'-
|'' '`access_granted`'' '|'' 'Triggered'' 'when'' 'a'' '{%'' 'data'' 'variables.product.pat_v2'' '%}'' 'is'' 'granted'' 'access'' 'to'' 'organization'' 'resources.'' 'For'' 'more'' 'information,'' 'see'' '"[Managing'' 'requests'' 'for'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'in'' 'your'' 'organization](/organizations/managing''
'-programmatic''
'-access''
'-to''
'-your''
'-organization/managing''
'-requests''
'-for''
'-personal''
'-access''
'-tokens''
'-in''
'-your''
'-organization)."
|'' '`access_revoked`'' '|'' 'Triggered'' 'when'' 'access'' 'to'' 'organization'' 'resources'' 'by'' 'a'' '{%'' 'data'' 'variables.product.pat_v2'' '%}'' 'is'' 'revoked.'' 'The'' 'token'' 'can'' 'still'' 'read'' 'public'' 'organization'' 'resources.'' 'For'' 'more'' 'information,'' 'see'' '"[Reviewing'' 'and'' 'revoking'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'in'' 'your'' 'organization](/organizations/managing''
'-programmatic''
'-access''
'-to''
'-your''
'-organization/reviewing''
'-and''
'-revoking''
'-personal''
'-access''
'-tokens''
'-in''
'-your''
'-organization)."
|'' '`request_cancelled`'' '|'' 'Triggered'' 'when'' 'a'' 'member'' 'of'' 'the'' 'organization'' 'cancels'' 'a'' 'request'' 'for'' 'their'' '{%'' 'data'' 'variables.product.pat_v2'' '%}'' 'to'' 'access'' 'organization'' 'resources.
|'' '`request_created`'' '|'' 'Triggered'' 'when'' 'a'' 'member'' 'of'' 'the'' 'organization'' 'creates'' 'a'' '{%'' 'data'' 'variables.product.pat_v2'' '%}'' 'to'' 'access'' 'organization'' 'resources'' 'and'' 'the'' 'organization'' 'requires'' 'approval'' 'before'' 'a'' '{%'' 'data'' 'variables.product.pat_v2'' '%}'' 'can'' 'access'' 'organization'' 'resources.'' 'For'' 'more'' 'information,'' 'see'' '"[Managing'' 'requests'' 'for'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'in'' 'your'' 'organization](/organizations/managing''
'-programmatic''
'-access''
'-to''
'-your''
'-organization/managing''
'-requests''
'-for''
'-personal''
'-access''
'-tokens''
'-in''
'-your''
'-organization)."
|'' '`request_denied`'' '|'' 'Triggered'' 'when'' 'a'' 'request'' 'for'' 'a'' '{%'' 'data'' 'variables.product.pat_v2'' '%}'' 'to'' 'access'' 'organization'' 'resources'' 'is'' 'denied.'' 'For'' 'more'' 'information,'' 'see'' '"[Managing'' 'requests'' 'for'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'in'' 'your'' 'organization](/organizations/managing''
'-programmatic''
'-access''
'-to''
'-your''
'-organization/managing''
'-requests''
'-for''
'-personal''
'-access''
'-tokens''
'-in''
'-your''
'-organization)."{%'' 'endif'' '%}###'' '`profile_picture`'' 'category'' 'actions
|'' 'Action'' '|'' 'Description
|''
'-|''
'-
'' '21'' ''' '
content/organizations/managing''
'-access''
'-to''
'-your''
'-organizations''
'-apps/index.md
This'' 'file'' 'was'' 'deleted.'' ''' '2'' ''' '
...''
'-access''
'-to''
'-your''
'-organizations''
'-repositories/about''
'-ssh''
'-certificate''
'-authorities.md
'@'@'' '''
'-25,7'' '+25,7'' ''@'@'' 'After'' 'you'' 'add'' 'an'' 'SSH'' 'CA'' 'to'' 'your'' 'organization'' 'or'' 'enterprise'' 'account,'' 'you'' 'can'' 'use
For'' 'example,'' 'you'' 'can'' 'build'' 'an'' 'internal'' 'system'' 'that'' 'issues'' 'a'' 'new'' 'certificate'' 'to'' 'your'' 'developers'' 'every'' 'morning.'' 'Each'' 'developer'' 'can'' 'use'' 'their'' 'daily'' 'certificate'' 'to'' 'work'' 'on'' 'your'' 'organization's'' 'repositories'' 'on'' '{%'' 'data'' 'variables.product.product_name'' '%}.'' 'At'' 'the'' 'end'' 'of'' 'the'' 'day,'' 'the'' 'certificate'' 'can'' 'automatically'' 'expire,'' 'protecting'' 'your'' 'repositories'' 'if'' 'the'' 'certificate'' 'is'' 'later'' 'compromised.{%'' 'ifversion'' 'ghec'' '%}
Organization'' 'members'' 'can'' 'use'' 'their'' 'signed'' 'certificates'' 'for'' 'authentication'' 'even'' 'if'' 'you've'' 'enforced'' 'SAML'' 'single'' 'sign''
'-on.'' 'Unless'' 'you'' 'make'' 'SSH'' 'certificates'' 'a'' 'requirement,'' 'organization'' 'members'' 'can'' 'continue'' 'to'' 'use'' 'other'' 'means'' 'of'' 'authentication'' 'to'' 'access'' 'your'' 'organization's'' 'resources'' 'with'' 'Git,'' 'including'' 'their'' 'username'' 'and'' 'password,'' 'personal'' 'access'' 'tokens,'' 'and'' 'their'' 'own'' 'SSH'' 'keys.
Organization'' 'members'' 'can'' 'use'' 'their'' 'signed'' 'certificates'' 'for'' 'authentication'' 'even'' 'if'' 'you've'' 'enforced'' 'SAML'' 'single'' 'sign''
'-on.'' 'Unless'' 'you'' 'make'' 'SSH'' 'certificates'' 'a'' 'requirement,'' 'organization'' 'members'' 'can'' 'continue'' 'to'' 'use'' 'other'' 'means'' 'of'' 'authentication'' 'to'' 'access'' 'your'' 'organization's'' 'resources'' 'with'' 'Git,'' 'including'' 'their'' 'username'' 'and'' 'password,'' '{%'' 'data'' 'variables.product.pat_generic'' '%}s,'' 'and'' 'their'' 'own'' 'SSH'' 'keys.
{%'' 'endif'' '%}Members'' 'will'' 'not'' 'be'' 'able'' 'to'' 'use'' 'their'' 'certificates'' 'to'' 'access'' 'forks'' 'of'' 'your'' 'repositories'' 'that'' 'are'' 'owned'' 'by'' 'their'' 'personal'' 'accounts.'' '
'' ''' '1'' ''' '
...ta/about''
'-oauth''
'-app''
'-access''
'-restrictions.md'' '???'' '...ta/about''
'-oauth''
'-app''
'-access''
'-restrictions.md
'@'@'' '''
'-5,6'' '+5,7'' ''@'@'' 'redirect_from:
'' ''' ''' '/articles/about''
'-third''
'-party''
'-application''
'-restrictions
'' ''' ''' '/articles/about''
'-oauth''
'-app''
'-access''
'-restrictions
'' ''' ''' '/github/setting''
'-up''
'-and''
'-managing''
'-organizations''
'-and''
'-teams/about''
'-oauth''
'-app''
'-access''
'-restrictions
'' ''' ''' '/organizations/restricting''
'-access''
'-to''
'-your''
'-organizations''
'-data/about''
'-oauth''
'-app''
'-access''
'-restrictions
versions:
'' ''' 'fpt:'' ''*'
'' ''' 'ghec:'' ''*'
'' ''' '1'' ''' '
...oving''
'-oauth''
'-apps''
'-for''
'-your''
'-organization.md'' '???'' '...oving''
'-oauth''
'-apps''
'-for''
'-your''
'-organization.md
'@'@'' '''
'-5,6'' '+5,7'' ''@'@'' 'redirect_from:
'' ''' ''' '/articles/approving''
'-third''
'-party''
'-applications''
'-for''
'-your''
'-organization
'' ''' ''' '/articles/approving''
'-oauth''
'-apps''
'-for''
'-your''
'-organization
'' ''' ''' '/github/setting''
'-up''
'-and''
'-managing''
'-organizations''
'-and''
'-teams/approving''
'-oauth''
'-apps''
'-for''
'-your''
'-organization
'' ''' ''' '/organizations/restricting''
'-access''
'-to''
'-your''
'-organizations''
'-data/approving''
'-oauth''
'-apps''
'-for''
'-your''
'-organization
versions:
'' ''' 'fpt:'' ''*'
'' ''' 'ghec:'' ''*'
'' ''' '1'' ''' '
...proved''
'-oauth''
'-app''
'-for''
'-your''
'-organization.md'' '???'' '...proved''
'-oauth''
'-app''
'-for''
'-your''
'-organization.md
'@'@'' '''
'-5,6'' '+5,7'' ''@'@'' 'redirect_from:
'' ''' ''' '/articles/denying''
'-access''
'-to''
'-a''
'-previously''
'-approved''
'-application''
'-for''
'-your''
'-organization
'' ''' ''' '/articles/denying''
'-access''
'-to''
'-a''
'-previously''
'-approved''
'-oauth''
'-app''
'-for''
'-your''
'-organization
'' ''' ''' '/github/setting''
'-up''
'-and''
'-managing''
'-organizations''
'-and''
'-teams/denying''
'-access''
'-to''
'-a''
'-previously''
'-approved''
'-oauth''
'-app''
'-for''
'-your''
'-organization
'' ''' ''' '/organizations/restricting''
'-access''
'-to''
'-your''
'-organizations''
'-data/denying''
'-access''
'-to''
'-a''
'-previously''
'-approved''
'-oauth''
'-app''
'-for''
'-your''
'-organization
versions:
'' ''' 'fpt:'' ''*'
'' ''' 'ghec:'' ''*'
'' ''' '1'' ''' '
...ess''
'-restrictions''
'-for''
'-your''
'-organization.md'' '???'' '...ess''
'-restrictions''
'-for''
'-your''
'-organization.md
'@'@'' '''
'-5,6'' '+5,7'' ''@'@'' 'redirect_from:
'' ''' ''' '/articles/disabling''
'-third''
'-party''
'-application''
'-restrictions''
'-for''
'-your''
'-organization
'' ''' ''' '/articles/disabling''
'-oauth''
'-app''
'-access''
'-restrictions''
'-for''
'-your''
'-organization
'' ''' ''' '/github/setting''
'-up''
'-and''
'-managing''
'-organizations''
'-and''
'-teams/disabling''
'-oauth''
'-app''
'-access''
'-restrictions''
'-for''
'-your''
'-organization
'' ''' ''' '/organizations/restricting''
'-access''
'-to''
'-your''
'-organizations''
'-data/disabling''
'-oauth''
'-app''
'-access''
'-restrictions''
'-for''
'-your''
'-organization
versions:
'' ''' 'fpt:'' ''*'
'' ''' 'ghec:'' ''*'
'' ''' '1'' ''' '
...ess''
'-restrictions''
'-for''
'-your''
'-organization.md'' '???'' '...ess''
'-restrictions''
'-for''
'-your''
'-organization.md
'@'@'' '''
'-5,6'' '+5,7'' ''@'@'' 'redirect_from:
'' ''' ''' '/articles/enabling''
'-third''
'-party''
'-application''
'-restrictions''
'-for''
'-your''
'-organization
'' ''' ''' '/articles/enabling''
'-oauth''
'-app''
'-access''
'-restrictions''
'-for''
'-your''
'-organization
'' ''' ''' '/github/setting''
'-up''
'-and''
'-managing''
'-organizations''
'-and''
'-teams/enabling''
'-oauth''
'-app''
'-access''
'-restrictions''
'-for''
'-your''
'-organization
'' ''' ''' '/organizations/restricting''
'-access''
'-to''
'-your''
'-organizations''
'-data/enabling''
'-oauth''
'-app''
'-access''
'-restrictions''
'-for''
'-your''
'-organization
versions:
'' ''' 'fpt:'' ''*'
'' ''' 'ghec:'' ''*'
'' ''' '5'' ''' '
...ccess''
'-to''
'-your''
'-organizations''
'-data/index.md'' '???'' '...ccess''
'-to''
'-your''
'-organizations''
'-data/index.md
'@'@'' '''
'-1,10'' '+1,11'' ''@'@
''
'-
title:'' 'Restricting'' 'access'' 'to'' 'your'' 'organization's'' 'data
title:'' 'Managing'' 'OAuth'' 'access'' 'to'' 'your'' 'organization's'' 'data
intro:'' ''{%'' 'data'' 'variables.product.prodname_oauth_app'' '%}'' 'access'' 'restrictions'' 'allow'' 'organization'' 'owners'' 'to'' 'restrict'' 'an'' 'untrusted'' 'app''s'' 'access'' 'to'' 'the'' 'organization''s'' 'data.'' 'Organization'' 'members'' 'can'' 'then'' 'use'' '{%'' 'data'' 'variables.product.prodname_oauth_apps'' '%}'' 'for'' 'their'' 'personal'' 'accounts'' 'while'' 'keeping'' 'organization'' 'data'' 'safe.'
redirect_from:
'' ''' ''' '/articles/restricting''
'-access''
'-to''
'-your''
'-organization''
'-s''
'-data
'' ''' ''' '/articles/restricting''
'-access''
'-to''
'-your''
'-organizations''
'-data
'' ''' ''' '/github/setting''
'-up''
'-and''
'-managing''
'-organizations''
'-and''
'-teams/restricting''
'-access''
'-to''
'-your''
'-organizations''
'-data
'' ''' ''' '/organizations/restricting''
'-access''
'-to''
'-your''
'-organizations''
'-data
versions:
'' ''' 'fpt:'' ''*'
'' ''' 'ghec:'' ''*'
'@'@'' '''
'-17,6'' '+18,6'' ''@'@'' 'children:
'' ''' ''' '/disabling''
'-oauth''
'-app''
'-access''
'-restrictions''
'-for''
'-your''
'-organization
'' ''' ''' '/approving''
'-oauth''
'-apps''
'-for''
'-your''
'-organization
'' ''' ''' '/denying''
'-access''
'-to''
'-a''
'-previously''
'-approved''
'-oauth''
'-app''
'-for''
'-your''
'-organization
shortTitle:'' 'Restrict'' 'access'' 'to'' 'organization'' 'data
shortTitle:'' 'Manage'' 'OAuth'' 'access
'' ''' '1'' ''' '
...thub''
'-app''
'-managers''
'-in''
'-your''
'-organization.md'' '???'' '...thub''
'-app''
'-managers''
'-in''
'-your''
'-organization.md
'@'@'' '''
'-4,6'' '+4,7'' ''@'@'' 'intro:'' ''Organization'' 'owners'' 'can'' 'grant'' 'users'' 'the'' 'ability'' 'to'' 'manage'' 'some'' 'or'' 'all'' '{%
redirect_from:
'' ''' ''' '/articles/adding''
'-github''
'-app''
'-managers''
'-in''
'-your''
'-organization
'' ''' ''' '/github/setting''
'-up''
'-and''
'-managing''
'-organizations''
'-and''
'-teams/adding''
'-github''
'-app''
'-managers''
'-in''
'-your''
'-organization
'' ''' ''' '/organizations/managing''
'-access''
'-to''
'-your''
'-organizations''
'-apps/adding''
'-github''
'-app''
'-managers''
'-in''
'-your''
'-organization
versions:
'' ''' 'fpt:'' ''*'
'' ''' 'ghes:'' ''*'
'' '26'' ''' '
content/organizations/managing''
'-programmatic''
'-access''
'-to''
'-your''
'-organization/index.md
'@'@'' '''
'-0,0'' '+1,26'' ''@'@
''
'-
title:'' 'Managing'' 'programmatic'' 'access'' 'to'' 'your'' 'organization
intro:'' ''As'' 'an'' 'organization'' 'owner,'' 'you'' 'can'' 'control'' 'access'' 'by'' 'apps'' 'and'' '{%'' 'data'' 'variables.product.pat_generic'' '%}s'' 'to'' 'your'' 'organization.'
redirect_from:
'' ''' ''' '/articles/managing''
'-access''
'-to''
'-your''
'-organization''
'-s''
'-apps
'' ''' ''' '/articles/managing''
'-access''
'-to''
'-your''
'-organizations''
'-apps
'' ''' ''' '/github/setting''
'-up''
'-and''
'-managing''
'-organizations''
'-and''
'-teams/managing''
'-access''
'-to''
'-your''
'-organizations''
'-apps
'' ''' ''' '/organizations/managing''
'-access''
'-to''
'-your''
'-organizations''
'-apps
versions:
'' ''' 'fpt:'' ''*'
'' ''' 'ghes:'' ''*'
'' ''' 'ghae:'' ''*'
'' ''' 'ghec:'' ''*'
topics:
'' ''' ''' 'Organizations
'' ''' ''' 'Teams
children:
'' ''' ''' '/adding''
'-github''
'-app''
'-managers''
'-in''
'-your''
'-organization
'' ''' ''' '/removing''
'-github''
'-app''
'-managers''
'-from''
'-your''
'-organization
'' ''' ''' '/reviewing''
'-your''
'-organizations''
'-installed''
'-integrations
'' ''' ''' '/setting''
'-a''
'-personal''
'-access''
'-token''
'-policy''
'-for''
'-your''
'-organization
'' ''' ''' '/managing''
'-requests''
'-for''
'-personal''
'-access''
'-tokens''
'-in''
'-your''
'-organization
'' ''' ''' '/reviewing''
'-and''
'-revoking''
'-personal''
'-access''
'-tokens''
'-in''
'-your''
'-organization
shortTitle:'' 'Manage'' 'programmatic'' 'access
'' '40'' ''' '
...ganization/managing''
'-requests''
'-for''
'-personal''
'-access''
'-tokens''
'-in''
'-your''
'-organization.md
'@'@'' '''
'-0,0'' '+1,40'' ''@'@
''
'-
title:'' 'Managing'' 'requests'' 'for'' 'personal'' 'access'' 'tokens'' 'in'' 'your'' 'organization
intro:'' 'Organization'' 'owners'' 'can'' 'approve'' 'or'' 'deny'' '{%'' 'data'' 'variables.product.pat_v2'' '%}s'' 'that'' 'request'' 'access'' 'to'' 'their'' 'organization.
versions:
'' ''' 'feature:'' 'pat''
'-v2
shortTitle:'' 'Manage'' 'token'' 'requests
''
'-{%'' 'data'' 'reusables.user''
'-settings.pat''
'-v2''
'-org''
'-opt''
'-in'' '%}##'' 'About'' '{%'' 'data'' 'variables.product.pat_v2'' '%}'' 'requestsWhen'' 'organization'' 'members'' 'create'' 'a'' '{%'' 'data'' 'variables.product.pat_v2'' '%}'' 'to'' 'access'' 'resources'' 'owned'' 'by'' 'the'' 'organization,'' 'if'' 'the'' 'organization'' 'requires'' 'approval'' 'for'' '{%'' 'data'' 'variables.product.pat_v2'' '%}s,'' 'then'' 'an'' 'organization'' 'owner'' 'must'' 'approve'' 'the'' 'token'' 'before'' 'it'' 'can'' 'be'' 'used'' 'to'' 'access'' 'any'' 'resources'' 'that'' 'are'' 'not'' 'public.'' 'For'' 'more'' 'information,'' 'see'' '"[Setting'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'policy'' 'for'' 'your'' 'organization](/organizations/managing''
'-programmatic''
'-access''
'-to''
'-your''
'-organization/setting''
'-a''
'-personal''
'-access''
'-token''
'-policy''
'-for''
'-your''
'-organization)."{%'' 'data'' 'variables.product.company_short'' '%}'' 'will'' 'notify'' 'organization'' 'owners'' 'with'' 'a'' 'daily'' 'email'' 'about'' 'all'' '{%'' 'data'' 'variables.product.pat_v2'' '%}s'' 'that'' 'are'' 'awaiting'' 'approval.'' 'When'' 'a'' 'token'' 'is'' 'denied'' 'or'' 'approved,'' 'the'' 'user'' 'who'' 'created'' 'the'' 'token'' 'will'' 'receive'' 'an'' 'email'' 'notification.{%'' 'note'' '%}**Note**:'' 'Only'' '{%'' 'data'' 'variables.product.pat_v2'' '%}s,'' 'not'' '{%'' 'data'' 'variables.product.pat_v1_plural'' '%},'' 'are'' 'subject'' 'to'' 'approval.'' 'Unless'' 'the'' 'organization'' 'has'' 'restricted'' 'access'' 'by'' '{%'' 'data'' 'variables.product.pat_v1_plural'' '%},'' 'any'' '{%'' 'data'' 'variables.product.pat_v1'' '%}'' 'can'' 'access'' 'organization'' 'resources'' 'without'' 'prior'' 'approval.'' 'For'' 'more'' 'information,'' 'see'' '"[Setting'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'policy'' 'for'' 'your'' 'organization](/organizations/managing''
'-programmatic''
'-access''
'-to''
'-your''
'-organization/setting''
'-a''
'-personal''
'-access''
'-token''
'-policy''
'-for''
'-your''
'-organization)."{%'' 'endnote'' '%}##'' 'Managing'' '{%'' 'data'' 'variables.product.pat_v2'' '%}'' 'requests{%'' 'data'' 'reusables.profile.access_org'' '%}
{%'' 'data'' 'reusables.profile.org_settings'' '%}
1.'' 'In'' 'the'' 'left'' 'sidebar,'' 'under'' '**{%'' 'octicon'' '"key"'' 'aria''
'-label="The'' 'key'' 'icon"'' '%}'' '{%'' 'data'' 'variables.product.pat_generic_caps'' '%}s**,'' 'click'' '**Pending'' 'requests**.'' 'If'' 'any'' 'tokens'' 'are'' 'pending'' 'approval'' 'for'' 'your'' 'organization,'' 'they'' 'will'' 'be'' 'displayed.
1.'' 'Click'' 'the'' 'name'' 'of'' 'the'' 'token'' 'that'' 'you'' 'want'' 'to'' 'approve'' 'or'' 'deny.
1.'' 'Review'' 'the'' 'access'' 'and'' 'permissions'' 'that'' 'the'' 'token'' 'is'' 'requesting.
1.'' 'To'' 'grant'' 'the'' 'token'' 'access'' 'to'' 'the'' 'organization,'' 'click'' '**Approve**.'' 'To'' 'deny'' 'the'' 'token'' 'access'' 'to'' 'the'' 'organization,'' 'click'' '**Deny**.
1.'' 'If'' 'you'' 'denied'' 'the'' 'request,'' 'in'' 'the'' 'confirmation'' 'box,'' 'optionally'' 'enter'' 'the'' 'reason'' 'that'' 'you'' 'denied'' 'the'' 'token.'' 'This'' 'reason'' 'will'' 'be'' 'shared'' 'in'' 'the'' 'notification'' 'that'' 'is'' 'sent'' 'to'' 'the'' 'token'' 'owner.'' 'Then,'' 'click'' '**Deny**.Alternatively,'' 'you'' 'can'' 'approve'' 'or'' 'deny'' 'multiple'' 'tokens'' 'at'' 'once:{%'' 'data'' 'reusables.profile.access_org'' '%}
{%'' 'data'' 'reusables.profile.org_settings'' '%}
1.'' 'In'' 'the'' 'left'' 'sidebar,'' 'under'' '**{%'' 'octicon'' '"key"'' 'aria''
'-label="The'' 'key'' 'icon"'' '%}'' '{%'' 'data'' 'variables.product.pat_generic_caps'' '%}s**,'' 'click'' '**Pending'' 'requests**.'' 'If'' 'any'' 'tokens'' 'are'' 'pending'' 'approval'' 'for'' 'your'' 'organization,'' 'they'' 'will'' 'be'' 'displayed.
1.'' 'Optionally,'' 'use'' 'the'' '**Owner**'' 'and'' '**Repository**'' 'dropdown'' 'menus'' 'to'' 'filter'' 'the'' 'requests'' 'by'' 'the'' 'member'' 'making'' 'the'' 'request.
1.'' 'Select'' 'each'' 'token'' 'that'' 'you'' 'want'' 'to'' 'approve'' 'or'' 'reject.
1.'' 'Select'' 'the'' '**request'' 'selected...**'' 'dropdown'' 'menu'' 'and'' 'click'' '**Approve...**'' 'or'' '**Deny...**.
'' ''' '1'' ''' '
...ub''
'-app''
'-managers''
'-from''
'-your''
'-organization.md'' '???'' '...ub''
'-app''
'-managers''
'-from''
'-your''
'-organization.md
'@'@'' '''
'-4,6'' '+4,7'' ''@'@'' 'intro:'' ''Organization'' 'owners'' 'can'' 'revoke'' '{%'' 'data'' 'variables.product.prodname_github
redirect_from:
'' ''' ''' '/articles/removing''
'-github''
'-app''
'-managers''
'-from''
'-your''
'-organization
'' ''' ''' '/github/setting''
'-up''
'-and''
'-managing''
'-organizations''
'-and''
'-teams/removing''
'-github''
'-app''
'-managers''
'-from''
'-your''
'-organization
'' ''' ''' '/organizations/managing''
'-access''
'-to''
'-your''
'-organizations''
'-apps/removing''
'-github''
'-app''
'-managers''
'-from''
'-your''
'-organization
versions:
'' ''' 'fpt:'' ''*'
'' ''' 'ghes:'' ''*'
'' '37'' ''' '
...anization/reviewing''
'-and''
'-revoking''
'-personal''
'-access''
'-tokens''
'-in''
'-your''
'-organization.md
'@'@'' '''
'-0,0'' '+1,37'' ''@'@
''
'-
title:'' 'Reviewing'' 'and'' 'revoking'' 'personal'' 'access'' 'tokens'' 'in'' 'your'' 'organization
intro:'' 'Organization'' 'owners'' 'can'' 'review'' 'the'' '{%'' 'data'' 'variables.product.pat_v2'' '%}s'' 'that'' 'can'' 'access'' 'their'' 'organization.'' 'They'' 'can'' 'also'' 'revoke'' 'access'' 'of'' 'specific'' '{%'' 'data'' 'variables.product.pat_v2'' '%}s.
versions:
'' ''' 'feature:'' 'pat''
'-v2
shortTitle:'' 'Review'' 'token'' 'access
''
'-{%'' 'data'' 'reusables.user''
'-settings.pat''
'-v2''
'-org''
'-opt''
'-in'' '%}##'' 'About'' 'reviewing'' 'and'' 'revoking'' ''' '{%'' 'data'' 'variables.product.pat_v2'' '%}sOrganization'' 'owners'' 'can'' 'view'' 'all'' '{%'' 'data'' 'variables.product.pat_v2'' '%}s'' 'that'' 'can'' 'access'' 'resources'' 'owned'' 'by'' 'the'' 'organization.'' 'Organization'' 'owners'' 'can'' 'also'' 'revoke'' 'access'' 'by'' '{%'' 'data'' 'variables.product.pat_v2'' '%}s.'' 'When'' 'a'' '{%'' 'data'' 'variables.product.pat_v2'' '%}'' 'is'' 'revoked,'' 'SSH'' 'keys'' 'created'' 'by'' 'the'' 'token'' 'will'' 'continue'' 'to'' 'work'' 'and'' 'the'' 'token'' 'will'' 'still'' 'be'' 'able'' 'to'' 'read'' 'public'' 'resources'' 'within'' 'the'' 'organization.When'' 'a'' 'token'' 'is'' 'revoked,'' 'the'' 'user'' 'who'' 'created'' 'the'' 'token'' 'will'' 'receive'' 'an'' 'email'' 'notification.Organization'' 'owners'' 'can'' 'only'' 'view'' 'and'' 'revoke'' '{%'' 'data'' 'variables.product.pat_v2'' '%}s,'' 'not'' '{%'' 'data'' 'variables.product.pat_v1_plural'' '%}.'' 'Unless'' 'the'' 'organization'' '{%'' 'ifversion'' 'ghec'' 'or'' 'ghes'' 'or'' 'ghae'' '%}or'' 'enterprise'' '{%'' 'endif'' '%}has'' 'restricted'' 'access'' 'by'' '{%'' 'data'' 'variables.product.pat_v1_plural'' '%},'' 'any'' '{%'' 'data'' 'variables.product.pat_v1'' '%}'' 'can'' 'access'' 'organization'' 'resources'' 'until'' 'the'' 'token'' 'expires.'' 'For'' 'more'' 'information'' 'about'' 'restricting'' 'access'' 'by'' '{%'' 'data'' 'variables.product.pat_v1_plural'' '%},'' 'see'' '"[Setting'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'policy'' 'for'' 'your'' 'organization](/organizations/managing''
'-programmatic''
'-access''
'-to''
'-your''
'-organization/setting''
'-a''
'-personal''
'-access''
'-token''
'-policy''
'-for''
'-your''
'-organization)"{%'' 'ifversion'' 'ghec'' 'or'' 'ghes'' 'or'' 'ghae'' '%}'' 'and'' '"[Enforcing'' 'policies'' 'for'' '{%'' 'data'' 'variables.product.pat_generic'' '%}s'' 'in'' 'your'' 'enterprise](/admin/policies/enforcing''
'-policies''
'-for''
'-your''
'-enterprise/enforcing''
'-policies''
'-for''
'-personal''
'-access''
'-tokens''
'-in''
'-your''
'-enterprise)"{%'' 'endif'' '%}.{%'' 'ifversion'' 'ghec'' '%}'' 'Organization'' 'owners'' 'can'' 'also'' 'view'' 'and'' 'revoke'' '{%'' 'data'' 'variables.product.pat_v1_plural'' '%}'' 'if'' 'their'' 'organization'' 'requires'' 'SAML'' 'single''
'-sign'' 'on.'' 'For'' 'more'' 'information,'' 'see'' '"[Viewing'' 'and'' 'managing'' 'a'' 'user's'' 'SAML'' 'access'' 'to'' 'your'' 'enterprise](/admin/user''
'-management/managing''
'-users''
'-in''
'-your''
'-enterprise/viewing''
'-and''
'-managing''
'-a''
'-users''
'-saml''
'-access''
'-to''
'-your''
'-enterprise#viewing''
'-and''
'-revoking''
'-authorized''
'-credentials)".'' 'For'' 'more'' 'information'' 'about'' 'using'' 'the'' 'REST'' 'API'' 'to'' 'do'' 'this,'' 'see'' '"[List'' 'SAML'' 'SSO'' 'authorizations'' 'for'' 'an'' 'organization](/rest/orgs/orgs#list''
'-saml''
'-sso''
'-authorizations''
'-for''
'-an''
'-organization)"'' 'and'' '"[Remove'' 'a'' 'SAML'' 'SSO'' 'authorization'' 'for'' 'an'' 'organization](/rest/orgs/orgs#remove''
'-a''
'-saml''
'-sso''
'-authorization''
'-for''
'-an''
'-organization)."{%'' 'endif'' '%}##'' 'Reviewing'' 'and'' 'revoking'' ''' '{%'' 'data'' 'variables.product.pat_v2'' '%}s{%'' 'data'' 'reusables.profile.access_org'' '%}
{%'' 'data'' 'reusables.profile.org_settings'' '%}
1.'' 'In'' 'the'' 'left'' 'sidebar,'' 'under'' '**{%'' 'octicon'' '"key"'' 'aria''
'-label="The'' 'key'' 'icon"'' '%}'' '{%'' 'data'' 'variables.product.pat_generic_caps'' '%}s**,'' 'click'' '**Active'' 'tokens**.'' 'Any'' '{%'' 'data'' 'variables.product.pat_v2'' '%}s'' 'that'' 'can'' 'access'' 'your'' 'organization'' 'will'' 'be'' 'displayed.
1.'' 'Click'' 'the'' 'name'' 'of'' 'the'' 'token'' 'that'' 'you'' 'want'' 'review'' 'or'' 'revoke.
1.'' 'Review'' 'the'' 'access'' 'and'' 'permissions'' 'that'' 'the'' 'token'' 'has.
1.'' 'To'' 'revoke'' 'access'' 'by'' 'the'' 'token'' 'to'' 'the'' 'organization,'' 'click'' '**Revoke**.Alternatively,'' 'you'' 'can'' 'revoke'' 'multiple'' 'tokens'' 'at'' 'once:{%'' 'data'' 'reusables.profile.access_org'' '%}
{%'' 'data'' 'reusables.profile.org_settings'' '%}
1.'' 'In'' 'the'' 'left'' 'sidebar,'' 'under'' '**{%'' 'octicon'' '"key"'' 'aria''
'-label="The'' 'key'' 'icon"'' '%}'' '{%'' 'data'' 'variables.product.pat_generic_caps'' '%}s**,'' 'click'' '**Active'' 'tokens**.'' 'Any'' '{%'' 'data'' 'variables.product.pat_v2'' '%}s'' 'that'' 'can'' 'access'' 'your'' 'organization'' 'will'' 'be'' 'displayed.
1.'' 'Optionally,'' 'use'' 'the'' '**Owner**'' 'dropdown'' 'to'' 'filter'' 'the'' 'tokens'' 'by'' 'the'' 'member'' 'who'' 'created'' 'the'' 'token.
1.'' 'Select'' 'each'' 'token'' 'that'' 'you'' 'want'' 'to'' 'revoke.
1.'' 'Select'' 'the'' '**tokens'' 'selected...**'' 'dropdown'' 'menu'' 'and'' 'click'' '**Revoke...**.
'' ''' '1'' ''' '
...r''
'-organizations''
'-installed''
'-integrations.md'' '???'' '...r''
'-organizations''
'-installed''
'-integrations.md
'@'@'' '''
'-6,6'' '+6,7'' ''@'@'' 'redirect_from:
'' ''' ''' '/articles/reviewing''
'-your''
'-organizations''
'-installed''
'-integrations
'' ''' ''' '/github/setting''
'-up''
'-and''
'-managing''
'-organizations''
'-and''
'-teams/reviewing''
'-your''
'-organizations''
'-installed''
'-integrations
'' ''' ''' '/organizations/keeping''
'-your''
'-organization''
'-secure/reviewing''
'-your''
'-organizations''
'-installed''
'-integrations
'' ''' ''' '/organizations/keeping''
'-your''
'-organization''
'-secure/managing''
'-security''
'-settings''
'-for''
'-your''
'-organization/reviewing''
'-your''
'-organizations''
'-installed''
'-integrations
versions:
'' ''' 'fpt:'' ''*'
'' ''' 'ghes:'' ''*'
'' '57'' ''' '
...ur''
'-organization/setting''
'-a''
'-personal''
'-access''
'-token''
'-policy''
'-for''
'-your''
'-organization.md
'@'@'' '''
'-0,0'' '+1,57'' ''@'@
''
'-
title:'' 'Setting'' 'a'' 'personal'' 'access'' 'token'' 'policy'' 'for'' 'your'' 'organization
intro:'' '"Organization'' 'owners'' 'can'' 'control'' 'whether'' 'to'' 'allow'' '{%'' 'data'' 'variables.product.pat_v2'' '%}s'' 'and'' '{%'' 'data'' 'variables.product.pat_v1_plural'' '%},'' 'and'' 'can'' 'require'' 'approval'' 'for'' '{%'' 'data'' 'variables.product.pat_v2'' '%}s."
versions:
'' ''' 'feature:'' 'pat''
'-v2
shortTitle:'' 'Set'' 'a'' 'token'' 'policy
''
'-{%'' 'data'' 'reusables.user''
'-settings.pat''
'-v2''
'-org''
'-opt''
'-in'' '%}##'' 'Restricting'' 'access'' 'by'' '{%'' 'data'' 'variables.product.pat_v2'' '%}sOrganization'' 'owners'' 'can'' 'prevent'' '{%'' 'data'' 'variables.product.pat_v2'' '%}s'' 'from'' 'accessing'' 'resources'' 'owned'' 'by'' 'the'' 'organization.'' '{%'' 'data'' 'variables.product.pat_v2_caps'' '%}s'' 'will'' 'still'' 'be'' 'able'' 'to'' 'read'' 'public'' 'resources'' 'within'' 'the'' 'organization.'' 'This'' 'setting'' 'only'' 'controls'' 'access'' 'by'' '{%'' 'data'' 'variables.product.pat_v2'' '%}s,'' 'not'' '{%'' 'data'' 'variables.product.pat_v1_plural'' '%}.'' 'For'' 'more'' 'information'' 'about'' 'restricting'' 'access'' 'by'' '{%'' 'data'' 'variables.product.pat_v1_plural'' '%},'' 'see'' '"[Restricting'' 'access'' 'by'' '{%'' 'data'' 'variables.product.pat_v1_plural'' '%}](#restricting''
'-access''
'-by''
'-personal''
'-access''
'-tokens''
'-classic)"'' 'on'' 'this'' 'page.{%'' 'ifversion'' 'ghec'' 'or'' 'ghes'' 'or'' 'ghae'' '%}'' 'If'' 'your'' 'organization'' 'is'' 'owned'' 'by'' 'an'' 'enterprise,'' 'and'' 'your'' 'enterprise'' 'owner'' 'has'' 'restricted'' 'access'' 'by'' '{%'' 'data'' 'variables.product.pat_v2'' '%}s,'' 'then'' 'you'' 'cannot'' 'override'' 'the'' 'policy'' 'in'' 'your'' 'organization.'' 'For'' 'more'' 'information,'' 'see'' '"[Enforcing'' 'policies'' 'for'' '{%'' 'data'' 'variables.product.pat_generic'' '%}s'' 'in'' 'your'' 'enterprise](/admin/policies/enforcing''
'-policies''
'-for''
'-your''
'-enterprise/enforcing''
'-policies''
'-for''
'-personal''
'-access''
'-tokens''
'-in''
'-your''
'-enterprise)."{%'' 'endif'' '%}{%'' 'data'' 'reusables.profile.access_org'' '%}
{%'' 'data'' 'reusables.profile.org_settings'' '%}
1.'' 'In'' 'the'' 'left'' 'sidebar,'' 'under'' '**{%'' 'octicon'' '"key"'' 'aria''
'-label="The'' 'key'' 'icon"'' '%}'' '{%'' 'data'' 'variables.product.pat_generic_caps'' '%}s**,'' 'click'' '**Settings**.
1.'' 'Under'' '**{%'' 'data'' 'variables.product.pat_v2_caps'' '%}s**,'' 'select'' 'the'' 'option'' 'that'' 'meets'' 'your'' 'needs:
'' ''' ''' ''' '**Allow'' 'access'' 'via'' '{%'' 'data'' 'variables.product.pat_v2'' '%}s**:'' ''' '{%'' 'data'' 'variables.product.pat_v2_caps'' '%}s'' 'can'' 'access'' 'resources'' 'owned'' 'by'' 'the'' 'organization.
'' ''' ''' ''' '**Restrict'' 'access'' 'via'' '{%'' 'data'' 'variables.product.pat_v2'' '%}s**:'' '{%'' 'data'' 'variables.product.pat_v2_caps'' '%}s'' 'cannot'' 'access'' 'resources'' 'owned'' 'by'' 'the'' 'organization.'' 'SSH'' 'keys'' 'created'' 'by'' '{%'' 'data'' 'variables.product.pat_v2'' '%}s'' 'will'' 'continue'' 'to'' 'work.
1.'' 'Click'' '**Save**.##'' 'Enforcing'' 'an'' 'approval'' 'policy'' 'for'' '{%'' 'data'' 'variables.product.pat_v2'' '%}sOrganization'' 'owners'' 'can'' 'require'' 'approval'' 'for'' 'each'' '{%'' 'data'' 'variables.product.pat_v2'' '%}'' 'that'' 'can'' 'access'' 'the'' 'organization.'' '{%'' 'data'' 'variables.product.pat_v2_caps'' '%}s'' 'will'' 'still'' 'be'' 'able'' 'to'' 'read'' 'public'' 'resources'' 'within'' 'the'' 'organization'' 'without'' 'approval.'' '{%'' 'data'' 'variables.product.pat_v2_caps'' '%}s'' 'created'' 'by'' 'organization'' 'owners'' 'will'' 'not'' 'need'' 'approval.{%'' 'ifversion'' 'ghec'' 'or'' 'ghes'' 'or'' 'ghae'' '%}'' 'If'' 'your'' 'organization'' 'is'' 'owned'' 'by'' 'an'' 'enterprise,'' 'and'' 'your'' 'enterprise'' 'owner'' 'has'' 'set'' 'an'' 'approval'' 'policy'' 'for'' '{%'' 'data'' 'variables.product.pat_v2'' '%}s,'' 'then'' 'you'' 'cannot'' 'override'' 'the'' 'policy'' 'in'' 'your'' 'organization.'' 'For'' 'more'' 'information,'' 'see'' '"[Enforcing'' 'policies'' 'for'' '{%'' 'data'' 'variables.product.pat_generic'' '%}s'' 'in'' 'your'' 'enterprise](/admin/policies/enforcing''
'-policies''
'-for''
'-your''
'-enterprise/enforcing''
'-policies''
'-for''
'-personal''
'-access''
'-tokens''
'-in''
'-your''
'-enterprise)."{%'' 'endif'' '%}{%'' 'note'' '%}**Note**:'' 'Only'' '{%'' 'data'' 'variables.product.pat_v2'' '%}s,'' 'not'' '{%'' 'data'' 'variables.product.pat_v1_plural'' '%},'' 'are'' 'subject'' 'to'' 'approval.'' 'Unless'' 'the'' 'organization'' 'has'' 'restricted'' 'access'' 'by'' '{%'' 'data'' 'variables.product.pat_v1_plural'' '%},'' 'any'' '{%'' 'data'' 'variables.product.pat_v1'' '%}'' 'can'' 'access'' 'organization'' 'resources'' 'without'' 'prior'' 'approval.'' 'For'' 'more'' 'information,'' 'see'' '"[Restricting'' 'access'' 'by'' '{%'' 'data'' 'variables.product.pat_v1_plural'' '%}](#restricting''
'-access''
'-by''
'-personal''
'-access''
'-tokens''
'-classic)"'' 'on'' 'this'' 'page.{%'' 'endnote'' '%}{%'' 'data'' 'reusables.profile.access_org'' '%}
{%'' 'data'' 'reusables.profile.org_settings'' '%}
1.'' 'In'' 'the'' 'left'' 'sidebar,'' 'under'' '**{%'' 'octicon'' '"key"'' 'aria''
'-label="The'' 'key'' 'icon"'' '%}'' '{%'' 'data'' 'variables.product.pat_generic_caps'' '%}s**,'' 'click'' '**Settings**.
1.'' 'Under'' '**Require'' 'approval'' 'of'' '{%'' 'data'' 'variables.product.pat_v2'' '%}s**,'' 'select'' 'the'' 'option'' 'that'' 'meets'' 'your'' 'needs:
'' ''' ''' ''' '**Require'' 'administrator'' 'approval**:'' 'An'' 'organization'' 'owner'' 'must'' 'approve'' 'each'' '{%'' 'data'' 'variables.product.pat_v2'' '%}'' 'that'' 'can'' 'access'' 'the'' 'organization.'' '{%'' 'data'' 'variables.product.pat_v2_caps'' '%}s'' 'created'' 'by'' 'organization'' 'owners'' 'will'' 'not'' 'need'' 'approval.
'' ''' ''' ''' '**Do'' 'not'' 'require'' 'administrator'' 'approval**:'' '{%'' 'data'' 'variables.product.pat_v2_caps'' '%}s'' 'created'' 'by'' 'organization'' 'members'' 'can'' 'access'' 'resources'' 'in'' 'the'' 'organization'' 'without'' 'prior'' 'approval.
1.'' 'Click'' '**Save**.##'' 'Restricting'' 'access'' 'by'' '{%'' 'data'' 'variables.product.pat_v1_plural'' '%}Organization'' 'owners'' 'can'' 'prevent'' '{%'' 'data'' 'variables.product.pat_v1_plural'' '%}'' 'from'' 'accessing'' 'resources'' 'owned'' 'by'' 'the'' 'organization.'' '{%'' 'data'' 'variables.product.pat_v1_caps_plural'' '%}'' 'will'' 'still'' 'be'' 'able'' 'to'' 'read'' 'public'' 'resources'' 'within'' 'the'' 'organization.'' 'This'' 'setting'' 'only'' 'controls'' 'access'' 'by'' '{%'' 'data'' 'variables.product.pat_v1_plural'' '%},'' 'not'' '{%'' 'data'' 'variables.product.pat_v2'' '%}s.'' 'For'' 'more'' 'information'' 'about'' 'restricting'' 'access'' 'by'' '{%'' 'data'' 'variables.product.pat_v2'' '%}s,'' 'see'' '"[Restricting'' 'access'' 'by'' '{%'' 'data'' 'variables.product.pat_v2'' '%}s](#restricting''
'-access''
'-by''
'-fine''
'-grained''
'-personal''
'-access''
'-tokens)"'' 'on'' 'this'' 'page.{%'' 'ifversion'' 'ghec'' 'or'' 'ghes'' 'or'' 'ghae'' '%}'' 'If'' 'your'' 'organization'' 'is'' 'owned'' 'by'' 'an'' 'enterprise,'' 'and'' 'your'' 'enterprise'' 'owner'' 'has'' 'restricted'' 'access'' 'by'' '{%'' 'data'' 'variables.product.pat_v1_plural'' '%},'' 'then'' 'you'' 'cannot'' 'override'' 'the'' 'policy'' 'in'' 'your'' 'organization.'' 'For'' 'more'' 'information,'' 'see'' '"[Enforcing'' 'policies'' 'for'' '{%'' 'data'' 'variables.product.pat_generic'' '%}s'' 'in'' 'your'' 'enterprise](/admin/policies/enforcing''
'-policies''
'-for''
'-your''
'-enterprise/enforcing''
'-policies''
'-for''
'-personal''
'-access''
'-tokens''
'-in''
'-your''
'-enterprise)."{%'' 'endif'' '%}{%'' 'data'' 'reusables.profile.access_org'' '%}
{%'' 'data'' 'reusables.profile.org_settings'' '%}
1.'' 'In'' 'the'' 'left'' 'sidebar,'' 'under'' '**{%'' 'octicon'' '"key"'' 'aria''
'-label="The'' 'key'' 'icon"'' '%}'' '{%'' 'data'' 'variables.product.pat_generic_caps'' '%}s**,'' 'click'' '**Settings**.
1.'' 'Under'' '**{%'' 'data'' 'variables.product.pat_v1_caps'' '%}**,'' 'select'' 'the'' 'option'' 'that'' 'meets'' 'your'' 'needs:
'' ''' ''' ''' '**Allow'' 'access'' 'via'' '{%'' 'data'' 'variables.product.pat_v1_plural'' '%}**:'' '{%'' 'data'' 'variables.product.pat_v1_caps_plural'' '%}'' 'can'' 'access'' 'resources'' 'owned'' 'by'' 'the'' 'organization.
'' ''' ''' ''' '**Restrict'' 'access'' 'via'' '{%'' 'data'' 'variables.product.pat_v1_plural'' '%}**:'' '{%'' 'data'' 'variables.product.pat_v1_caps_plural'' '%}'' 'cannot'' 'access'' 'resources'' 'owned'' 'by'' 'the'' 'organization.'' 'SSH'' 'keys'' 'created'' 'by'' '{%'' 'data'' 'variables.product.pat_v1_plural'' '%}'' 'will'' 'continue'' 'to'' 'work.
1.'' 'Click'' '**Save**.
'' ''' '2'' ''' '
...r''
'-organization/about''
'-identity''
'-and''
'-access''
'-management''
'-with''
'-saml''
'-single''
'-sign''
'-on.md
'@'@'' '''
'-30,7'' '+30,7'' ''@'@'' 'For'' 'an'' 'organization,'' 'SAML'' 'SSO'' 'can'' 'be'' 'disabled,'' 'enabled'' 'but'' 'not'' 'enforced,'' 'or'' 'enabMembers'' 'must'' 'periodically'' 'authenticate'' 'with'' 'your'' 'IdP'' 'to'' 'authenticate'' 'and'' 'gain'' 'access'' 'to'' 'your'' 'organization's'' 'resources.'' 'The'' 'duration'' 'of'' 'this'' 'login'' 'period'' 'is'' 'specified'' 'by'' 'your'' 'IdP'' 'and'' 'is'' 'generally'' '24'' 'hours.'' 'This'' 'periodic'' 'login'' 'requirement'' 'limits'' 'the'' 'length'' 'of'' 'access'' 'and'' 'requires'' 'users'' 'to'' 're''
'-identify'' 'themselves'' 'to'' 'continue.To'' 'access'' 'the'' 'organization's'' 'protected'' 'resources'' 'using'' 'the'' 'API'' 'and'' 'Git'' 'on'' 'the'' 'command'' 'line,'' 'members'' 'must'' 'authorize'' 'and'' 'authenticate'' 'with'' 'a'' 'personal'' 'access'' 'token'' 'or'' 'SSH'' 'key.'' 'For'' 'more'' 'information,'' 'see'' '"[Authorizing'' 'a'' 'personal'' 'access'' 'token'' 'for'' 'use'' 'with'' 'SAML'' 'single'' 'sign''
'-on](/github/authenticating''
'-to''
'-github/authorizing''
'-a''
'-personal''
'-access''
'-token''
'-for''
'-use''
'-with''
'-saml''
'-single''
'-sign''
'-on)"'' 'and'' '"[Authorizing'' 'an'' 'SSH'' 'key'' 'for'' 'use'' 'with'' 'SAML'' 'single'' 'sign''
'-on](/github/authenticating''
'-to''
'-github/authorizing''
'-an''
'-ssh''
'-key''
'-for''
'-use''
'-with''
'-saml''
'-single''
'-sign''
'-on)."
To'' 'access'' 'the'' 'organization's'' 'protected'' 'resources'' 'using'' 'the'' 'API'' 'and'' 'Git'' 'on'' 'the'' 'command'' 'line,'' 'members'' 'must'' 'authorize'' 'and'' 'authenticate'' 'with'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'or'' 'SSH'' 'key.'' 'For'' 'more'' 'information,'' 'see'' '"[Authorizing'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'for'' 'use'' 'with'' 'SAML'' 'single'' 'sign''
'-on](/github/authenticating''
'-to''
'-github/authorizing''
'-a''
'-personal''
'-access''
'-token''
'-for''
'-use''
'-with''
'-saml''
'-single''
'-sign''
'-on)"'' 'and'' '"[Authorizing'' 'an'' 'SSH'' 'key'' 'for'' 'use'' 'with'' 'SAML'' 'single'' 'sign''
'-on](/github/authenticating''
'-to''
'-github/authorizing''
'-an''
'-ssh''
'-key''
'-for''
'-use''
'-with''
'-saml''
'-single''
'-sign''
'-on)."The'' 'first'' 'time'' 'a'' 'member'' 'uses'' 'SAML'' 'SSO'' 'to'' 'access'' 'your'' 'organization,'' '{%'' 'data'' 'variables.product.prodname_dotcom'' '%}'' 'automatically'' 'creates'' 'a'' 'record'' 'that'' 'links'' 'your'' 'organization,'' 'the'' 'member's'' 'account'' 'on'' '{%'' 'data'' 'variables.location.product_location'' '%},'' 'and'' 'the'' 'member's'' 'account'' 'on'' 'your'' 'IdP.'' 'You'' 'can'' 'view'' 'and'' 'revoke'' 'the'' 'linked'' 'SAML'' 'identity,'' 'active'' 'sessions,'' 'and'' 'authorized'' 'credentials'' 'for'' 'members'' 'of'' 'your'' 'organization'' 'or'' 'enterprise'' 'account.'' 'For'' 'more'' 'information,'' 'see'' '"[Viewing'' 'and'' 'managing'' 'a'' 'member's'' 'SAML'' 'access'' 'to'' 'your'' 'organization](/organizations/granting''
'-access''
'-to''
'-your''
'-organization''
'-with''
'-saml''
'-single''
'-sign''
'-on/viewing''
'-and''
'-managing''
'-a''
'-members''
'-saml''
'-access''
'-to''
'-your''
'-organization)"'' 'and'' '"[Viewing'' 'and'' 'managing'' 'a'' 'user's'' 'SAML'' 'access'' 'to'' 'your'' 'enterprise'' 'account](/enterprise''
'-cloud'@latest/admin/user''
'-management/managing''
'-users''
'-in''
'-your''
'-enterprise/viewing''
'-and''
'-managing''
'-a''
'-users''
'-saml''
'-access''
'-to''
'-your''
'-enterprise)."'' ''' '2'' ''' '
...ization/troubleshooting''
'-identity''
'-and''
'-access''
'-management''
'-for''
'-your''
'-organization.md
'@'@'' '''
'-79,7'' '+79,7'' ''@'@'' 'This'' 'GraphQL'' 'query'' 'shows'' 'you'' 'the'' 'SAML'' '`NameId`,'' 'the'' 'SCIM'' '`UserName`'' 'and'' 'the'' '{%'' 'd
curl'' '''
'-X'' 'POST'' '''
'-H'' '"Authorization:'' 'Bearer'' '<personal'' 'access'' 'token>"'' '''
'-H'' '"Content''
'-Type:'' 'application/json"'' '''
'-d'' ''{'' '"query":'' '"{'' 'organization(login:'' '\"ORG\")'' '{'' 'samlIdentityProvider'' '{'' 'externalIdentities(first:'' '100)'' '{'' 'pageInfo'' '{'' 'endCursor'' 'startCursor'' 'hasNextPage'' '}'' 'edges'' '{'' 'cursor'' 'node'' '{'' 'samlIdentity'' '{'' 'nameId'' '}'' 'scimIdentity'' '{username}'' ''' 'user'' '{'' 'login'' '}'' '}'' '}'' '}'' '}'' '}'' '}"'' '}''' ''' 'https://api.github.com/graphql
curl'' '''
'-X'' 'POST'' '''
'-H'' '"Authorization:'' 'Bearer'' 'YOUR_TOKEN"'' '''
'-H'' '"Content''
'-Type:'' 'application/json"'' '''
'-d'' ''{'' '"query":'' '"{'' 'organization(login:'' '\"ORG\")'' '{'' 'samlIdentityProvider'' '{'' 'externalIdentities(first:'' '100)'' '{'' 'pageInfo'' '{'' 'endCursor'' 'startCursor'' 'hasNextPage'' '}'' 'edges'' '{'' 'cursor'' 'node'' '{'' 'samlIdentity'' '{'' 'nameId'' '}'' 'scimIdentity'' '{username}'' ''' 'user'' '{'' 'login'' '}'' '}'' '}'' '}'' '}'' '}'' '}"'' '}''' ''' 'https://api.github.com/graphql
For'' 'more'' 'information'' 'on'' 'using'' 'the'' 'GraphQL'' 'API,'' 'see:'' '1
...s''
'-to''
'-repositories''
'-in''
'-your''
'-organization.md'' '???'' '...s''
'-to''
'-repositories''
'-in''
'-your''
'-organization.md'' ''@'@'' '''
'-4,6'' '+4,7'' ''@'@'' 'intro:'' 'You'' 'can'' 'allow'' 'people'' 'who'' 'aren't'' 'members'' 'of'' 'your'' 'organization'' 'to'' 'access'' 're'' 'redirect_from:/articles/adding''
'-outside''
'-collaborators''
'-to''
'-repositories''
'-in''
'-your''
'-organization
/github/setting''
'-up''
'-and''
'-managing''
'-organizations''
'-and''
'-teams/adding''
'-outside''
'-collaborators''
'-to''
'-repositories''
'-in''
'-your''
'-organization
/organizations/managing''
'-access''
'-to''
'-your''
'-organizations''
'-repositories/adding''
'-outside''
'-collaborators''
'-to''
'-repositories''
'-in''
'-your''
'-organization'' 'versions:'' 'fpt:'' ''''' 'ghes:'' ''''' '1
...side''
'-collaborator''
'-in''
'-your''
'-organization.md'' '???'' '...side''
'-collaborator''
'-in''
'-your''
'-organization.md'' ''@'@'' '''
'-4,6'' '+4,7'' ''@'@'' 'intro:'' 'You'' 'can'' 'cancel'' 'all'' 'invitations'' 'for'' 'a'' 'person'' 'to'' 'become'' 'an'' 'outside'' 'collabor'' 'permissions:'' 'Organization'' 'owners'' 'can'' 'cancel'' 'an'' 'invitation'' 'to'' 'become'' 'an'' 'outside'' 'collaborator'' 'in'' 'the'' 'organization.'' 'redirect_from:
/github/setting''
'-up''
'-and''
'-managing''
'-organizations''
'-and''
'-teams/canceling''
'-an''
'-invitation''
'-to''
'-become''
'-an''
'-outside''
'-collaborator''
'-in''
'-your''
'-organization
/organizations/managing''
'-access''
'-to''
'-your''
'-organizations''
'-repositories/canceling''
'-an''
'-invitation''
'-to''
'-become''
'-an''
'-outside''
'-collaborator''
'-in''
'-your''
'-organization'' 'versions:'' 'fpt:'' ''''' 'ghec:'' ''''' '3
...tion''
'-member''
'-to''
'-an''
'-outside''
'-collaborator.md'' '???'' '...tion''
'-member''
'-to''
'-an''
'-outside''
'-collaborator.md'' ''@'@'' '''
'-1,10'' '+1,11'' ''@'@
title:'' 'Converting'' 'an'' 'organization'' 'member'' 'to'' 'an'' 'outside'' 'collaborator'' 'intro:'' ''If'' 'a'' 'current'' 'member'' 'of'' 'your'' 'organization'' 'only'' 'needs'' 'access'' 'to'' 'certain'' 'repositories,'' 'such'' 'as'' 'consultants'' 'or'' 'temporary'' 'employees,'' 'you'' 'can'' 'convert'' 'them'' 'to'' 'an'' 'outside'' 'collaborator.''' 'permissions:'' ''Organization'' 'owners'' 'can'' 'convert'' 'an'' 'organization'' 'member'' 'to'' 'an'' 'outside'' 'collaborator.''' 'permissions:'' 'Organization'' 'owners'' 'can'' 'convert'' 'an'' 'organization'' 'member'' 'to'' 'an'' 'outside'' 'collaborator.'' 'redirect_from:/articles/converting''
'-an''
'-organization''
'-member''
'-to''
'-an''
'-outside''
'-collaborator
/github/setting''
'-up''
'-and''
'-managing''
'-organizations''
'-and''
'-teams/converting''
'-an''
'-organization''
'-member''
'-to''
'-an''
'-outside''
'-collaborator
/organizations/managing''
'-access''
'-to''
'-your''
'-organizations''
'-repositories/converting''
'-an''
'-organization''
'-member''
'-to''
'-an''
'-outside''
'-collaborator'' 'versions:'' 'fpt:'' ''''' 'ghes:'' ''''' '1
...collaborator''
'-to''
'-an''
'-organization''
'-member.md'' '???'' '...collaborator''
'-to''
'-an''
'-organization''
'-member.md'' ''@'@'' '''
'-4,6'' '+4,7'' ''@'@'' 'intro:'' ''If'' 'you'' 'would'' 'like'' 'to'' 'give'' 'an'' 'outside'' 'collaborator'' 'on'' 'your'' 'organization'''' 'redirect_from:
/articles/converting''
'-an''
'-outside''
'-collaborator''
'-to''
'-an''
'-organization''
'-member
/github/setting''
'-up''
'-and''
'-managing''
'-organizations''
'-and''
'-teams/converting''
'-an''
'-outside''
'-collaborator''
'-to''
'-an''
'-organization''
'-member
/organizations/managing''
'-access''
'-to''
'-your''
'-organizations''
'-repositories/converting''
'-an''
'-outside''
'-collaborator''
'-to''
'-an''
'-organization''
'-member'' 'versions:'' 'fpt:'' ''''' 'ghes:'' ''''' '5
...''
'-your''
'-organizations''
'-repositories/index.md'' '???'' '...''
'-your''
'-organizations''
'-repositories/index.md'' ''@'@'' '''
'-1,11'' '+1,12'' ''@'@
title:'' 'Managing'' 'access'' 'to'' 'your'' 'organization's'' 'repositories'' 'title:'' 'Managing'' 'user'' 'access'' 'to'' 'your'' 'organization's'' 'repositories'' 'intro:'' 'Organization'' 'owners'' 'can'' 'manage'' 'individual'' 'and'' 'team'' 'access'' 'to'' 'the'' 'organization's'' 'repositories.'' 'Team'' 'maintainers'' 'can'' 'also'' 'manage'' 'a'' 'team's'' 'repository'' 'access.'' 'redirect_from:/articles/permission''
'-levels''
'-for''
'-an''
'-organization''
'-repository
/articles/managing''
'-access''
'-to''
'-your''
'-organization''
'-s''
'-repositories
/articles/managing''
'-access''
'-to''
'-your''
'-organizations''
'-repositories
/github/setting''
'-up''
'-and''
'-managing''
'-organizations''
'-and''
'-teams/managing''
'-access''
'-to''
'-your''
'-organizations''
'-repositories
/organizations/managing''
'-access''
'-to''
'-your''
'-organizations''
'-repositories'' 'versions:'' 'fpt:'' ''''' 'ghes:'' ''''' ''@'@'' '''
'-26,6'' '+27,6'' ''@'@'' 'children:
/converting''
'-an''
'-organization''
'-member''
'-to''
'-an''
'-outside''
'-collaborator
/converting''
'-an''
'-outside''
'-collaborator''
'-to''
'-an''
'-organization''
'-member
/reinstating''
'-a''
'-former''
'-outside''
'-collaborators''
'-access''
'-to''
'-your''
'-organization'' 'shortTitle:'' 'Manage'' 'access'' 'to'' 'repositories'' 'shortTitle:'' 'Manage'' 'user'' 'access'' 'to'' 'repos
1
...s''
'-access''
'-to''
'-an''
'-organization''
'-repository.md'' '???'' '...s''
'-access''
'-to''
'-an''
'-organization''
'-repository.md'' ''@'@'' '''
'-6,6'' '+6,7'' ''@'@'' 'redirect_from:/articles/managing''
'-an''
'-individual''
'-s''
'-access''
'-to''
'-an''
'-organization''
'-repository
/articles/managing''
'-an''
'-individuals''
'-access''
'-to''
'-an''
'-organization''
'-repository
/github/setting''
'-up''
'-and''
'-managing''
'-organizations''
'-and''
'-teams/managing''
'-an''
'-individuals''
'-access''
'-to''
'-an''
'-organization''
'-repository
/organizations/managing''
'-access''
'-to''
'-your''
'-organizations''
'-repositories/managing''
'-an''
'-individuals''
'-access''
'-to''
'-an''
'-organization''
'-repository'' 'versions:'' 'fpt:'' ''''' 'ghes:'' ''''' '1
...m''
'-access''
'-to''
'-an''
'-organization''
'-repository.md'' '???'' '...m''
'-access''
'-to''
'-an''
'-organization''
'-repository.md'' ''@'@'' '''
'-5,6'' '+5,7'' ''@'@'' 'redirect_from:
/articles/managing''
'-team''
'-access''
'-to''
'-an''
'-organization''
'-repository''
'-early''
'-access''
'-program
/articles/managing''
'-team''
'-access''
'-to''
'-an''
'-organization''
'-repository
/github/setting''
'-up''
'-and''
'-managing''
'-organizations''
'-and''
'-teams/managing''
'-team''
'-access''
'-to''
'-an''
'-organization''
'-repository
/organizations/managing''
'-access''
'-to''
'-your''
'-organizations''
'-repositories/managing''
'-team''
'-access''
'-to''
'-an''
'-organization''
'-repository'' 'versions:'' 'fpt:'' ''''' 'ghes:'' ''''' '1
...laborators''
'-access''
'-to''
'-your''
'-organization.md'' '???'' '...laborators''
'-access''
'-to''
'-your''
'-organization.md'' ''@'@'' '''
'-5,6'' '+5,7'' ''@'@'' 'redirect_from:
/articles/reinstating''
'-a''
'-former''
'-outside''
'-collaborator''
'-s''
'-access''
'-to''
'-your''
'-organization
/articles/reinstating''
'-a''
'-former''
'-outside''
'-collaborators''
'-access''
'-to''
'-your''
'-organization
/github/setting''
'-up''
'-and''
'-managing''
'-organizations''
'-and''
'-teams/reinstating''
'-a''
'-former''
'-outside''
'-collaborators''
'-access''
'-to''
'-your''
'-organization
/organizations/managing''
'-access''
'-to''
'-your''
'-organizations''
'-repositories/reinstating''
'-a''
'-former''
'-outside''
'-collaborators''
'-access''
'-to''
'-your''
'-organization'' 'versions:'' 'fpt:'' ''''' 'ghes:'' ''''' '1
...orator''
'-from''
'-an''
'-organization''
'-repository.md'' '???'' '...orator''
'-from''
'-an''
'-organization''
'-repository.md'' ''@'@'' '''
'-4,6'' '+4,7'' ''@'@'' 'intro:'' 'Owners'' 'and'' 'repository'' 'admins'' 'can'' 'remove'' 'an'' 'outside'' 'collaborator's'' 'access'' 'redirect_from:
/articles/removing''
'-an''
'-outside''
'-collaborator''
'-from''
'-an''
'-organization''
'-repository
/github/setting''
'-up''
'-and''
'-managing''
'-organizations''
'-and''
'-teams/removing''
'-an''
'-outside''
'-collaborator''
'-from''
'-an''
'-organization''
'-repository
/organizations/managing''
'-access''
'-to''
'-your''
'-organizations''
'-repositories/removing''
'-an''
'-outside''
'-collaborator''
'-from''
'-an''
'-organization''
'-repository'' 'versions:'' 'fpt:'' ''''' 'ghes:'' ''''' '1
...s/repository''
'-roles''
'-for''
'-an''
'-organization.md'' '???'' '...s/repository''
'-roles''
'-for''
'-an''
'-organization.md'' ''@'@'' '''
'-7,6'' '+7,7'' ''@'@'' 'redirect_from:
/articles/repository''
'-permission''
'-levels''
'-for''
'-an''
'-organization
/github/setting''
'-up''
'-and''
'-managing''
'-organizations''
'-and''
'-teams/repository''
'-permission''
'-levels''
'-for''
'-an''
'-organization
/organizations/managing''
'-access''
'-to''
'-your''
'-organizations''
'-repositories/repository''
'-permission''
'-levels''
'-for''
'-an''
'-organization
/organizations/managing''
'-access''
'-to''
'-your''
'-organizations''
'-repositories/repository''
'-roles''
'-for''
'-an''
'-organization'' 'versions:'' 'fpt:'' ''''' 'ghes:'' ''''' '1
...g''
'-base''
'-permissions''
'-for''
'-an''
'-organization.md'' '???'' '...g''
'-base''
'-permissions''
'-for''
'-an''
'-organization.md'' ''@'@'' '''
'-4,6'' '+4,7'' ''@'@'' 'intro:'' 'You'' 'can'' 'set'' 'base'' 'permissions'' 'for'' 'the'' 'repositories'' 'that'' 'an'' 'organization'' 'ow'' 'permissions:'' 'Organization'' 'owners'' 'can'' 'set'' 'base'' 'permissions'' 'for'' 'an'' 'organization.'' 'redirect_from:
/github/setting''
'-up''
'-and''
'-managing''
'-organizations''
'-and''
'-teams/setting''
'-base''
'-permissions''
'-for''
'-an''
'-organization
/organizations/managing''
'-access''
'-to''
'-your''
'-organizations''
'-repositories/setting''
'-base''
'-permissions''
'-for''
'-an''
'-organization'' 'versions:'' 'fpt:'' ''''' 'ghes:'' ''''' '1
...''
'-people''
'-with''
'-access''
'-to''
'-your''
'-repository.md'' '???'' '...''
'-people''
'-with''
'-access''
'-to''
'-your''
'-repository.md'' ''@'@'' '''
'-4,6'' '+4,7'' ''@'@'' 'intro:'' ''You'' 'can'' 'view{%'' 'ifversion'' 'ghec'' 'or'' 'ghes'' 'or'' 'ghae'' '%}'' 'and'' 'export{%'' 'endif'' '%}'' 'a'' 'redirect_from:
/articles/viewing''
'-people''
'-with''
'-access''
'-to''
'-your''
'-repository
/github/setting''
'-up''
'-and''
'-managing''
'-organizations''
'-and''
'-teams/viewing''
'-people''
'-with''
'-access''
'-to''
'-your''
'-repository
/organizations/managing''
'-access''
'-to''
'-your''
'-organizations''
'-repositories/viewing''
'-people''
'-with''
'-access''
'-to''
'-your''
'-repository'' 'versions:'' 'fpt:'' ''''' 'ghes:'' ''''' '14
content/packages/learn''
'-github''
'-packages/about''
'-permissions''
'-for''
'-github''
'-packages.md'' ''@'@'' '''
'-45,11'' '+45,13'' ''@'@'' 'For'' 'more'' 'information,'' 'see'' '"[Configuring'' 'a'' 'package's'' 'access'' 'control'' 'and'' 'visibilit
About'' 'scopes'' 'and'' 'permissions'' 'for'' 'package'' 'registries
To'' 'use'' 'or'' 'manage'' 'a'' 'package'' 'hosted'' 'by'' 'a'' 'package'' 'registry,'' 'you'' 'must'' 'use'' 'a'' 'token'' 'with'' 'the'' 'appropriate'' 'scope,'' 'and'' 'your'' 'personal'' 'account'' 'must'' 'have'' 'appropriate'' 'permissions.'' '{%'' 'data'' 'reusables.package_registry.packages''
'-classic''
'-pat''
'-only'' '%}To'' 'use'' 'or'' 'manage'' 'a'' 'package'' 'hosted'' 'by'' 'a'' 'package'' 'registry,'' 'you'' 'must'' 'use'' 'a'' '{%'' 'data'' 'variables.product.pat_v1'' '%}'' 'with'' 'the'' 'appropriate'' 'scope,'' 'and'' 'your'' 'personal'' 'account'' 'must'' 'have'' 'appropriate'' 'permissions.For'' 'example:To'' 'download'' 'and'' 'install'' 'packages'' 'from'' 'a'' 'repository,'' 'your'' 'token'' 'must'' 'have'' 'the'' 'read:packages'' 'scope,'' 'and'' 'your'' 'user'' 'account'' 'must'' 'have'' 'read'' 'permission.
{%'' 'ifversion'' 'fpt'' 'or'' 'ghes'' 'or'' 'ghec'' '%}To'' 'delete'' 'a'' 'package'' 'on'' '{%'' 'data'' 'variables.product.product_name'' '%},'' 'your'' 'token'' 'must'' 'at'' 'least'' 'have'' 'the'' 'delete:packages'' 'and'' 'read:packages'' 'scope.'' 'The'' 'repo'' 'scope'' 'is'' 'also'' 'required'' 'for'' 'repo''
'-scoped'' 'packages.'' 'For'' 'more'' 'information,'' 'see'' '"Deleting'' 'and'' 'restoring'' 'a'' 'package."{%'' 'elsif'' 'ghae'' '%}To'' 'delete'' 'a'' 'specified'' 'version'' 'of'' 'a'' 'package'' 'on'' '{%'' 'data'' 'variables.product.product_name'' '%},'' 'your'' 'token'' 'must'' 'have'' 'the'' 'delete:packages'' 'and'' 'repo'' 'scope.'' 'For'' 'more'' 'information,'' 'see'' '"Deleting'' 'and'' 'restoring'' 'a'' 'package."{%'' 'endif'' '%}
To'' 'download'' 'and'' 'install'' 'packages'' 'from'' 'a'' 'repository,'' 'your'' '{%'' 'data'' 'variables.product.pat_v1'' '%}'' 'must'' 'have'' 'the'' 'read:packages'' 'scope,'' 'and'' 'your'' 'user'' 'account'' 'must'' 'have'' 'read'' 'permission.
{%'' 'ifversion'' 'fpt'' 'or'' 'ghes'' 'or'' 'ghec'' '%}To'' 'delete'' 'a'' 'package'' 'on'' '{%'' 'data'' 'variables.product.product_name'' '%},'' 'your'' '{%'' 'data'' 'variables.product.pat_v1'' '%}'' 'must'' 'at'' 'least'' 'have'' 'the'' 'delete:packages'' 'and'' 'read:packages'' 'scope.'' 'The'' 'repo'' 'scope'' 'is'' 'also'' 'required'' 'for'' 'repo''
'-scoped'' 'packages.'' 'For'' 'more'' 'information,'' 'see'' '"Deleting'' 'and'' 'restoring'' 'a'' 'package."{%'' 'elsif'' 'ghae'' '%}To'' 'delete'' 'a'' 'specified'' 'version'' 'of'' 'a'' 'package'' 'on'' '{%'' 'data'' 'variables.product.product_name'' '%},'' 'your'' '{%'' 'data'' 'variables.product.pat_v1'' '%}'' 'must'' 'have'' 'the'' 'delete:packages'' 'and'' 'repo'' 'scope.'' 'For'' 'more'' 'information,'' 'see'' '"Deleting'' 'and'' 'restoring'' 'a'' 'package."{%'' 'endif'' '%}
Scope	Description	Required'' 'permission
'@'@'' '''
'-58,12'' '+60,12'' ''@'@'' 'For'' 'example:		
delete:packages	{%'' 'ifversion'' 'fpt'' 'or'' 'ghes'' 'or'' 'ghec'' '%}'' 'Delete'' 'packages'' 'from'' '{%'' 'data'' 'variables.product.prodname_registry'' '%}'' '{%'' 'elsif'' 'ghae'' '%}'' 'Delete'' 'specified'' 'versions'' 'of'' 'packages'' 'from'' '{%'' 'data'' 'variables.product.prodname_registry'' '%}'' '{%'' 'endif'' '%}	admin
repo	Upload'' 'and'' 'delete'' 'packages'' '(along'' 'with'' 'write:packages,'' 'or'' 'delete:packages)	write'' 'or'' 'admin
When'' 'you'' 'create'' 'a'' '{%'' 'data'' 'variables.product.prodname_actions'' '%}'' 'workflow,'' 'you'' 'can'' 'use'' 'the'' 'GITHUB_TOKEN'' 'to'' 'publish'' 'and'' 'install'' 'packages'' 'in'' '{%'' 'data'' 'variables.product.prodname_registry'' '%}'' 'without'' 'needing'' 'to'' 'store'' 'and'' 'manage'' 'a'' 'personal'' 'access'' 'token.'' 'When'' 'you'' 'create'' 'a'' '{%'' 'data'' 'variables.product.prodname_actions'' '%}'' 'workflow,'' 'you'' 'can'' 'use'' 'the'' 'GITHUB_TOKEN'' 'to'' 'publish'' 'and'' 'install'' 'packages'' 'in'' '{%'' 'data'' 'variables.product.prodname_registry'' '%}'' 'without'' 'needing'' 'to'' 'store'' 'and'' 'manage'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}.For'' 'more'' 'information,'' 'see:{%'' 'ifversion'' 'fpt'' 'or'' 'ghec'' '%}"Configuring'' 'a'' 'package???s'' 'access'' 'control'' 'and'' 'visibility"{%'' 'endif'' '%}
"Publishing'' 'and'' 'installing'' 'a'' 'package'' 'with'' '{%'' 'data'' 'variables.product.prodname_actions'' '%}"
"Creating'' 'a'' 'personal'' 'access'' 'token"
"Creating'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}"
"Available'' 'scopes"
Maintaining'' 'access'' 'to'' 'packages'' 'in'' '{%'' 'data'' 'variables.product.prodname_actions'' '%}'' 'workflows
'@'@'' '''
'-75,7'' '+77,7'' ''@'@'' 'For'' 'more'' 'conceptual'' 'background'' 'on'' '{%'' 'data'' 'variables.product.prodname_actions'' '%}Access'' 'tokens
To'' 'publish'' 'packages'' 'associated'' 'with'' 'the'' 'workflow'' 'repository,'' 'use'' 'GITHUB_TOKEN.
To'' 'install'' 'packages'' 'associated'' 'with'' 'other'' 'private'' 'repositories'' 'that'' 'GITHUB_TOKEN'' 'can't'' 'access,'' 'use'' 'a'' 'personal'' 'access'' 'token
To'' 'install'' 'packages'' 'associated'' 'with'' 'other'' 'private'' 'repositories'' 'that'' 'GITHUB_TOKEN'' 'can't'' 'access,'' 'use'' 'a'' '{%'' 'data'' 'variables.product.pat_v1'' '%}
For'' 'more'' 'information'' 'about'' 'GITHUB_TOKEN'' 'used'' 'in'' '{%'' 'data'' 'variables.product.prodname_actions'' '%}'' 'workflows,'' 'see'' '"Authentication'' 'in'' 'a'' 'workflow."6
content/packages/learn''
'-github''
'-packages/deleting''
'-and''
'-restoring''
'-a''
'-package.md'' ''@'@'' '''
'-40,6'' '+40,8'' ''@'@'' 'On'' '{%'' 'data'' 'variables.product.prodname_dotcom'' '%},'' 'you'' 'can'' 'also'' 'restore'' 'an'' 'entire'' '{%'' 'ifversion'' 'fpt'' 'or'' 'ghec'' 'or'' 'ghes'' '%}Packages'' 'API'' 'support
{%'' 'data'' 'reusables.package_registry.packages''
'-classic''
'-pat''
'-only'' '%}{%'' 'ifversion'' 'fpt'' 'or'' 'ghec'' '%}You'' 'can'' 'use'' 'the'' 'REST'' 'API'' 'to'' 'manage'' 'your'' 'packages.'' 'For'' 'more'' 'information,'' 'see'' 'the'' '"{%'' 'data'' 'variables.product.prodname_registry'' '%}'' 'API."'' ''@'@'' '''
'-92,7'' '+94,7'' ''@'@'' 'For'' 'packages'' 'that'' 'inherit'' 'their'' 'permissions'' 'and'' 'access'' 'from'' 'repositories,'' 'you'' 'ca{%'' 'data'' 'reusables.package_registry.no''
'-graphql''
'-to''
'-delete''
'-packages'' '%}{%'' 'ifversion'' 'fpt'' 'or'' 'ghec'' '%}'' 'You'' 'can'' 'however'' 'use'' 'the'' 'REST'' 'API.'' 'For'' 'more'' 'information,'' 'see'' 'the'' '"{%'' 'data'' 'variables.product.prodname_registry'' '%}'' 'API."{%'' 'endif'' '%}Use'' 'the'' 'deletePackageVersion'' 'mutation'' 'in'' 'the'' 'GraphQL'' 'API.'' 'You'' 'must'' 'use'' 'a'' 'token'' 'with'' 'the'' 'read:packages,'' 'delete:packages,'' 'and'' 'repo'' 'scopes.'' 'For'' 'more'' 'information'' 'about'' 'tokens,'' 'see'' '"About'' '{%'' 'data'' 'variables.product.prodname_registry'' '%}."'' 'Use'' 'the'' 'deletePackageVersion'' 'mutation'' 'in'' 'the'' 'GraphQL'' 'API.'' 'You'' 'must'' 'use'' 'a'' '{%'' 'data'' 'variables.product.pat_v1'' '%}'' 'with'' 'the'' 'read:packages,'' 'delete:packages,'' 'and'' 'repo'' 'scopes.'' 'For'' 'more'' 'information'' 'about'' '{%'' 'data'' 'variables.product.pat_v1_plural'' '%},'' 'see'' '"About'' '{%'' 'data'' 'variables.product.prodname_registry'' '%}."The'' 'following'' 'example'' 'demonstrates'' 'how'' 'to'' 'delete'' 'a'' 'package'' 'version,'' 'using'' 'a'' 'packageVersionId'' 'of'' 'MDIyOlJlZ2lzdHJ5UGFja2FnZVZlcnNpb243MTExNg.'@'@'' '''
'-104,7'' '+106,7'' ''@'@'' 'curl'' '''
'-X'' 'POST
HOSTNAME/graphql
To'' 'find'' 'all'' 'of'' 'the'' 'private'' 'packages'' 'you'' 'have'' 'published'' 'to'' '{%'' 'data'' 'variables.product.prodname_registry'' '%},'' 'along'' 'with'' 'the'' 'version'' 'IDs'' 'for'' 'the'' 'packages,'' 'you'' 'can'' 'use'' 'the'' '`packages`'' 'connection'' 'through'' 'the'' '`repository`'' 'object.'' 'You'' 'will'' 'need'' 'a'' 'token'' 'with'' 'the'' '`read:packages`'' 'and'' '`repo`'' 'scopes.'' 'For'' 'more'' 'information,'' 'see'' 'the'' '[`packages`](/graphql/reference/objects#repository)'' 'connection'' 'or'' 'the'' '[`PackageOwner`](/graphql/reference/interfaces#packageowner)'' 'interface.
To'' 'find'' 'all'' 'of'' 'the'' 'private'' 'packages'' 'you'' 'have'' 'published'' 'to'' '{%'' 'data'' 'variables.product.prodname_registry'' '%},'' 'along'' 'with'' 'the'' 'version'' 'IDs'' 'for'' 'the'' 'packages,'' 'you'' 'can'' 'use'' 'the'' '`packages`'' 'connection'' 'through'' 'the'' '`repository`'' 'object.'' 'You'' 'will'' 'need'' 'a'' '{%'' 'data'' 'variables.product.pat_v1'' '%}'' 'with'' 'the'' '`read:packages`'' 'and'' '`repo`'' 'scopes.'' 'For'' 'more'' 'information,'' 'see'' 'the'' '[`packages`](/graphql/reference/objects#repository)'' 'connection'' 'or'' 'the'' '[`PackageOwner`](/graphql/reference/interfaces#packageowner)'' 'interface.For'' 'more'' 'information'' 'about'' 'the'' '`deletePackageVersion`'' 'mutation,'' 'see'' '"[`deletePackageVersion`](/graphql/reference/mutations#deletepackageversion)."'' ''' '2'' ''' '
content/packages/learn''
'-github''
'-packages/introduction''
'-to''
'-github''
'-packages.md
'@'@'' '''
'-114,7'' '+114,7'' ''@'@'' 'You'' 'can'' 'delete'' 'a'' 'private'' 'or'' 'public'' 'package'' 'in'' 'the'' '{%'' 'data'' 'variables.product.prod
You'' 'can'' 'delete'' 'a'' 'version'' 'of'' 'a'' 'package'' 'in'' 'the'' '{%'' 'data'' 'variables.product.product_name'' '%}'' 'user'' 'interface'' 'or'' 'using'' 'the'' 'GraphQL'' 'API.
{%'' 'endif'' '%}When'' 'you'' 'use'' 'the'' 'GraphQL'' 'API'' 'to'' 'query'' 'and'' 'delete'' 'private'' 'packages,'' 'you'' 'must'' 'use'' 'the'' 'same'' 'token'' 'you'' 'use'' 'to'' 'authenticate'' 'to'' '{%'' 'data'' 'variables.product.prodname_registry'' '%}.
When'' 'you'' 'use'' 'the'' 'GraphQL'' 'API'' 'to'' 'query'' 'and'' 'delete'' 'private'' 'packages,'' 'you'' 'must'' 'use'' 'the'' 'same'' '{%'' 'data'' 'variables.product.pat_v1'' '%}'' 'you'' 'use'' 'to'' 'authenticate'' 'to'' '{%'' 'data'' 'variables.product.prodname_registry'' '%}.For'' 'more'' 'information,'' 'see'' '{%'' 'ifversion'' 'ghes'' 'or'' 'ghae'' '%}"[Deleting'' 'and'' 'restoring'' 'a'' 'package](/packages/learn''
'-github''
'-packages/deleting''
'-and''
'-restoring''
'-a''
'-package)"'' 'and'' '{%'' 'endif'' '%}"[Forming'' 'calls'' 'with'' 'GraphQL](/graphql/guides/forming''
'-calls''
'-with''
'-graphql)."'' ''' '6'' ''' '
content/packages/learn''
'-github''
'-packages/publishing''
'-a''
'-package.md
'@'@'' '''
'-28,10'' '+28,12'' ''@'@'' 'If'' 'a'' 'new'' 'version'' 'of'' 'a'' 'package'' 'fixes'' 'a'' 'security'' 'vulnerability,'' 'you'' 'should'' 'publish##'' 'Publishing'' 'a'' 'package{%'' 'data'' 'reusables.package_registry.packages''
'-classic''
'-pat''
'-only'' '%}You'' 'can'' 'publish'' 'a'' 'package'' 'to'' '{%'' 'data'' 'variables.product.prodname_registry'' '%}'' 'using'' 'any'' '{%'' 'ifversion'' 'fpt'' 'or'' 'ghae'' 'or'' 'ghec'' '%}supported'' 'package'' 'client{%'' 'else'' '%}package'' 'type'' 'enabled'' 'for'' 'your'' 'instance{%'' 'endif'' '%}'' 'by'' 'following'' 'the'' 'same'' 'general'' 'guidelines.1.'' 'Create'' 'or'' 'use'' 'an'' 'existing'' 'access'' 'token'' 'with'' 'the'' 'appropriate'' 'scopes'' 'for'' 'the'' 'task'' 'you'' 'want'' 'to'' 'accomplish.'' 'For'' 'more'' 'information,'' 'see'' '"[About'' 'permissions'' 'for'' '{%'' 'data'' 'variables.product.prodname_registry'' '%}](/packages/learn''
'-github''
'-packages/about''
'-permissions''
'-for''
'-github''
'-packages)."
2.'' 'Authenticate'' 'to'' '{%'' 'data'' 'variables.product.prodname_registry'' '%}'' 'using'' 'your'' 'access'' 'token'' 'and'' 'the'' 'instructions'' 'for'' 'your'' 'package'' 'client.
1.'' 'Create'' 'or'' 'use'' 'an'' 'existing'' '{%'' 'data'' 'variables.product.pat_v1'' '%}'' 'with'' 'the'' 'appropriate'' 'scopes'' 'for'' 'the'' 'task'' 'you'' 'want'' 'to'' 'accomplish.'' 'For'' 'more'' 'information,'' 'see'' '"[About'' 'permissions'' 'for'' '{%'' 'data'' 'variables.product.prodname_registry'' '%}](/packages/learn''
'-github''
'-packages/about''
'-permissions''
'-for''
'-github''
'-packages)."
2.'' 'Authenticate'' 'to'' '{%'' 'data'' 'variables.product.prodname_registry'' '%}'' 'using'' 'your'' '{%'' 'data'' 'variables.product.pat_v1'' '%}'' 'and'' 'the'' 'instructions'' 'for'' 'your'' 'package'' 'client.
3.'' 'Publish'' 'the'' 'package'' 'using'' 'the'' 'instructions'' 'for'' 'your'' 'package'' 'client.For'' 'instructions'' 'specific'' 'to'' 'your'' 'package'' 'client,'' 'see'' '"[Working'' 'with'' 'a'' 'GitHub'' 'Packages'' 'registry](/packages/working''
'-with''
'-a''
'-github''
'-packages''
'-registry)."
'' ''' '14'' ''' '
...ub''
'-actions''
'-workflows/publishing''
'-and''
'-installing''
'-a''
'-package''
'-with''
'-github''
'-actions.md
'@'@'' '''
'-32,7'' '+32,7'' ''@'@'' 'You'' 'can'' 'extend'' 'the'' 'CI'' 'and'' 'CD'' 'capabilities'' 'of'' 'your'' 'repository'' 'by'' 'publishing'' 'or'' 'in###'' 'Authenticating'' 'to'' 'package'' 'registries'' 'on'' '{%'' 'data'' 'variables.product.prodname_dotcom'' '%}{%'' 'ifversion'' 'fpt'' 'or'' 'ghec'' '%}If'' 'you'' 'want'' 'your'' 'workflow'' 'to'' 'authenticate'' 'to'' '{%'' 'data'' 'variables.product.prodname_registry'' '%}'' 'to'' 'access'' 'a'' 'package'' 'registry'' 'other'' 'than'' 'the'' '{%'' 'data'' 'variables.product.prodname_container_registry'' '%}'' 'on'' '{%'' 'data'' 'variables.location.product_location'' '%},'' 'then{%'' 'else'' '%}To'' 'authenticate'' 'to'' 'package'' 'registries'' 'on'' '{%'' 'data'' 'variables.product.product_name'' '%},{%'' 'endif'' '%}'' 'we'' 'recommend'' 'using'' 'the'' '`GITHUB_TOKEN`'' 'that'' '{%'' 'data'' 'variables.product.product_name'' '%}'' 'automatically'' 'creates'' 'for'' 'your'' 'repository'' 'when'' 'you'' 'enable'' '{%'' 'data'' 'variables.product.prodname_actions'' '%}'' 'instead'' 'of'' 'a'' 'personal'' 'access'' 'token'' 'for'' 'authentication.'' 'You'' 'should'' 'set'' 'the'' 'permissions'' 'for'' 'this'' 'access'' 'token'' 'in'' 'the'' 'workflow'' 'file'' 'to'' 'grant'' 'read'' 'access'' 'for'' 'the'' '`contents`'' 'scope'' 'and'' 'write'' 'access'' 'for'' 'the'' '`packages`'' 'scope.'' 'For'' 'forks,'' 'the'' '`GITHUB_TOKEN`'' 'is'' 'granted'' 'read'' 'access'' 'for'' 'the'' 'parent'' 'repository.'' 'For'' 'more'' 'information,'' 'see'' '"[Authenticating'' 'with'' 'the'' 'GITHUB_TOKEN](/actions/configuring''
'-and''
'-managing''
'-workflows/authenticating''
'-with''
'-the''
'-github_token)."
{%'' 'ifversion'' 'fpt'' 'or'' 'ghec'' '%}If'' 'you'' 'want'' 'your'' 'workflow'' 'to'' 'authenticate'' 'to'' '{%'' 'data'' 'variables.product.prodname_registry'' '%}'' 'to'' 'access'' 'a'' 'package'' 'registry'' 'other'' 'than'' 'the'' '{%'' 'data'' 'variables.product.prodname_container_registry'' '%}'' 'on'' '{%'' 'data'' 'variables.location.product_location'' '%},'' 'then{%'' 'else'' '%}To'' 'authenticate'' 'to'' 'package'' 'registries'' 'on'' '{%'' 'data'' 'variables.product.product_name'' '%},{%'' 'endif'' '%}'' 'we'' 'recommend'' 'using'' 'the'' '`GITHUB_TOKEN`'' 'that'' '{%'' 'data'' 'variables.product.product_name'' '%}'' 'automatically'' 'creates'' 'for'' 'your'' 'repository'' 'when'' 'you'' 'enable'' '{%'' 'data'' 'variables.product.prodname_actions'' '%}'' 'instead'' 'of'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'for'' 'authentication.'' 'You'' 'should'' 'set'' 'the'' 'permissions'' 'for'' 'this'' 'access'' 'token'' 'in'' 'the'' 'workflow'' 'file'' 'to'' 'grant'' 'read'' 'access'' 'for'' 'the'' '`contents`'' 'scope'' 'and'' 'write'' 'access'' 'for'' 'the'' '`packages`'' 'scope.'' 'For'' 'forks,'' 'the'' '`GITHUB_TOKEN`'' 'is'' 'granted'' 'read'' 'access'' 'for'' 'the'' 'parent'' 'repository.'' 'For'' 'more'' 'information,'' 'see'' '"[Authenticating'' 'with'' 'the'' 'GITHUB_TOKEN](/actions/configuring''
'-and''
'-managing''
'-workflows/authenticating''
'-with''
'-the''
'-github_token)."You'' 'can'' 'reference'' 'the'' '`GITHUB_TOKEN`'' 'in'' 'your'' 'workflow'' 'file'' 'using'' 'the'' '{%'' 'raw'' '%}`{{secrets.GITHUB_TOKEN}}`{%'' 'endraw'' '%}'' 'context.'' 'For'' 'more'' 'information,'' 'see'' '"[Authenticating'' 'with'' 'the'' 'GITHUB_TOKEN](/actions/automating''
'-your''
'-workflow''
'-with''
'-github''
'-actions/authenticating''
'-with''
'-the''
'-github_token)."'@'@'' '''
'-53,7'' '+53,7'' ''@'@'' 'When'' 'you'' 'enable'' 'GitHub'' 'Actions,'' 'GitHub'' 'installs'' 'a'' 'GitHub'' 'App'' 'on'' 'your'' 'repository.The'' '{%'' 'data'' 'variables.packages.prodname_ghcr_and_npm_registry_full'' '%}'' 'allows'' 'users'' 'to'' 'create'' 'and'' 'administer'' 'packages'' 'as'' 'free''
'-standing'' 'resources'' 'at'' 'the'' 'organization'' 'level.'' 'Packages'' 'can'' 'be'' 'owned'' 'by'' 'an'' 'organization'' 'or'' 'personal'' 'account'' 'and'' 'you'' 'can'' 'customize'' 'access'' 'to'' 'each'' 'of'' 'your'' 'packages'' 'separately'' 'from'' 'repository'' 'permissions.All'' 'workflows'' 'accessing'' 'the'' '{%'' 'data'' 'variables.packages.prodname_ghcr_and_npm_registry'' '%}'' 'should'' 'use'' 'the'' '`GITHUB_TOKEN`'' 'instead'' 'of'' 'a'' 'personal'' 'access'' 'token.'' 'For'' 'more'' 'information'' 'about'' 'security'' 'best'' 'practices,'' 'see'' '"[Security'' 'hardening'' 'for'' 'GitHub'' 'Actions](/actions/learn''
'-github''
'-actions/security''
'-hardening''
'-for''
'-github''
'-actions#using''
'-secrets)."
All'' 'workflows'' 'accessing'' 'the'' '{%'' 'data'' 'variables.packages.prodname_ghcr_and_npm_registry'' '%}'' 'should'' 'use'' 'the'' '`GITHUB_TOKEN`'' 'instead'' 'of'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}.'' 'For'' 'more'' 'information'' 'about'' 'security'' 'best'' 'practices,'' 'see'' '"[Security'' 'hardening'' 'for'' 'GitHub'' 'Actions](/actions/learn''
'-github''
'-actions/security''
'-hardening''
'-for''
'-github''
'-actions#using''
'-secrets)."##'' 'Default'' 'permissions'' 'and'' 'access'' 'settings'' 'for'' 'containers'' 'modified'' 'through'' 'workflows'@'@'' '''
'-484,13'' '+484,13'' ''@'@'' 'Installing'' 'packages'' 'hosted'' 'by'' '{%'' 'data'' 'variables.product.prodname_registry'' '%}'' 'thr
{%'' 'data'' 'reusables.package_registry.actions''
'-configuration'' '%}{%'' 'ifversion'' 'fpt'' 'or'' 'ghec'' '%}
##'' 'Upgrading'' 'a'' 'workflow'' 'that'' 'accesses'' 'a'' 'registry'' 'using'' 'a'' 'PAT
##'' 'Upgrading'' 'a'' 'workflow'' 'that'' 'accesses'' 'a'' 'registry'' 'using'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}The'' '{%'' 'data'' 'variables.packages.prodname_ghcr_and_npm_registry'' '%}'' 'support'' 'the'' '`GITHUB_TOKEN`'' 'for'' 'easy'' 'and'' 'secure'' 'authentication'' 'in'' 'your'' 'workflows.'' 'If'' 'your'' 'workflow'' 'is'' 'using'' 'a'' 'personal'' 'access'' 'token'' '(PAT)'' 'to'' 'authenticate'' 'to'' 'the'' 'registry,'' 'then'' 'we'' 'highly'' 'recommend'' 'you'' 'update'' 'your'' 'workflow'' 'to'' 'use'' 'the'' '`GITHUB_TOKEN`.
The'' '{%'' 'data'' 'variables.packages.prodname_ghcr_and_npm_registry'' '%}'' 'support'' 'the'' '`GITHUB_TOKEN`'' 'for'' 'easy'' 'and'' 'secure'' 'authentication'' 'in'' 'your'' 'workflows.'' 'If'' 'your'' 'workflow'' 'is'' 'using'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'to'' 'authenticate'' 'to'' 'the'' 'registry,'' 'then'' 'we'' 'highly'' 'recommend'' 'you'' 'update'' 'your'' 'workflow'' 'to'' 'use'' 'the'' '`GITHUB_TOKEN`.For'' 'more'' 'information'' 'about'' 'the'' '`GITHUB_TOKEN`,'' 'see'' '"[Authentication'' 'in'' 'a'' 'workflow](/actions/reference/authentication''
'-in''
'-a''
'-workflow#using''
'-the''
'-github_token''
'-in''
'-a''
'-workflow)."Using'' 'the'' '`GITHUB_TOKEN`'' 'instead'' 'of'' 'a'' 'PAT,'' 'which'' 'includes'' 'the'' '`repo`'' 'scope,'' 'increases'' 'the'' 'security'' 'of'' 'your'' 'repository'' 'as'' 'you'' 'don't'' 'need'' 'to'' 'use'' 'a'' 'long''
'-lived'' 'PAT'' 'that'' 'offers'' 'unnecessary'' 'access'' 'to'' 'the'' 'repository'' 'where'' 'your'' 'workflow'' 'is'' 'run.'' 'For'' 'more'' 'information'' 'about'' 'security'' 'best'' 'practices,'' 'see'' '"[Security'' 'hardening'' 'for'' 'GitHub'' 'Actions](/actions/learn''
'-github''
'-actions/security''
'-hardening''
'-for''
'-github''
'-actions#using''
'-secrets)."
Using'' 'the'' '`GITHUB_TOKEN`'' 'instead'' 'of'' 'a'' '{%'' 'data'' 'variables.product.pat_v1'' '%},'' 'which'' 'includes'' 'the'' '`repo`'' 'scope,'' 'increases'' 'the'' 'security'' 'of'' 'your'' 'repository'' 'as'' 'you'' 'don't'' 'need'' 'to'' 'use'' 'a'' 'long''
'-lived'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'that'' 'offers'' 'unnecessary'' 'access'' 'to'' 'the'' 'repository'' 'where'' 'your'' 'workflow'' 'is'' 'run.'' 'For'' 'more'' 'information'' 'about'' 'security'' 'best'' 'practices,'' 'see'' '"[Security'' 'hardening'' 'for'' 'GitHub'' 'Actions](/actions/learn''
'-github''
'-actions/security''
'-hardening''
'-for''
'-github''
'-actions#using''
'-secrets)."1.'' 'Navigate'' 'to'' 'your'' 'package'' 'landing'' 'page.
1.'' 'In'' 'the'' 'left'' 'sidebar,'' 'click'' '**Actions'' 'access**.
'@'@'' '''
'-504,7'' '+504,7'' ''@'@'' 'Using'' 'the'' '`GITHUB_TOKEN`'' 'instead'' 'of'' 'a'' 'PAT,'' 'which'' 'includes'' 'the'' '`repo`'' 'scope,'' 'incr
'' ''' '{%'' 'endnote'' '%}
1.'' 'Optionally,'' 'using'' 'the'' '"role"'' 'drop''
'-down'' 'menu,'' 'select'' 'the'' 'default'' 'access'' 'level'' 'that'' 'you'd'' 'like'' 'the'' 'repository'' 'to'' 'have'' 'to'' 'your'' 'container'' 'image.
'' ''' '![Permission'' 'access'' 'levels'' 'to'' 'give'' 'to'' 'repositories](/assets/images/help/package''
'-registry/repository''
'-permission''
'-options''
'-for''
'-package''
'-access''
'-through''
'-actions.png)
1.'' 'Open'' 'your'' 'workflow'' 'file.'' 'On'' 'the'' 'line'' 'where'' 'you'' 'log'' 'in'' 'to'' 'the'' 'registry,'' 'replace'' 'your'' 'PAT'' 'with'' '{%'' 'raw'' '%}`${{'' 'secrets.GITHUB_TOKEN'' '}}`{%'' 'endraw'' '%}.
1.'' 'Open'' 'your'' 'workflow'' 'file.'' 'On'' 'the'' 'line'' 'where'' 'you'' 'log'' 'in'' 'to'' 'the'' 'registry,'' 'replace'' 'your'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'with'' '{%'' 'raw'' '%}`${{'' 'secrets.GITHUB_TOKEN'' '}}`{%'' 'endraw'' '%}.For'' 'example,'' 'this'' 'workflow'' 'publishes'' 'a'' 'Docker'' 'image'' 'to'' 'the'' '{%'' 'data'' 'variables.product.prodname_container_registry'' '%}'' 'and'' 'uses'' '{%'' 'raw'' '%}`${{'' 'secrets.GITHUB_TOKEN'' '}}`{%'' 'endraw'' '%}'' 'to'' 'authenticate.'@'@'' '''
'-544,7'' '+544,7'' ''@'@'' 'jobs:
'' ''' ''' ''' ''' ''' ''' ''' 'run:'' 'docker'' 'build'' '.'' '''
'-file'' 'Dockerfile'' '''
'-tag'' '$IMAGE_NAME'' '''
'-label'' '"runnumber=${GITHUB_RUN_ID}"'' ''' ''' ''' ''' ''' ''' 'name:'' 'Log'' 'in'' 'to'' 'registry
'' ''' ''' ''' ''' ''' ''' ''' '#'' 'This'' 'is'' 'where'' 'you'' 'will'' 'update'' 'the'' 'PAT'' 'to'' 'GITHUB_TOKEN
'' ''' ''' ''' ''' ''' ''' ''' '#'' 'This'' 'is'' 'where'' 'you'' 'will'' 'update'' 'the'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'to'' 'GITHUB_TOKEN
'' ''' ''' ''' ''' ''' ''' ''' 'run:'' 'echo'' '"{%'' 'raw'' '%}${{'' 'secrets.GITHUB_TOKEN'' '}}{%'' 'endraw'' '%}"'' '|'' 'docker'' 'login'' 'ghcr.io'' '''
'-u'' '${{'' 'github.actor'' '}}'' '''
'-password''
'-stdin'' ''' ''' ''' ''' ''' ''' 'name:'' 'Push'' 'image
'' ''' '6'' ''' '
...rking''
'-with''
'-a''
'-github''
'-packages''
'-registry/working''
'-with''
'-the''
'-apache''
'-maven''
'-registry.md
'@'@'' '''
'-27,13'' '+27,13'' ''@'@'' 'shortTitle:'' 'Apache'' 'Maven'' 'registry{%'' 'data'' 'reusables.package_registry.authenticate''
'-packages''
'-github''
'-token'' '%}###'' 'Authenticating'' 'with'' 'a'' 'personal'' 'access'' 'token
###'' 'Authenticating'' 'with'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}{%'' 'data'' 'reusables.package_registry.required''
'-scopes'' '%}You'' 'can'' 'authenticate'' 'to'' '{%'' 'data'' 'variables.product.prodname_registry'' '%}'' 'with'' 'Apache'' 'Maven'' 'by'' 'editing'' 'your'' '*~/.m2/settings.xml*'' 'file'' 'to'' 'include'' 'your'' 'personal'' 'access'' 'token.'' 'Create'' 'a'' 'new'' '*~/.m2/settings.xml*'' 'file'' 'if'' 'one'' 'doesn't'' 'exist.
You'' 'can'' 'authenticate'' 'to'' '{%'' 'data'' 'variables.product.prodname_registry'' '%}'' 'with'' 'Apache'' 'Maven'' 'by'' 'editing'' 'your'' '*~/.m2/settings.xml*'' 'file'' 'to'' 'include'' 'your'' '{%'' 'data'' 'variables.product.pat_v1'' '%}.'' 'Create'' 'a'' 'new'' '*~/.m2/settings.xml*'' 'file'' 'if'' 'one'' 'doesn't'' 'exist.In'' 'the'' '`servers`'' 'tag,'' 'add'' 'a'' 'child'' '`server`'' 'tag'' 'with'' 'an'' '`id`,'' 'replacing'' '*USERNAME*'' 'with'' 'your'' '{%'' 'data'' 'variables.product.prodname_dotcom'' '%}'' 'username,'' 'and'' '*TOKEN*'' 'with'' 'your'' 'personal'' 'access'' 'token.
In'' 'the'' '`servers`'' 'tag,'' 'add'' 'a'' 'child'' '`server`'' 'tag'' 'with'' 'an'' '`id`,'' 'replacing'' '*USERNAME*'' 'with'' 'your'' '{%'' 'data'' 'variables.product.prodname_dotcom'' '%}'' 'username,'' 'and'' '*TOKEN*'' 'with'' 'your'' '{%'' 'data'' 'variables.product.pat_generic'' '%}.In'' 'the'' '`repositories`'' 'tag,'' 'configure'' 'a'' 'repository'' 'by'' 'mapping'' 'the'' '`id`'' 'of'' 'the'' 'repository'' 'to'' 'the'' '`id`'' 'you'' 'added'' 'in'' 'the'' '`server`'' 'tag'' 'containing'' 'your'' 'credentials.'' 'Replace'' '{%'' 'ifversion'' 'ghes'' 'or'' 'ghae'' '%}*HOSTNAME*'' 'with'' 'the'' 'host'' 'name'' 'of'' '{%'' 'data'' 'variables.location.product_location'' '%},'' 'and{%'' 'endif'' '%}'' '*OWNER*'' 'with'' 'the'' 'name'' 'of'' 'the'' 'user'' 'or'' 'organization'' 'account'' 'that'' 'owns'' 'the'' 'repository.'' 'Because'' 'uppercase'' 'letters'' 'aren't'' 'supported,'' 'you'' 'must'' 'use'' 'lowercase'' 'letters'' 'for'' 'the'' 'repository'' 'owner'' 'even'' 'if'' 'the'' '{%'' 'data'' 'variables.product.prodname_dotcom'' '%}'' 'user'' 'or'' 'organization'' 'name'' 'contains'' 'uppercase'' 'letters.'' ''' '6'' ''' '
...ges/working''
'-with''
'-a''
'-github''
'-packages''
'-registry/working''
'-with''
'-the''
'-docker''
'-registry.md
'@'@'' '''
'-42,13'' '+42,13'' ''@'@'' 'When'' 'installing'' 'or'' 'publishing'' 'a'' 'Docker'' 'image,'' 'the'' 'Docker'' 'registry'' 'does'' 'not'' 'curre{%'' 'data'' 'reusables.package_registry.authenticate''
'-packages''
'-github''
'-token'' '%}###'' 'Authenticating'' 'with'' 'a'' 'personal'' 'access'' 'token
###'' 'Authenticating'' 'with'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}{%'' 'data'' 'reusables.package_registry.required''
'-scopes'' '%}You'' 'can'' 'authenticate'' 'to'' '{%'' 'data'' 'variables.product.prodname_registry'' '%}'' 'with'' 'Docker'' 'using'' 'the'' '`docker`'' 'login'' 'command.To'' 'keep'' 'your'' 'credentials'' 'secure,'' 'we'' 'recommend'' 'you'' 'save'' 'your'' 'personal'' 'access'' 'token'' 'in'' 'a'' 'local'' 'file'' 'on'' 'your'' 'computer'' 'and'' 'use'' 'Docker's'' '`''
'-password''
'-stdin`'' 'flag,'' 'which'' 'reads'' 'your'' 'token'' 'from'' 'a'' 'local'' 'file.
To'' 'keep'' 'your'' 'credentials'' 'secure,'' 'we'' 'recommend'' 'you'' 'save'' 'your'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'in'' 'a'' 'local'' 'file'' 'on'' 'your'' 'computer'' 'and'' 'use'' 'Docker's'' '`''
'-password''
'-stdin`'' 'flag,'' 'which'' 'reads'' 'your'' 'token'' 'from'' 'a'' 'local'' 'file.{%'' 'ifversion'' 'fpt'' 'or'' 'ghec'' '%}
{%'' 'raw'' '%}
'@'@'' '''
'-79,7'' '+79,7'' ''@'@'' 'If'' 'your'' 'instance'' 'has'' 'subdomain'' 'isolation'' 'disabled:{%'' 'endif'' '%}To'' 'use'' 'this'' 'example'' 'login'' 'command,'' 'replace'' '`USERNAME`'' 'with'' 'your'' '{%'' 'data'' 'variables.product.product_name'' '%}'' 'username{%'' 'ifversion'' 'ghes'' 'or'' 'ghae'' '%},'' '`HOSTNAME`'' 'with'' 'the'' 'URL'' 'for'' '{%'' 'data'' 'variables.location.product_location'' '%},{%'' 'endif'' '%}'' 'and'' '`~/TOKEN.txt`'' 'with'' 'the'' 'file'' 'path'' 'to'' 'your'' 'personal'' 'access'' 'token'' 'for'' '{%'' 'data'' 'variables.product.product_name'' '%}.
To'' 'use'' 'this'' 'example'' 'login'' 'command,'' 'replace'' '`USERNAME`'' 'with'' 'your'' '{%'' 'data'' 'variables.product.product_name'' '%}'' 'username{%'' 'ifversion'' 'ghes'' 'or'' 'ghae'' '%},'' '`HOSTNAME`'' 'with'' 'the'' 'URL'' 'for'' '{%'' 'data'' 'variables.location.product_location'' '%},{%'' 'endif'' '%}'' 'and'' '`~/TOKEN.txt`'' 'with'' 'the'' 'file'' 'path'' 'to'' 'your'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'for'' '{%'' 'data'' 'variables.product.product_name'' '%}.For'' 'more'' 'information,'' 'see'' '"[Docker'' 'login](https://docs.docker.com/engine/reference/commandline/login/#provide''
'-a''
'-password''
'-using''
'-stdin)."'' ''' '6'' ''' '
...ges/working''
'-with''
'-a''
'-github''
'-packages''
'-registry/working''
'-with''
'-the''
'-gradle''
'-registry.md
'@'@'' '''
'-27,19'' '+27,19'' ''@'@'' 'shortTitle:'' 'Gradle'' 'registry{%'' 'data'' 'reusables.package_registry.authenticate''
'-packages''
'-github''
'-token'' '%}'' 'For'' 'more'' 'information'' 'about'' 'using'' '`GITHUB_TOKEN`'' 'with'' 'Gradle,'' 'see'' '"[Publishing'' 'Java'' 'packages'' 'with'' 'Gradle](/actions/guides/publishing''
'-java''
'-packages''
'-with''
'-gradle#publishing''
'-packages''
'-to''
'-github''
'-packages)."###'' 'Authenticating'' 'with'' 'a'' 'personal'' 'access'' 'token
###'' 'Authenticating'' 'with'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}{%'' 'data'' 'reusables.package_registry.required''
'-scopes'' '%}You'' 'can'' 'authenticate'' 'to'' '{%'' 'data'' 'variables.product.prodname_registry'' '%}'' 'with'' 'Gradle'' 'using'' 'either'' 'Gradle'' 'Groovy'' 'or'' 'Kotlin'' 'DSL'' 'by'' 'editing'' 'your'' '*build.gradle*'' 'file'' '(Gradle'' 'Groovy)'' 'or'' '*build.gradle.kts*'' 'file'' '(Kotlin'' 'DSL)'' 'file'' 'to'' 'include'' 'your'' 'personal'' 'access'' 'token.'' 'You'' 'can'' 'also'' 'configure'' 'Gradle'' 'Groovy'' 'and'' 'Kotlin'' 'DSL'' 'to'' 'recognize'' 'a'' 'single'' 'package'' 'or'' 'multiple'' 'packages'' 'in'' 'a'' 'repository.
You'' 'can'' 'authenticate'' 'to'' '{%'' 'data'' 'variables.product.prodname_registry'' '%}'' 'with'' 'Gradle'' 'using'' 'either'' 'Gradle'' 'Groovy'' 'or'' 'Kotlin'' 'DSL'' 'by'' 'editing'' 'your'' '*build.gradle*'' 'file'' '(Gradle'' 'Groovy)'' 'or'' '*build.gradle.kts*'' 'file'' '(Kotlin'' 'DSL)'' 'file'' 'to'' 'include'' 'your'' '{%'' 'data'' 'variables.product.pat_v1'' '%}.'' 'You'' 'can'' 'also'' 'configure'' 'Gradle'' 'Groovy'' 'and'' 'Kotlin'' 'DSL'' 'to'' 'recognize'' 'a'' 'single'' 'package'' 'or'' 'multiple'' 'packages'' 'in'' 'a'' 'repository.{%'' 'ifversion'' 'ghes'' '%}
Replace'' '*REGISTRY''
'-URL*'' 'with'' 'the'' 'URL'' 'for'' 'your'' 'instance's'' 'Maven'' 'registry.'' 'If'' 'your'' 'instance'' 'has'' 'subdomain'' 'isolation'' 'enabled,'' 'use'' '`maven.HOSTNAME`.'' 'If'' 'your'' 'instance'' 'has'' 'subdomain'' 'isolation'' 'disabled,'' 'use'' '`HOSTNAME/_registry/maven`.'' 'In'' 'either'' 'case,'' 'replace'' '*HOSTNAME*'' 'with'' 'the'' 'host'' 'name'' 'of'' 'your'' '{%'' 'data'' 'variables.product.prodname_ghe_server'' '%}'' 'instance.
{%'' 'elsif'' 'ghae'' '%}
Replace'' '*REGISTRY''
'-URL*'' 'with'' 'the'' 'URL'' 'for'' 'your'' 'enterprise's'' 'Maven'' 'registry,'' '`maven.HOSTNAME`.'' 'Replace'' '*HOSTNAME*'' 'with'' 'the'' 'host'' 'name'' 'of'' '{%'' 'data'' 'variables.location.product_location'' '%}.
{%'' 'endif'' '%}Replace'' '*USERNAME*'' 'with'' 'your'' '{%'' 'data'' 'variables.product.prodname_dotcom'' '%}'' 'username,'' '*TOKEN*'' 'with'' 'your'' 'personal'' 'access'' 'token,'' '*REPOSITORY*'' 'with'' 'the'' 'name'' 'of'' 'the'' 'repository'' 'containing'' 'the'' 'package'' 'you'' 'want'' 'to'' 'publish,'' 'and'' '*OWNER*'' 'with'' 'the'' 'name'' 'of'' 'the'' 'user'' 'or'' 'organization'' 'account'' 'on'' '{%'' 'data'' 'variables.product.prodname_dotcom'' '%}'' 'that'' 'owns'' 'the'' 'repository.'' 'Because'' 'uppercase'' 'letters'' 'aren't'' 'supported,'' 'you'' 'must'' 'use'' 'lowercase'' 'letters'' 'for'' 'the'' 'repository'' 'owner'' 'even'' 'if'' 'the'' '{%'' 'data'' 'variables.product.prodname_dotcom'' '%}'' 'user'' 'or'' 'organization'' 'name'' 'contains'' 'uppercase'' 'letters.
Replace'' '*USERNAME*'' 'with'' 'your'' '{%'' 'data'' 'variables.product.prodname_dotcom'' '%}'' 'username,'' '*TOKEN*'' 'with'' 'your'' '{%'' 'data'' 'variables.product.pat_v1'' '%},'' '*REPOSITORY*'' 'with'' 'the'' 'name'' 'of'' 'the'' 'repository'' 'containing'' 'the'' 'package'' 'you'' 'want'' 'to'' 'publish,'' 'and'' '*OWNER*'' 'with'' 'the'' 'name'' 'of'' 'the'' 'user'' 'or'' 'organization'' 'account'' 'on'' '{%'' 'data'' 'variables.product.prodname_dotcom'' '%}'' 'that'' 'owns'' 'the'' 'repository.'' 'Because'' 'uppercase'' 'letters'' 'aren't'' 'supported,'' 'you'' 'must'' 'use'' 'lowercase'' 'letters'' 'for'' 'the'' 'repository'' 'owner'' 'even'' 'if'' 'the'' '{%'' 'data'' 'variables.product.prodname_dotcom'' '%}'' 'user'' 'or'' 'organization'' 'name'' 'contains'' 'uppercase'' 'letters.{%'' 'note'' '%}'' ''' '8'' ''' '
...ckages/working''
'-with''
'-a''
'-github''
'-packages''
'-registry/working''
'-with''
'-the''
'-npm''
'-registry.md
'@'@'' '''
'-42,13'' '+42,13'' ''@'@'' 'If'' 'you'' 'reach'' 'this'' 'limit,'' 'consider'' 'deleting'' 'package'' 'versions'' 'or'' 'contact'' 'Support'' 'f
You'' 'can'' 'also'' 'choose'' 'to'' 'give'' 'access'' 'permissions'' 'to'' 'packages'' 'independently'' 'for'' '{%'' 'data'' 'variables.product.prodname_codespaces'' '%}'' 'and'' '{%'' 'data'' 'variables.product.prodname_actions'' '%}.'' 'For'' 'more'' 'information,'' 'see'' '"[Ensuring'' 'Codespaces'' 'access'' 'to'' 'your'' 'package](/packages/learn''
'-github''
'-packages/configuring''
'-a''
'-packages''
'-access''
'-control''
'-and''
'-visibility#ensuring''
'-codespaces''
'-access''
'-to''
'-your''
'-package)'' 'and'' '[Ensuring'' 'workflow'' 'access'' 'to'' 'your'' 'package](/packages/learn''
'-github''
'-packages/configuring''
'-a''
'-packages''
'-access''
'-control''
'-and''
'-visibility#ensuring''
'-workflow''
'-access''
'-to''
'-your''
'-package)."
{%'' 'endif'' '%}###'' 'Authenticating'' 'with'' 'a'' 'personal'' 'access'' 'token
###'' 'Authenticating'' 'with'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}{%'' 'data'' 'reusables.package_registry.required''
'-scopes'' '%}You'' 'can'' 'authenticate'' 'to'' '{%'' 'data'' 'variables.product.prodname_registry'' '%}'' 'with'' 'npm'' 'by'' 'either'' 'editing'' 'your'' 'per''
'-user'' '*~/.npmrc*'' 'file'' 'to'' 'include'' 'your'' 'personal'' 'access'' 'token'' 'or'' 'by'' 'logging'' 'in'' 'to'' 'npm'' 'on'' 'the'' 'command'' 'line'' 'using'' 'your'' 'username'' 'and'' 'personal'' 'access'' 'token.
You'' 'can'' 'authenticate'' 'to'' '{%'' 'data'' 'variables.product.prodname_registry'' '%}'' 'with'' 'npm'' 'by'' 'either'' 'editing'' 'your'' 'per''
'-user'' '*~/.npmrc*'' 'file'' 'to'' 'include'' 'your'' '{%'' 'data'' 'variables.product.pat_v1'' '%}'' 'or'' 'by'' 'logging'' 'in'' 'to'' 'npm'' 'on'' 'the'' 'command'' 'line'' 'using'' 'your'' 'username'' 'and'' '{%'' 'data'' 'variables.product.pat_generic'' '%}.To'' 'authenticate'' 'by'' 'adding'' 'your'' 'personal'' 'access'' 'token'' 'to'' 'your'' '*~/.npmrc*'' 'file,'' 'edit'' 'the'' '*~/.npmrc*'' 'file'' 'for'' 'your'' 'project'' 'to'' 'include'' 'the'' 'following'' 'line,'' 'replacing'' '{%'' 'ifversion'' 'ghes'' 'or'' 'ghae'' '%}*HOSTNAME*'' 'with'' 'the'' 'host'' 'name'' 'of'' '{%'' 'data'' 'variables.location.product_location'' '%}'' 'and'' '{%'' 'endif'' '%}*TOKEN*'' 'with'' 'your'' 'personal'' 'access'' 'token.'' 'Create'' 'a'' 'new'' '*~/.npmrc*'' 'file'' 'if'' 'one'' 'doesn't'' 'exist.
To'' 'authenticate'' 'by'' 'adding'' 'your'' '{%'' 'data'' 'variables.product.pat_v1'' '%}'' 'to'' 'your'' '*~/.npmrc*'' 'file,'' 'edit'' 'the'' '*~/.npmrc*'' 'file'' 'for'' 'your'' 'project'' 'to'' 'include'' 'the'' 'following'' 'line,'' 'replacing'' '{%'' 'ifversion'' 'ghes'' 'or'' 'ghae'' '%}*HOSTNAME*'' 'with'' 'the'' 'host'' 'name'' 'of'' '{%'' 'data'' 'variables.location.product_location'' '%}'' 'and'' '{%'' 'endif'' '%}*TOKEN*'' 'with'' 'your'' '{%'' 'data'' 'variables.product.pat_generic'' '%}.'' 'Create'' 'a'' 'new'' '*~/.npmrc*'' 'file'' 'if'' 'one'' 'doesn't'' 'exist.{%'' 'ifversion'' 'ghes'' '%}
If'' 'your'' 'instance'' 'has'' 'subdomain'' 'isolation'' 'enabled:
'@'@'' '''
'-66,7'' '+66,7'' ''@'@'' 'If'' 'your'' 'instance'' 'has'' 'subdomain'' 'isolation'' 'disabled:
{%'' 'endif'' '%}To'' 'authenticate'' 'by'' 'logging'' 'in'' 'to'' 'npm,'' 'use'' 'the'' 'npm'' 'login'' 'command,'' 'replacing'' 'USERNAME'' 'with'' 'your'' '{%'' 'data'' 'variables.product.prodname_dotcom'' '%}'' 'username,'' 'TOKEN'' 'with'' 'your'' 'personal'' 'access'' 'token,'' 'and'' 'PUBLIC''
'-EMAIL''
'-ADDRESS'' 'with'' 'your'' 'email'' 'address.'' 'To'' 'authenticate'' 'by'' 'logging'' 'in'' 'to'' 'npm,'' 'use'' 'the'' 'npm'' 'login'' 'command,'' 'replacing'' 'USERNAME'' 'with'' 'your'' '{%'' 'data'' 'variables.product.prodname_dotcom'' '%}'' 'username,'' 'TOKEN'' 'with'' 'your'' '{%'' 'data'' 'variables.product.pat_v1'' '%},'' 'and'' 'PUBLIC''
'-EMAIL''
'-ADDRESS'' 'with'' 'your'' 'email'' 'address.If'' '{%'' 'data'' 'variables.product.prodname_registry'' '%}'' 'is'' 'not'' 'your'' 'default'' 'package'' 'registry'' 'for'' 'using'' 'npm'' 'and'' 'you'' 'want'' 'to'' 'use'' 'the'' 'npm'' 'audit'' 'command,'' 'we'' 'recommend'' 'you'' 'use'' 'the'' '''
'-scope'' 'flag'' 'with'' 'the'' 'owner'' 'of'' 'the'' 'package'' 'when'' 'you'' 'authenticate'' 'to'' '{%'' 'data'' 'variables.product.prodname_registry'' '%}.16
...ages/working''
'-with''
'-a''
'-github''
'-packages''
'-registry/working''
'-with''
'-the''
'-nuget''
'-registry.md'' ''@'@'' '''
'-28,23'' '+28,23'' ''@'@'' 'shortTitle:'' 'NuGet'' 'registryAuthenticating'' 'with'' 'GITHUB_TOKEN'' 'in'' '{%'' 'data'' 'variables.product.prodname_actions'' '%}
Use'' 'the'' 'following'' 'command'' 'to'' 'authenticate'' 'to'' '{%'' 'data'' 'variables.product.prodname_registry'' '%}'' 'in'' 'a'' '{%'' 'data'' 'variables.product.prodname_actions'' '%}'' 'workflow'' 'using'' 'the'' 'GITHUB_TOKEN'' 'instead'' 'of'' 'hardcoding'' 'a'' 'token'' 'in'' 'a'' 'nuget.config'' 'file'' 'in'' 'the'' 'repository:'' 'Use'' 'the'' 'following'' 'command'' 'to'' 'authenticate'' 'to'' '{%'' 'data'' 'variables.product.prodname_registry'' '%}'' 'in'' 'a'' '{%'' 'data'' 'variables.product.prodname_actions'' '%}'' 'workflow'' 'using'' 'the'' 'GITHUB_TOKEN'' 'instead'' 'of'' 'hardcoding'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'in'' 'a'' 'nuget.config'' 'file'' 'in'' 'the'' 'repository:dotnet'' 'nuget'' 'add'' 'source'' '''
'-username'' 'USERNAME'' '''
'-password'' '{%raw%}${{'' 'secrets.GITHUB_TOKEN'' '}}{%'' 'endraw'' '%}'' '''
'-store''
'-password''
'-in''
'-clear''
'-text'' '''
'-name'' 'github'' '"https://{%'' 'ifversion'' 'fpt'' 'or'' 'ghec'' '%}nuget.pkg.github.com{%'' 'else'' '%}nuget.HOSTNAME{%'' 'endif'' '%}/OWNER/index.json"
{%'' 'data'' 'reusables.package_registry.authenticate''
'-packages''
'-github''
'-token'' '%}Authenticating'' 'with'' 'a'' 'personal'' 'access'' 'token
Authenticating'' 'with'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}
{%'' 'data'' 'reusables.package_registry.required''
'-scopes'' '%}To'' 'authenticate'' 'to'' '{%'' 'data'' 'variables.product.prodname_registry'' '%}'' 'with'' 'the'' 'dotnet'' 'command''
'-line'' 'interface'' '(CLI),'' 'create'' 'a'' 'nuget.config'' 'file'' 'in'' 'your'' 'project'' 'directory'' 'specifying'' '{%'' 'data'' 'variables.product.prodname_registry'' '%}'' 'as'' 'a'' 'source'' 'under'' 'packageSources'' 'for'' 'the'' 'dotnet'' 'CLI'' 'client.You'' 'must'' 'replace:USERNAME'' 'with'' 'the'' 'name'' 'of'' 'your'' 'personal'' 'account'' 'on'' '{%'' 'data'' 'variables.product.prodname_dotcom'' '%}.
TOKEN'' 'with'' 'your'' 'personal'' 'access'' 'token.
TOKEN'' 'with'' 'your'' '{%'' 'data'' 'variables.product.pat_v1'' '%}.
OWNER'' 'with'' 'the'' 'name'' 'of'' 'the'' 'user'' 'or'' 'organization'' 'account'' 'that'' 'owns'' 'the'' 'repository'' 'containing'' 'your'' 'project.{%'' 'ifversion'' 'ghes'' 'or'' 'ghae'' '%}
HOSTNAME'' 'with'' 'the'' 'host'' 'name'' 'for'' '{%'' 'data'' 'variables.location.product_location'' '%}.{%'' 'endif'' '%}
'@'@'' '''
'-89,11'' '+89,11'' ''@'@'' 'If'' 'your'' 'instance'' 'has'' 'subdomain'' 'isolation'' 'disabled:Publishing'' 'a'' 'package
You'' 'can'' 'publish'' 'a'' 'package'' 'to'' '{%'' 'data'' 'variables.product.prodname_registry'' '%}'' 'by'' 'authenticating'' 'with'' 'a'' 'nuget.config'' 'file,'' 'or'' 'by'' 'using'' 'the'' '''
'-api''
'-key'' 'command'' 'line'' 'option'' 'with'' 'your'' '{%'' 'data'' 'variables.product.prodname_dotcom'' '%}'' 'personal'' 'access'' 'token'' '(PAT).'' 'You'' 'can'' 'publish'' 'a'' 'package'' 'to'' '{%'' 'data'' 'variables.product.prodname_registry'' '%}'' 'by'' 'authenticating'' 'with'' 'a'' 'nuget.config'' 'file,'' 'or'' 'by'' 'using'' 'the'' '''
'-api''
'-key'' 'command'' 'line'' 'option'' 'with'' 'your'' '{%'' 'data'' 'variables.product.prodname_dotcom'' '%}'' '{%'' 'data'' 'variables.product.pat_v1'' '%}.Publishing'' 'a'' 'package'' 'using'' 'a'' 'GitHub'' 'PAT'' 'as'' 'your'' 'API'' 'key
Publishing'' 'a'' 'package'' 'using'' 'a'' 'GitHub'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'as'' 'your'' 'API'' 'key
If'' 'you'' 'don't'' 'already'' 'have'' 'a'' 'PAT'' 'to'' 'use'' 'for'' 'your'' 'account'' 'on'' '{%'' 'ifversion'' 'ghae'' '%}{%'' 'data'' 'variables.product.product_name'' '%}{%'' 'else'' '%}{%'' 'data'' 'variables.location.product_location'' '%}{%'' 'endif'' '%},'' 'see'' '"Creating'' 'a'' 'personal'' 'access'' 'token."'' 'If'' 'you'' 'don't'' 'already'' 'have'' 'a'' 'PAT'' 'to'' 'use'' 'for'' 'your'' 'account'' 'on'' '{%'' 'ifversion'' 'ghae'' '%}{%'' 'data'' 'variables.product.product_name'' '%}{%'' 'else'' '%}{%'' 'data'' 'variables.location.product_location'' '%}{%'' 'endif'' '%},'' 'see'' '"Creating'' 'a'' '{%'' 'data'' 'variables.product.pat_generic'' '%}."Create'' 'a'' 'new'' 'project.
'@'@'' '''
'-104,7'' '+104,7'' ''@'@'' 'If'' 'you'' 'don't'' 'already'' 'have'' 'a'' 'PAT'' 'to'' 'use'' 'for'' 'your'' 'account'' 'on'' '{%'' 'ifversion'' 'ghae'' '%}{
dotnet'' 'pack'' '''
'-configuration'' 'Release
Publish'' 'the'' 'package'' 'using'' 'your'' 'PAT'' 'as'' 'the'' 'API'' 'key.
Publish'' 'the'' 'package'' 'using'' 'your'' '{%'' 'data'' 'variables.product.pat_generic'' '%}'' 'as'' 'the'' 'API'' 'key.
dotnet'' 'nuget'' 'push'' '"bin/Release/OctocatApp.1.0.0.nupkg"'' ''' '''
'-api''
'-key'' 'YOUR_GITHUB_PAT'' '''
'-source'' '"github"
'@'@'' '''
'-232,7'' '+232,7'' ''@'@'' 'Your'' 'NuGet'' 'package'' 'may'' 'fail'' 'to'' 'push'' 'if'' 'the'' 'RepositoryUrl'' 'in'' '.csproj'' 'is'' 'not'' 'sIf'' 'you're'' 'using'' 'a'' 'nuspec'' 'file,'' 'ensure'' 'that'' 'it'' 'has'' 'a'' 'repository'' 'element'' 'with'' 'the'' 'required'' 'type'' 'and'' 'url'' 'attributes.If'' 'you're'' 'using'' 'a'' 'GITHUB_TOKEN'' 'to'' 'authenticate'' 'to'' 'a'' '{%'' 'data'' 'variables.product.prodname_registry'' '%}'' 'registry'' 'within'' 'a'' '{%'' 'data'' 'variables.product.prodname_actions'' '%}'' 'workflow,'' 'the'' 'token'' 'cannot'' 'access'' 'private'' 'repository''
'-based'' 'packages'' 'in'' 'a'' 'different'' 'repository'' 'other'' 'than'' 'where'' 'the'' 'workflow'' 'is'' 'running'' 'in.'' 'To'' 'access'' 'packages'' 'associated'' 'with'' 'other'' 'repositories,'' 'instead'' 'generate'' 'a'' 'PAT'' 'with'' 'the'' 'read:packages'' 'scope'' 'and'' 'pass'' 'this'' 'token'' 'in'' 'as'' 'a'' 'secret.'' 'If'' 'you're'' 'using'' 'a'' 'GITHUB_TOKEN'' 'to'' 'authenticate'' 'to'' 'a'' '{%'' 'data'' 'variables.product.prodname_registry'' '%}'' 'registry'' 'within'' 'a'' '{%'' 'data'' 'variables.product.prodname_actions'' '%}'' 'workflow,'' 'the'' 'token'' 'cannot'' 'access'' 'private'' 'repository''
'-based'' 'packages'' 'in'' 'a'' 'different'' 'repository'' 'other'' 'than'' 'where'' 'the'' 'workflow'' 'is'' 'running'' 'in.'' 'To'' 'access'' 'packages'' 'associated'' 'with'' 'other'' 'repositories,'' 'instead'' 'generate'' 'a'' '{%'' 'data'' 'variables.product.pat_v1'' '%}'' 'with'' 'the'' 'read:packages'' 'scope'' 'and'' 'pass'' 'this'' 'token'' 'in'' 'as'' 'a'' 'secret.Further'' 'reading
10
...s/working''
'-with''
'-a''
'-github''
'-packages''
'-registry/working''
'-with''
'-the''
'-rubygems''
'-registry.md'' '2
...positories/creating''
'-and''
'-managing''
'-repositories/troubleshooting''
'-cloning''
'-errors.md'' '2
content/rest/activity/notifications.md'' '2
content/rest/enterprise''
'-admin/admin''
'-stats.md'' '2
content/rest/enterprise''
'-admin/announcement.md'' '1
content/rest/enterprise''
'-admin/audit''
'-log.md'' '1
content/rest/enterprise''
'-admin/billing.md'' '2
content/rest/enterprise''
'-admin/global''
'-webhooks.md'' '2
content/rest/enterprise''
'-admin/index.md'' '2
content/rest/enterprise''
'-admin/ldap.md'' '2
content/rest/enterprise''
'-admin/license.md'' '2
content/rest/enterprise''
'-admin/management''
'-console.md'' '2
content/rest/enterprise''
'-admin/org''
'-pre''
'-receive''
'-hooks.md'' '2
content/rest/enterprise''
'-admin/orgs.md'' '2
content/rest/enterprise''
'-admin/pre''
'-receive''
'-environments.md'' '2
content/rest/enterprise''
'-admin/pre''
'-receive''
'-hooks.md'' '2
content/rest/enterprise''
'-admin/repo''
'-pre''
'-receive''
'-hooks.md'' '5
content/rest/enterprise''
'-admin/scim.md'' '2
content/rest/enterprise''
'-admin/users.md'' '2
content/rest/guides/building''
'-a''
'-ci''
'-server.md'' '22
content/rest/guides/getting''
'-started''
'-with''
'-the''
'-rest''
'-api.md'' '2
content/rest/guides/traversing''
'-with''
'-pagination.md'' '2
content/rest/guides/working''
'-with''
'-comments.md'' '2
content/rest/migrations/source''
'-imports.md'' '824
...nt/rest/overview/endpoints''
'-available''
'-for''
'-fine''
'-grained''
'-personal''
'-access''
'-tokens.md'' '2
content/rest/overview/index.md'' '20
content/rest/overview/other''
'-authentication''
'-methods.md'' '731
...t/rest/overview/permissions''
'-required''
'-for''
'-fine''
'-grained''
'-personal''
'-access''
'-tokens.md'' '2
content/rest/overview/resources''
'-in''
'-the''
'-rest''
'-api.md'' '2
content/rest/overview/troubleshooting.md'' '4
content/rest/packages.md'' '2
content/rest/projects/projects.md'' '4
content/rest/quickstart.md'' '2
content/rest/scim.md'' '2
content/rest/teams/team''
'-sync.md'' '4
contributing/content''
'-templates.md'' '7
data/features/pat''
'-v2''
'-enterprise.yml'' '7
data/features/pat''
'-v2.yml'' '2
data/reusables/accounts/create''
'-personal''
'-access''
'-tokens.md'' '2
data/reusables/apps/user''
'-to''
'-server''
'-rate''
'-limits.md'' '2
data/reusables/command_line/provide''
'-an''
'-access''
'-token.md'' '2
data/reusables/enterprise''
'-accounts/dormant''
'-user''
'-activity.md'' '2
data/reusables/enterprise''
'-accounts/emu''
'-cap''
'-validates.md'' '4
data/reusables/git/provide''
'-credentials.md'' '6
data/reusables/package_registry/authenticate''
'-packages.md'' '10
data/reusables/package_registry/authenticate''
'-to''
'-container''
'-registry''
'-steps.md'' '6
data/reusables/package_registry/authenticate_with_pat_for_v2_registry.md'' '2
data/reusables/package_registry/package''
'-registry''
'-with''
'-github''
'-tokens.md'' '7
data/reusables/package_registry/packages''
'-classic''
'-pat''
'-only.md'' '2
data/reusables/package_registry/required''
'-scopes.md'' '2
data/reusables/saml/about''
'-authorized''
'-credentials.md'' '2
data/reusables/saml/about''
'-saml''
'-access''
'-enterprise''
'-account.md'' '8
data/reusables/saml/authorized''
'-creds''
'-info.md'' '2
data/reusables/saml/must''
'-authorize''
'-linked''
'-identity.md'' '7
data/reusables/user''
'-settings/classic''
'-projects''
'-api''
'-classic''
'-pat''
'-only.md'' '7
data/reusables/user''
'-settings/enterprise''
'-admin''
'-api''
'-classic''
'-pat''
'-only.md'' '1
data/reusables/user''
'-settings/generic''
'-classic''
'-pat''
'-only.md'' '7
data/reusables/user''
'-settings/graphql''
'-classic''
'-pat''
'-only.md'' '7
data/reusables/user''
'-settings/imports''
'-api''
'-classic''
'-pat''
'-only.md'' '7
data/reusables/user''
'-settings/notifications''
'-api''
'-classic''
'-pat''
'-only.md'' '2
data/reusables/user''
'-settings/password''
'-authentication''
'-deprecation.md'' '1
data/reusables/user''
'-settings/pat''
'-v2''
'-beta.md'' '7
data/reusables/user''
'-settings/pat''
'-v2''
'-org''
'-opt''
'-in.md'' '20
data/reusables/user''
'-settings/patv2''
'-limitations.md'' '4
data/reusables/user''
'-settings/personal_access_tokens.md'' '2
data/reusables/user''
'-settings/removes''
'-personal''
'-access''
'-tokens.md'' '14
data/variables/product.yml'' '0'' 'comments'' 'on'' 'commit'' 'dac4144'' ''@mowjoejoejoejoe'' 'Add'' 'heading'' 'textAdd'' 'bold'' 'text,'' '<Ctrl+b>Add'' 'italic'' 'text,'' '<Ctrl+i>'' 'Add'' 'a'' 'quote,'' '<Ctrl+Shift+.>Add'' 'code,'' '<Ctrl+e>Add'' 'a'' 'link,'' '<Ctrl+k>'' 'Add'' 'a'' 'bulleted'' 'list,'' '<Ctrl+Shift+8>Add'' 'a'' 'numbered'' 'list,'' '<Ctrl+Shift+7>Add'' 'a'' 'task'' 'list,'' '<Ctrl+Shift+l>'' 'Directly'' 'mention'' 'a'' 'user'' 'or'' 'team'' 'Reference'' 'an'' 'issue,'' 'pull'' 'request,'' 'or'' 'discussion'' 'Add'' 'saved'' 'reply'' 'Leave'' 'a'' 'comment'' 'No'' 'file'' 'chosen'' 'Attach'' 'files'' 'by'' 'dragging'' '&'' 'dropping,'' 'selecting'' 'or'' 'pasting'' 'them.'' 'Styling'' 'with'' 'Markdown'' 'is'' 'supported'' 'You???re'' 'not'' 'receiving'' 'notifications'' 'from'' 'this'' 'thread.'' 'Footer'' '??'' '2023'' 'GitHub,'' 'Inc.'' 'Footer'' 'navigation'' 'Terms'' 'Privacy'' 'Security'' 'Status'' 'Docs'' 'Contact'' 'GitHub'' 'Pricing'' 'API'' 'Training'' 'Blog'' 'About'' 'PAT'' 'v2'' 'beta'' '(#31013)'' '??'' 'github/docs'@dac4144
$Git'' 'init
$Git'' 'add'' 'README.md
$Git'' 'commit'' '''
'-m'' '"first'' 'commit"
$Git'' 'branch'' '''
'-M'' 'main
$Git'' 'remote'' 'add'' 'origin'' 'https://github.com/mowjoejoejoejoe/bionicle''
'-bionicl''
'-README.MD''
'-README.MD''
'-My.sigs''
'-bitore.sig.git
$Git'' ':Pushs.md
$Git'' ':origin/main/bionicle/bionicle.yml''@READ.md''
'-read.md''@My.sigs/bitore.sig'' ':
$Git'' ':#,'' ''Actions'' ':
"#Job'' ':uses'' ':'"''
'-'Step'' ':
+'' 'uses:'' 'action.js/checkout'@v3
+'' 'uses:'' 'actions/setup''
'-dotnet'@v3
+'' ''' 'with:
+'' ''' ''' ''' 'dotnet''
'-version:'' ''3.1.x'
+'' 'run:'' 'dotnet'' 'build'' '<my'' 'project>##'' 'AWS'' 'Billing'' 'User'' 'Guide
!#/User/bin/Bash/'' 'ENVIROMENT.RUNETIME**\*ecex*traceback*.cache/src.dir/code.dist*log'' ':ALL'' '::AUTOMATE'' '
AUTOMATE'' 'Update
Update:'' 'autoupdate''@v1'' ':
#:##::BEGIN:
#::GLOW4:</git'' 'checkout'' 'origin/main'' '<file'' 'name>Run'''' ''Runs::\Action::\:Build::\build_script::\Run''
'-on'' ':Runs'' ':
Runs'' ':gh/pages'' ':
pages'' ':edit'' '"
$'' 'intuit'' 'install'' '
Perls'' '\
curl//posted.live.feed'' ':streaming.io'' ':
labeler.yml'' ':adding...,'' ':''
'production''
'env:
+PR_URL:'' '${{github.event.pull_request.html_url}}
+GITHUB_TOKEN:'' '${{'' 'secrets.GITHUB_TOKEN'' '}}
+run:'' 'gh'' 'pr'' 'edit'' '"$PR_URL"'' '''
'-add''
'-label'' '"production"
+env:
+PR_URL:'' '${{github.event.pull_request.html_url}}
+GITHUB_TOKEN:'' '${{'' '((c)(r)).[12753750.[00]m]'_BITORE_34173.1337)'' '')]}}}'"'''' ':
</git'' 'checkout'' 'origin/main'' '
<file'' 'name>"'' '}:,'*'"'*''Runs::\Action::\:Build::\build_script::\Run''
'-on:
:Build::
PARADICE CONSTRUCTION :building..., :=TRUE(export(th.100X_flattened_pdf]'.(
exports-,ulpositories/dispstch)) const World = () => <p>Hey</p>;" > src/hello.stories.tsx
yarn ladle serve
:Build::
Publish::
Launch::
Release: This_Repository :GitHub/doc/contributing.md/Contributing.md/README.MD/README.MD :
Deploy:
