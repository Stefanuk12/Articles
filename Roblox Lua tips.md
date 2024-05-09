# Roblox Lua tips

## Use events to your advantage

Roblox is an event-driven platform, majority of actions like when a child is added has an event which you can listen to. Do not underestimate the power of events, they can make your code a lot cleaner, easier to understand, and faster. Do not have a loop that checks if a child is added, instead, use the `ChildAdded` event.

If you find yourself doing an infinite while loop to check if something happens within the game, you're likely doing something wrong. You can achieve the same thing with events most of the time which would be more efficient.

Note that you're not limited to Roblox events, you can create your own events using the `BindableEvent` class or a custom implementation like signals. As a learning exercise, try to create your own event system. [Here is mine](https://github.com/Stefanuk12/Signal) if you want to take a look.

## Code in Visual Studio Code

Roblox Studio's code editor is not as customisable as Visual Studio Code. You can install plugins, themes, and customise the layout to your liking. You can also use Git to manage your code, which is a huge advantage over Roblox Studio's built-in version control system. There are plugins like Rojo which allow you to sync your code with Roblox Studio, meaning there's almost no reason to use Roblox Studio's code editor.

You can install a better AI completion plugin like GitHub Copilot, a formatter like StyLua, better type checking.

## Use types

Since Lua doesn't need types, many people aren't accustomed to putting them in. While Luau types aren't the best currently, they still are very useful in finding bugs early. For example, if you write a function that takes in a number but you pass in a string, your editor will tell you that you're passing in the wrong type. This can save you a lot of time debugging. It can also make you more confident in your code, meaning you don't have to worry about erroring as much.

Also, types can give your editor intellisense, meaning you can see what functions are available on a variable. This can save you a lot of time looking up the documentation or back at your own code to see what it does.

## Split your code up into many files

When you start to make bigger projects, you will find that your code becomes harder to manage. You can split your code up into many files, each with a specific purpose. For example, you can have a file for UI, a file for networking, a file for player management, etc. This makes your code a lot cleaner and easier to understand. You can also reuse code more easily via modules (ModuleScripts), meaning you don't have to copy and paste the same code over and over again. If you need to change a specific aspect, you can easily locate that part of the code and change it, instead of going through a huge file to find it.

Similarly, you can use a bundler like [darklua](https://github.com/seaofvoices/darklua) to combine your files into one, making it easier to distribute your code.

## Format and name your code properly

When I started to script, I greatly underestimated the power of proper formatting. I would always mess up my `end` statements because I didn't format my code properly. Many people, like myself, get confused on how many ends to put, where to put them, and whether they need closing bracket `)` or not.

Here is a side-by-side comparison:

```lua
-- Bad
function aaa(ff)
if ff() then
local x = 1
while true do wait(1)
x = x + 1
if x == 10 then
break
end
end
end
end
aaa(function() return true end)
```

```lua
-- Good
local function Wait(CheckFunction)
    if CheckFunction() then
        local counter = 1

        while true do
            wait(1)
            counter = counter + 1

            if counter == 10 then
                break
            end
        end
    end
end
Wait(
    function()
        return true
    end
)
```

Which one is easier to read? The second one, right? That's because it's properly formatted with proper naming. You can use a formatter like StyLua to format your code automatically. It will save you a lot of time and headaches. You can clearly see how each `end` corrosponds the start of a block (`if`, `while`, `function`, etc).

## Guard clauses and other techniques

Guard clauses are a great way to reduce nesting in your code. Instead of having a lot of `if` statements, you can return early if a condition is met. This makes your code a lot cleaner and easier to understand. There are other techniques that can make your code cleaner, please research these in your own time by watching videos online or other resources.

Here is an example:

```lua
-- Bad
if x then
    if y then
        if z then
            -- Do something
        else
            error("z is false")
        end
    else
        error("y is false")
    end
else
    error("x is false")
end
```

```lua
-- Good
if not x then
    error("x is false")
end

if not y then
    error("y is false")
end

if not z then
    error("z is false")
end
```