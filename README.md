# tekton-dotnet

This repo is for experimenting with .NET and Tekton.

It contains a Task `dotnet` based on the `s2i-dotnet` Task (https://github.com/openshift/pipelines-catalog/blob/master/task/s2i-dotnet/0.1/s2i-dotnet.yaml).

`s2i-dotnet` is meant as a cluster task, while `dotnet` is meant to be imported in a namespace.

The `dotnet` task has the following parameters:

| Name | Description |
|---|---|
| PROJECT | Location of the .NET project file or its parent folder. |
| CONFIGURATION | Build configuration. |
| NUGETCONFIG | XML for NuGet.Config file. |

The parameters can be specified for the Task, or they can be specified for all tasks in the namespace by adding them to the `dotnet-configmap` ConfigMap.

For example, the following ConfigMap causes all builds to use a specific NuGet server.

```yaml
kind: ConfigMap
apiVersion: v1
data:
  NUGETCONFIG: |-
    <configuration>
      <packageSources>
        <clear />
        <add key="mycompany" value="https://nuget.mycompany.com/v3/index.json" />
      </packageSources>
    </configuration>
```