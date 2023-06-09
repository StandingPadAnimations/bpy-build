# Bpy-build
A tool to make building addons faster

# How to use
Install from PyPi:
`pip install bpy-addon-build`

First create a file called `bpy-build.yaml` and add the following contents:
```yaml
addon_folder: . # or the folder with the addon source code
build_name: my_addon
```

Then run `bpy-addon-build`, your addon will be built in the `build` folder!

Now let's automatically install our addon:
```yaml
addon_folder: . # or the folder with the addon source code
build_name: my_addon

install_versions:
  - '3.5'
```

We can also do stuff during the build process:
```yaml
during_build:
  # This will always be executed
  default:
    - create_file("mcprep_dev.txt") 
```

When we build, the default case will always run. We can also define cases we want to only run if we specify them:
```yaml
during_build:
  # This will always be executed
  default:
    - create_file("mcprep_dev.txt") 
  dev:
    - copy_file("some_file -> destination in the addon folder")
    - [some_command with-args | and-pipes, another_command]
```

To run the `dev` case, we pass the `-b` argument, like `bpy-addon-build -b dev`. Note that when making an action, the action is ran at the root of your addon folder.

Our addon will now automatically be installed in Blender 3.5! If it doesn't exist, `bpy-build` will just ignore it.

