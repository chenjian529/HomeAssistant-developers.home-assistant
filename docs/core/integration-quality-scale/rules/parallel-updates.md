---
title: "Set Parallel updates"
---

## Reasoning

Some devices or services don't like receiving a lot of requests at the same time.
To avoid that, Home Assistant has a built-in feature to limit the number of requests that are sent to a device or service at the same time.

This will be applied to both entity updates and actions calls.

We consider it a good practice to explicitly set the number of parallel updates.

## Example implementation

In the example below, we set the number of parallel updates to 1.
Which means if there are more entities on the sensor platform, they will be updated one by one.
If there is no need to limit the number of parallel updates, you can set it to 0.

`sensor.py`
```python {1} showLineNumbers
PARALLEL_UPDATES = 1

class MySensor(SensorEntity):
    """Representation of a sensor."""

    def __init__(self, device: Device) -> None:
        """Initialize the sensor."""
        ...
```

:::info
When using a coordinator, you are already centralizing the data updates.
This means that usually only the action calls will be relevant to consider for setting the number of parallel updates.
:::

## Additional resources

For more information about request parallelism, check the [documentation](../../../integration_fetching_data#request-parallelism) for it.

## Exceptions

There are no exceptions to this rule.