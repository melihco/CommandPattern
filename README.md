In this example, we have the `ICommand` interface, which defines the contract for different commands. The `LightOnCommand` and `LightOffCommand` are concrete implementations of the command interface.

The `Light` class acts as the receiver, which performs the actual operations when the commands are executed. It has methods to turn the light on and off.

The `RemoteControl` class acts as the invoker. It holds a collection of commands and provides methods to set commands and execute them. When the `ExecuteCommands` method is called, it iterates over the commands and invokes their `Execute` method.

In the `Main` method, we create an instance of the `Light` class. Then, we create instances of the `LightOnCommand` and `LightOffCommand`, passing the `Light` object as a parameter. We create an instance of the `RemoteControl` and set the commands in the remote control. Finally, we call the `ExecuteCommands` method on the remote control, which executes the commands. The output displays the messages indicating whether the light is turned on or off.

The Command Pattern allows us to encapsulate requests as objects, which decouples the sender of the request from the receiver. It provides a way to parameterize clients with different requests, queue or log requests, and support undo operations.

```csharp
using System;
using System.Collections.Generic;

// Step 1: Define the command interface
public interface ICommand
{
    void Execute();
}

// Step 2: Implement concrete commands
public class LightOnCommand : ICommand
{
    private readonly Light _light;

    public LightOnCommand(Light light)
    {
        _light = light;
    }

    public void Execute()
    {
        _light.TurnOn();
    }
}

public class LightOffCommand : ICommand
{
    private readonly Light _light;

    public LightOffCommand(Light light)
    {
        _light = light;
    }

    public void Execute()
    {
        _light.TurnOff();
    }
}

// Step 3: Define the receiver
public class Light
{
    public void TurnOn()
    {
        Console.WriteLine("Light is turned on");
    }

    public void TurnOff()
    {
        Console.WriteLine("Light is turned off");
    }
}

// Step 4: Define the invoker
public class RemoteControl
{
    private readonly List<ICommand> _commands;

    public RemoteControl()
    {
        _commands = new List<ICommand>();
    }

    public void SetCommand(ICommand command)
    {
        _commands.Add(command);
    }

    public void ExecuteCommands()
    {
        foreach (var command in _commands)
        {
            command.Execute();
        }
    }
}

// Step 5: Usage example
class Program
{
    static void Main(string[] args)
    {
        // Create the receiver
        var light = new Light();

        // Create the commands
        var lightOnCommand = new LightOnCommand(light);
        var lightOffCommand = new LightOffCommand(light);

        // Create the invoker (remote control)
        var remoteControl = new RemoteControl();

        // Set the commands in the remote control
        remoteControl.SetCommand(lightOnCommand);
        remoteControl.SetCommand(lightOffCommand);

        // Execute the commands
        remoteControl.ExecuteCommands();
    }
}
```
