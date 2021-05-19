# Usefull commands Shell

## Grep

Sometimes you need to filter what you are getting in your command line. For this, grep is very usefull. Some usefull options for grep are:

### Context controll

-B (--before-context=NUM): print NUM lines before the filtered word

-A (--after-context=NUM): print NUM lines after the filtered word.

Example:

```sh
kubectl get pods | grep -A3 example
```

Get the next 3 lines after lines with 'example' word.