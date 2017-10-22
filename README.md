# msbuild-tools

Work with Visual Studio (MSBuild) projects from inside Visual Studio Code.

Feedback is highy appreciated! Let me know if this works for you? Are there any showstopping bugs? Any features missing?

(I should probably merge this is vscode-xbuild-tools when I have time)

## Caveats

* First release, my first non-trivial TypeScript/JavaScript program - expect bugs, problems, and non-idiomatic code.
* Managing the project (adding files, changing settings, etc.) has to be done using Visual Studio itself.

## Features

* Build/Clean/Debug/Run Visual Studio solutions from within vscode.
* Switch between configurations (Debug/Release)
* Debug directly from vscode - easily define debug configuration.
* Status bar items that make it easy to build, debug, switch build and debug configurations.

## Example

In a new directory:

1. Create a new Visual Studio command line project, with the original name `project` and a solution `project.sln'.

2. Create a configuration as a file named `.vscode/msbuild-tools.json`:

```json
{
    "solution": "${workspaceRoot}/project/project.sln",
    "variables": {
        "MSBUILD": "C:/Program Files (x86)/Microsoft Visual Studio/2017/Community/MSBuild/15.0/Bin/MSBuild.exe",
        "DEVENV": "C:/Program Files (x86)/Microsoft Visual Studio/2017/Community/Common7/IDE/devenv.com"
    },
    "postBuildTasks": [
        {
            "name": "Sleep for a few seconds",
            "program": "cmd",
            "args": [ "/c", "sleep 10" ],
            "cwd": "${workspaceRoot}"
        }
    ],
    "debugConfigurations": [
        {
            "name": "test",
            "cwd": "${workspaceRoot}",
            "program": "${buildPath}/project/${buildConfig}/hello.exe",
            "args": [
                "${ARG1}",
                "${ARG2}"
            ]
        }
    ] 
}
```

3. Use `msbuild-tools` command to build, debug, run, clean, switch build configuration, and switch debug configurations.

4. Use the status bar to build, debug, switch configurations or kill the build.

## Credits

* Heavily influenced by the great [CMake-Tools](https://github.com/vector-of-bool/vscode-cmake-tools) extension. 
* Code derived from the basic extension generated by [`yo code`](https://github.com/Microsoft/vscode-generator-code).
