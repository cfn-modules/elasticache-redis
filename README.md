# cfn-modules: ElastiCache redis

ElastiCache redis cluster with secure firewall configuration, [encryption](https://www.npmjs.com/package/@cfn-modules/kms-key), multi AZ, backup enabled, and [alerting](https://www.npmjs.com/package/@cfn-modules/alerting).

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
        KmsKeyModule: '' # optional
        EngineVersion: '5.0.5' # optional
        CacheNodeType: 'cache.t2.micro' # optional
        TransitEncryption: 'true' # optional
        AuthToken: '' # optional
        SnapshotRetentionLimit: '35' # optional
        SnapshotName: '' # optional
        NumShards: '1' # optional
        NumReplicas: '1' # optional
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
      <td>KmsKeyModule</td>
      <td>Stack name of <a href="https://www.npmjs.com/package/@cfn-modules/kms-key">kms-key module</a></td>
      <td></td>
      <td>no</td>
      <td></td>
    </tr>
    <tr>
      <td>EngineVersion</td>
      <td>Redis version</td>
      <td>5.0.5</td>
      <td>no</td>
      <td>[5.0.5,5.0.6,6.0,6.2]</td>
    </tr>
    <tr>
      <td>CacheNodeType</td>
      <td>The compute and memory capacity of the nodes in the node group (shard)</td>
      <td>cache.t2.micro</td>
      <td>no</td>
      <td></td>
    </tr>
    <tr>
      <td>TransitEncryption</td>
      <td>Enable [encryption for data in transit](https://docs.aws.amazon.com/AmazonElastiCache/latest/red-ug/in-transit-encryption.html)?</td>
      <td>true</td>
      <td>no</td>
      <td>[true, false]</td>
    </tr>
    <tr>
      <td>AuthToken</td>
      <td>Password (16 to 128 characters) used to authenticate against Redis (requires TransitEncryption := true; leave blank to disable password-protection)</td>
      <td></td>
      <td>no</td>
      <td></td>
    </tr>
    <tr>
      <td>SnapshotRetentionLimit</td>
      <td>The number of days for which ElastiCache retains automatic snapshots before deleting them (set to 0 to disable backups)</td>
      <td>35</td>
      <td>no</td>
      <td>[0...35]</td>
    </tr>
    <tr>
      <td>SnapshotName</td>
      <td>Name of a snapshot from which you want to restore (leave blank to create an empty cache)</td>
      <td></td>
      <td>no</td>
      <td></td>
    </tr>
    <tr>
      <td>NumShards</td>
      <td>Number of shards in the cluster.</td>
      <td>1</td>
      <td>no</td>
      <td>[1-250]</td>
    </tr>
    <tr>
      <td>NumReplicas</td>
      <td>Number of replicas per shard.</td>
      <td>1</td>
      <td>no</td>
      <td>[0-5]</td>
    </tr>
  </tbody>
</table>

## Limitations

* Scalable: Cache instances capacity (CPU, RAM, network, ...) is limited by design
* Monitoring: Network In+Out is not monitored according to capacity of instance type
