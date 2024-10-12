In a Dockerfile, both `ENTRYPOINT` and `CMD` are used to specify what command should run when a container starts, but they serve different purposes and have distinct behaviors.

### `CMD`
- **Purpose**: Provides default arguments for the `ENTRYPOINT` instruction or specifies the command to run when no `ENTRYPOINT` is defined.
- **Syntax**: Can be used in two forms:
  1. **Exec form** (preferred):
     ```dockerfile
     CMD ["executable", "param1", "param2"]
     ```
  2. **Shell form**:
     ```dockerfile
     CMD command param1 param2
     ```
- **Overridable**: If you provide a command when running the container (e.g., `docker run my_image my_command`), it will override the `CMD`.

### `ENTRYPOINT`
- **Purpose**: Specifies a command that will always run when the container starts, allowing you to set the primary command for the container.
- **Syntax**: Similar to `CMD`, it can also be defined in two forms:
  1. **Exec form** (preferred):
     ```dockerfile
     ENTRYPOINT ["executable", "param1", "param2"]
     ```
  2. **Shell form**:
     ```dockerfile
     ENTRYPOINT command param1 param2
     ```
- **Not easily overridable**: If you run a container with a different command, it will be appended as arguments to the `ENTRYPOINT` command rather than replacing it.

### Example

Here's a simple example to illustrate the difference:

```dockerfile
# Using CMD
CMD ["nginx", "-g", "daemon off;"]

# Using ENTRYPOINT
ENTRYPOINT ["nginx", "-g", "daemon off;"]
```

- If you specify `CMD`, you can override it when running the container:
  ```bash
  docker run my_image my_custom_command
  ```

- If you specify `ENTRYPOINT`, you can append additional arguments to the command:
  ```bash
  docker run my_image --help
  ```

### Summary
- Use `CMD` for default commands or parameters that can be overridden.
- Use `ENTRYPOINT` to define the main command that should always run. 

Often, they are used together to create a flexible and powerful command setup in Docker containers.
