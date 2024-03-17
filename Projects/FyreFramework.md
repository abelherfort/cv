## FyreFramework

An all-in-one multi-target framework system, that uses a shared API, that ensures that developers can use the same code for Bukkit, Velocity or any server implementation. It covers all tasks of plugin development, such as configuration serialization, plugin messages, command system, database management, placeholder management, persistent data wrapper, dependency injection tool, service registration, dependency injection. and much more.

### Architecture

Plugin development is done accessing the API layer only. This makes sure that the developer can only see the important functionalities, and do not have to worry about how the system work "under the hood".

The implementation for these mechanics are provided by the side-specific implementation layers. Each server should contain the desired implementation plugin for their platform type. Therefore the implementation is provided at runtime, and no framework logic must be included in the plugins' jar files.

![architecture](https://media.yoursit.ee/cv/framework/architecture.png)

### Example plugin

Desiging the making of a framework plugin was difficult. We had to keep in mind, that our team is used to writing plugins the "standard way". Therefore I had to come up with a solution, that would allow the developers to use a similar syntax, whilst using the power the framework provides.

Below is a quick example showcase, that how a framework plugin enable logic could possibly look like.

![example-plugin](https://media.yoursit.ee/cv/framework/example-plugin.png)

### Scoreboards

Scoreboard handling was a huge dilemma. Each minigame plugin used a robust logic for creating scoreboard handlers. Multiple plugins had to each implement thousands of lines, just to create a proper scoreboard with the information the minigame provided.

I came to a conclusion, that it would be easier for both the programmer, and later the configurator, to define scoreboards in a configuration file, such as any other configuration would be done. The framework would implicitly load and parse these configurations, and create scoreboard instances.

![scoreboard-config](https://media.yoursit.ee/cv/framework/scoreboard-config.png)

Scoreboard information providing is done using hooks. These hooks are called every time, as it is defined in the `refresh-rate`. These hooks are called for each player, that the scoreboard is registered to.

This means, that anyone making a scoreboard integration in their plugins, would only need to define few functions, to provide minigame information, and the framework would call these functions, whenever necessary.

![scoreboard-hooks](https://media.yoursit.ee/cv/framework/scoreboard-hooks.png?)

### Command system

The biggest problem of defining commands in Bukkit, is that the syntax is very low-level. This means, that each command must have logic for complex argument validation and sub-command handling.

This all was solved with an annotation pattern. This means that the framework would implicitly check all input given by the user. Error messages are provided by the framework based on the information defined in the command. Therefore the arguments that are passed to the command handler, are already validated and safe to use.

Another huge advantage this system provides, is that developers could write the same exact code for Bukkit and Velocity plugins. This is considered a huge advantage, as command registration and handling is way different on these platforms.

![command-descriptor](https://media.yoursit.ee/cv/framework/command-descriptor.png)

![command-execution](https://media.yoursit.ee/cv/framework/command-execution.png)

The same logic applies to command tab completion.

![command-completion](https://media.yoursit.ee/cv/framework/command-completion.png)
