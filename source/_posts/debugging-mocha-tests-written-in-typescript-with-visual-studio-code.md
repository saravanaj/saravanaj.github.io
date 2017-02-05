title: Debugging Mocha Tests Written in TypeScript with Visual Studio Code
date: 2017-02-05 08:55:38
tags:
- visual studio code
- mocha
- config
---

Visual Studio Code is an excellent IDE for frontend development. One of the great things about it is how easily it integrates with other tools. Let's see how to integrate it with Mocha and debug tests written in TypeScript right inside VS Code:

### Folder Structure

Here is my folder structure. The code I want to test is in `src/main.ts` and my tests are in `test/main.test.ts`. The code is available at https://github.com/saravanaj/vscode-mocha-ts-config

![Folder structure](/images/mocha-folder-structure.png)

### Configuration

Add a configuration to debug Mocha tests in `.vscode/launch.json`:

```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "type": "node",
            "request": "launch",
            "preLaunchTask": "tsc",
            "name": "Run Mocha",
            "program": "${workspaceRoot}/node_modules/mocha/bin/_mocha",
            "args": ["${workspaceRoot}/test/**/*.js"],
            "cwd": "${workspaceRoot}",
            "outFiles": []
        }
    ]
}
```

Note that the `preLaunchTask` property is set to the TypeScript compilation task I have defined in `.vscode/tasks.json`. This will compile all your `*.ts` files before running the tests. You can modify the `args` property to run a specific test file that you are debugging. Currently it executes all test files inside `test` directory.

And that is it. Add some breakpoints in your `*.test.ts` file and select `Run Mocha` from the debug dropdown:

![Debugger](/images/mocha-debugger.png)

