GetChild-.API-Module-by-orcus0
(Roblox Luau)
# GetChild [API] Module 🧒 | Hate Infinite Yield Possible(s)? 😔 | With Multi-searching?

![image](https://github.com/user-attachments/assets/c6c8f173-79c4-4ba1-b6da-15210a544326)

[Downloaded scripts in main can be inserted in to your game by: Right clicking Workspace and click “Insert from File”, then locate the .rbxm file and double click it]

KIDNAPPING ❌ | KIDCATCHING ✅

In need of finding a child? No worries! We've got you covered.

[Highest Recorded Memory Usage (p.u.): 0.060 MB]

## Synopsis

GetChild is a method that attempts to find a child within a parent object based on specified criteria. 
- It allows for both recursive and non-recursive searches and can be forced to wait for a specified amount of time before failing.

## Parameter(s)

- childName (string or {string}): The name or names of the child(ren) to search for.
- failTick (number, optional): The number of ticks to wait before the search fails. If not provided, the function will not wait.
- recursive (boolean): If true, the function will search recursively through all descendants. If false, only immediate children will be searched.
- forceCall (boolean): If true, forces the function to wait until failTick before returning a result. If false, the function returns immediately if no child is found.
- callback (function, optional): A callback function that is executed with the result if a child is found. The callback should accept a single argument, the found Instance.

## Returns

- Instance: The first child instance that matches the criteria, or nil if none is found.
- Table: A table containing two RBXScriptSignals:
   - Result: Fired when the search is completed.
     
   - Update: Fired during the search process.

## Annotations
```
GetChild(childName: string | {string}, fallTick: number?, recursive: boolean, forcecall: boolean)
    -- callback: (result: Instance) -> any?): (Instance, {|Result: RBXScriptSignal, Update: RBXScriptSignal|})
```
## Syntax(es)
```
local result, connection = newParent:GetChild(childName, failTick, recursive, forceCall, callback)
```
## Special Search: Example
```
local result, connection = newParent:GetChild('Part:typeof:Instance', 10, false, true);
```
## Multi-search/Special Search: Example
```
local result, connection = newParent:GetChild({'Part:class:LocalScript', 'Part:typeof:Instance', 'Baseplate'}, 10, false, true);
```
## How to: Add new special Parameters

1. Go into the GetChild Module and find: array.Parameters
2. By using this table, you're able to add functions like this.
```
function array.Parameters:typeof(comparison: Instance, data: {[number]: string})
    assert(#data[3] >= 1, `Special Parameter Missing, cause: [3] from: = {table.concat(data, ':')}`)

    return (typeof(comparison) == data[3])
end; -- Already existing function
```

## Functionality

In below image you will see ChildrenFound (which is apart of the hidden table), you should be able to call this, next you will see HasFound being used by WaitForChild, there should be no delay between these actions, you can also see that it is using an while loop for pausing the current main task.

![image](https://github.com/user-attachments/assets/6be9f80c-585c-461b-9361-53aa0616a996)


## Examples
- callback: (result: Instance) -> any?)
  ```
  local result, connection = newParent:GetChild('Part', 10, false, true, function(foundInstance)
    print("Child found: ", foundInstance) 
  end)
  ```

- Practical Set-up:
  ```
  local GetChild = require(script.GetChild) -- 1. Require Module

  local newParent = GetChild.new(workspace) -- 2. Find an DataModel/Instance to serach from.
  newParent.RecursiveTimeout = 1;
  newParent.Debugger = true; -- OPTIONAL, THOUGH RECOMMEND SINCE IT PRINTS FOR YOU.

  local result, connection = newParent:GetChild('Part', 10, false, true); -- 3. Set up some appropriate parameters.

  if not result and connection then
        connection.Result:Connect(function(...) -- (response, result)
        print(...)                              -- Consists of { [~s] = `Took GetChild({self.Total}), result success.`, [~s] = FirstChild } 
        end);                              
        connection.Update:Connect(function(...) -- Basically useless junk data.  --print(...) -- ONLY NEEDED FOR CERTAIN EVENTS, NOT DEBUGGING.
        end); 
  else
        print(result) -- Prints if forceCall was bypassed.
  end;
  ```
### Note that in the ExampleScript, print(result) is changed to warn(result) 
