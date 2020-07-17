---
category: Using Form Builder
expires: 2021-01-10
---

# Node Dependencies

The two main Node based applications are the fb-runner-node and the fb-editor-console-electron.

However there are also several component dependencies that are used in both:

- fb-components
- fb-client
- fb-editor-node
- fb-transformers
- module-alias

![circular dependencies](/images/circular_dependencies.png)

Basically if, for example, module-alias is updated be aware that it is used in both a parent and a child dependency.

The editor-node is particularly unusual in that it has a dependency on the fb-runner-node.
