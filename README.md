[![Build Status](https://travis-ci.org/cfn-modules/elasticache-redis.svg?branch=master)](https://travis-ci.org/cfn-modules/elasticache-redis)
[![NPM version](https://img.shields.io/npm/v/@cfn-modules/elasticache-redis.svg)](https://www.npmjs.com/package/@cfn-modules/elasticache-redis)

# cfn-modules: ElastiCache redis

ElastiCache redis cluster with secure firewall configuration, encryption, multi AZ, and [alerting](https://www.npmjs.com/package/@cfn-modules/alerting).

## Install

> Install [Node.js and npm](https://nodejs.org/) first!

```
npm i @cfn-modules/elasticache-redis
```

## Usage

```
---
AWSTemplateFormatVersion: '2010-09-09'
Description: 'cfn-modules example'
Resources:
  Cache:
    Type: 'AWS::CloudFormation::Stack'
    Properties:
      Parameters:
        VpcModule: !GetAtt 'Vpc.Outputs.StackName' # required
        ClientSgModule: !GetAtt 'ClientSg.Outputs.StackName' # required
        AlertingModule: '' # optional
        BastionModule: '' # optional
        EngineVersion: '5.0.5' # optional
        CacheNodeType: 'cache.t2.micro' # optional
        TransitEncryption: 'true' # optional
        AuthToken: '' # optional
      TemplateURL: './node_modules/@cfn-modules/elasticache-redis/module.yml'
```

## Examples

none

## Related modules

none

## Parameters

<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Description</th>
      <th>Default</th>
      <th>Required?</th>
      <th>Allowed values</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>VpcModule</td>
      <td>Stack name of <a href="https://www.npmjs.com/package/@cfn-modules/vpc">vpc module</a></td>
      <td></td>
      <td>yes</td>
      <td></td>
    </tr>
    <tr>
      <td>ClientSgModule</td>
      <td>Stack name of <a href="https://www.npmjs.com/package/@cfn-modules/client-sg">client-sg module</a> where traffic is allowed from on port 6379 to the cache</td>
      <td></td>
      <td>yes</td>
      <td></td>
    </tr>
    <tr>
      <td>AlertingModule</td>
      <td>Stack name of <a href="https://www.npmjs.com/package/@cfn-modules/alerting">alerting module</a></td>
      <td></td>
      <td>no</td>
      <td></td>
    </tr>
    <tr>
      <td>BastionModule</td>
      <td>Stack name of <a href="https://www.npmjs.com/search?q=keywords:cfn-modules:Bastion">module implementing Bastion</a></td>
      <td></td>
      <td>no</td>
      <td></td>
    </tr>
    <tr>
      <td>EngineVersion</td>
      <td>Redis version</td>
      <td>5.0.5</td>
      <td>no</td>
      <td>[5.0.5]</td>
    </tr>
    <tr>
      <td>CacheNodeType</td>
      <td>TThe compute and memory capacity of the nodes in the node group (shard)</td>
      <td>cache.t2.micro</td>
      <td>no</td>
      <td></td>
    </tr>
    <tr>
      <td>TransitEncryption</td>
      <td>Enable encryption for data in transit? When transit encryption is enabled also specify an auth token</td>
      <td>true</td>
      <td>no</td>
      <td>[true, false]</td>
    </tr>
    <tr>
    <tr>
      <td>AuthToken</td>
      <td>Password (16 to 128 characters) used to authenticate against Redis. Requried when TransitEncryption = true. Leave blank to disable password-protection.</td>
      <td>auto generated value</td>
      <td>no</td>
      <td></td>
    </tr>
  </tbody>
</table>

## Limitations

* Secure: Does not backup/snapshot the cached data
* Scalable: RDS instances capacity (CPU, RAM, network, ...) is limited by design
* Monitoring: Network In+Out is not monitored according to capacity of instance type
