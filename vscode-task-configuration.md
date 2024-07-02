## VS Code Task Configuration

This is a Visual Studio Code (VS Code) task configuration file (`tasks.json`) that defines a task for starting a development server using Yarn. Below is a breakdown of each part of the configuration:

```json
{
  "version": "2.0.0",
  "tasks": [
    {
      "label": "Start Server",
      "type": "shell",
      "command": "yarn dev",
      "group": "none",
      "presentation": {
        "reveal": "always",
        "panel": "new"
      },
      "runOptions": {
        "runOn": "folderOpen"
      }
    }
  ]
}
```

## Configuration Breakdown

### `version: "2.0.0"`
Specifies the version of the task configuration format being used. Version 2.0.0 is a common choice for modern VS Code task configurations.

### `tasks: []`
An array of task objects. Each task object defines a specific task that can be executed in VS Code.

## Task Object

### `label: "Start Server"`
A human-readable label for the task. This label is used to identify and run the task from the VS Code task runner.

### `type: "shell"`
Specifies that the task will be executed in the shell. This allows you to run shell commands.

### `command: "yarn dev"`
The shell command to be executed when the task runs. In this case, it runs `yarn dev`, which typically starts a development server using Yarn.

### `group: "none"`
Indicates that this task does not belong to any specific group. Task groups can be used to group related tasks together (e.g., build, test).

## Presentation Object

### `presentation: {}`
Configures how the task output is presented in the terminal.

- **`reveal: "always"`**
    - Ensures that the terminal always reveals itself when the task is run, making the output visible.

- **`panel: "new"`**
    - Opens a new terminal panel for this task each time it runs, rather than reusing an existing terminal panel.

## Run Options Object

### `runOptions: {}`
Specifies additional options for running the task.

- **`runOn: "folderOpen"`**
    - Configures the task to run automatically when the folder containing the task configuration is opened in VS Code.

## Summary

This task configuration file defines a task labeled "Start Server" that runs the `yarn dev` command in a new terminal panel every time the task is executed. The terminal is always revealed, and the task is automatically run when the folder is opened in VS Code.

Reference: [VS Code Tasks Documentation](https://code.visualstudio.com/docs/editor/tasks)