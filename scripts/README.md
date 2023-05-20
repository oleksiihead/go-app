# HowTo use kubelugin

This `kubeplugin` helps to execute `kubectl top` command. Plugin requires two parameters:

- resource
- namespace 

## Before you start

Just check if `kubeplugin` has execution permission

```
ls -l kubeplugin
```
if no - add it

```
sudo +x ./kubeplugin
```

## Usage

You can use this `kubeplugin` in two ways:

1. As bash script:

```
./kubeplugin <resource> <namespace>
```

2. As `kubectl` pligin
```
sudo cp ./kubeplugin /usr/local/bin
kubectl kubeplugin <resource> <namespace>
```

In both cases, change the values to your own
