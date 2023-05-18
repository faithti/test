### Configuration for Telegraf:

To customize the default values, you can make changes in the following section of the values.yaml file:

In this section, you can modify the *replicaCount* to specify the desired number of Telegraf replicas. Additionally, you can change the `image` version for Telegraf by modifying the `tag` field:

```yaml
telegraf:
  name: telegraf
  replicaCount: 1
  image:
    repo: "telegraf"
    tag: "1.26-alpine"
```
