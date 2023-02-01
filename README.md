# `kubectl eks-node`

## Install

### Get the latest script
```sh
$ wget -O /usr/local/bin/kubectl-eks_node https://raw.githubusercontent.com/flavono123/kubectl-eks-node/main/kubectl-eks_node && chmod +x /usr/local/bin/kubectl-eks_node
```

### Krew
- From [the custom index](https://github.com/flavono123/flew-index)

```sh
$ k krew index add flew https://github.com/flavono123/flew-index.git
$ k krew install flew/eks-node
```

## Usage

```sh
Print the information on a eks node as JSON

Usage:
  eks-node <nodename>
  eks-node <filter-type> <value>
  eks-node po|pod <podname>

Filter types:
  - avaliability_zone(az)
  - instance_type(ins)
  - nodegroup(ng)

Examples:
  # 1. Print the information on a eks node as JSON
  $ kubectl eks-node ip-172-16-200-10.your.domain
  {
    "ip-172-16-200-10.your.domain": {
      "nodegroup": "awsomenode",
      "instance_type": "t3.small",
      "zone": "ap-northeast-2a",
      "pods": [
        "pod-a",
        "pod-b"
      ]
    }
  }

  # 2. Filter nodes by an availability zone
  $ k eks-node az ap-northeast-2a
  NAME                           STATUS   ROLES    AGE    VERSION
  ip-172-16-200-10.your.domain   Ready    <none>   3d4h   v1.23.9-eks-ba74326
  ip-172-16-200-11.your.domain   Ready    <none>   4h2m   v1.23.9-eks-ba74326

  # By an instance type
  $ k eks-node ins t3.large
  NAME                           STATUS   ROLES    AGE    VERSION
  ip-172-16-200-10.your.domain   Ready    <none>   3d4h   v1.23.9-eks-ba74326
  ip-172-16-201-10.your.domain   Ready    <none>   16d    v1.23.9-eks-ba74326
  ip-172-16-202-10.your.domain   Ready    <none>   80m    v1.23.9-eks-ba74326
  ip-172-16-200-12.your.domain   Ready    <none>   5d7h   v1.23.9-eks-ba74326
  ip-172-16-201-11.your.domain   Ready    <none>   3d4h   v1.23.9-eks-ba74326

  # By a nodegroup
  $ k eks-node ng awsomenode
  NAME                           STATUS   ROLES    AGE    VERSION
  ip-172-16-200-10.your.domain   Ready    <none>   3d4h   v1.23.9-eks-ba74326

  # Or print the node information where the specified pod is running
  $ k eks-node po awsomepod-xxxxxxxxxx-yyyyy
  {
    "ip-172-16-200-10.your.domain": {
      "nodegroup": "awsomenode",
      "instance_type": "t3.small",
      "zone": "ap-northeast-2a",
      "pods": [
        "awsomepod-xxxxxxxxxx-yyyyy",
        "pod-a",
        "pod-b"
      ]
    }
  }
```
