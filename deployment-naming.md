# Naming

Currently multiple things are named jobs which is confusing in code or in operation. Below diagram shows new proposed naming hierarchy:

```
Director (prod)
 |
 +-- Deployment (cf1)
      |
      +-- Cluster (cell-linux) *new*
           |
           +-- Node (2f66d0c7-b182-4f3e-96dd-a09ebaef2ae4) *new*
                |
                +-- Job (cell)
                     |
                     +-- Process (cell)
```

Director: Main orchestration components which is accessed by multiple users.

Deployment: Logically wraps together allocated cloud resources, saved configurations, used release versions, ACLs, etc. Typically user operates on a deployment which ties multiple releases and stemcells.

Cluster: Collection of X number of Nodes tasked to do same thing.

Node: Part of a Cluster doing a specific thing. Each node in a cluster is configured in a similar way in regards to machine size, disk size, OS, configuration values, etc.

Job: Represents a specific thing to do on a Node. Could be placed with other jobs on a node to cooperate. Typically is long running.

Process: Actual implementation of a Job. One or more processes may be needed to perform a Job. Processes are monitored and restarted.
