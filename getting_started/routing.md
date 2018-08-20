# Routing

Routing is a core feature that allows to **route** your data through Filters and finally to one or multiple destinations.

There are two important concepts in Routing:

* Tag
* Match

When the data is generated by the input plugins, it comes with a **Tag** \(most of the time the Tag is configured manually\), the Tag is a human-readable indicator that helps to identify the data source.

Now to define **where** the data should be routed, a **Match** rule is assigned in the configuration.

Consider the following configuration example that aims to deliver CPU metrics to an Elasticsearch database and Memory metrics to the standard output interface:

```text
[INPUT]
    Name cpu
    Tag  my_cpu

[INPUT]
    Name mem
    Tag  my_mem

[OUTPUT]
    Name   es
    Match  my_cpu

[OUTPUT]
    Name   stdout
    Match  my_mem
```

> Note: the above example aim to demonstrate in a simplified way how Routing is configured.

Routing works automatically reading the Input Tags and the Output Match rules. If some data have a Tag that don't have a match upon routing time, the data it's deleted.

## Routing with Wildcard

Routing is flexible enough to support _wildcard_ in the **Match** pattern. The below example defines a common destination for both sources of data:

```text
[INPUT]
    Name cpu
    Tag  my_cpu

[INPUT]
    Name mem
    Tag  my_mem

[OUTPUT]
    Name   stdout
    Match  my_*
```

The match rule is set to **my\_\*** which means it will match any Tag that starts with **my\_**.
