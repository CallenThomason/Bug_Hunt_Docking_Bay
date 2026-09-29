# Docking Bay Bug Log

**Name:** ______________________________

Log **every** bug as you fix it, one row per bug. There are **15**: 5 syntax, 4 runtime, 6 logic.

- **File**: which file the bug was in, e.g. `Services/ShipService.cs`
- **Line**: the line number where you made the fix
- **Kind**: `Syntax`, `Runtime` or `Logic`
- **What was wrong**: what the code did, and how you noticed (the build error, the exception, or the wrong result in Postman)
- **How I fixed it**: exactly what you changed

## Example (not one of the 15)

| # | File | Line | Kind | What was wrong | How I fixed it |
|---|------|------|------|----------------|----------------|
| 0 | `Services/ExampleService.cs` | 22 | Logic | `GET /api/example/cheapest` returned the **most** expensive item. The list was sorted with `OrderByDescending(i => i.Price)`, so the first item was the priciest. | Changed `OrderByDescending` to `OrderBy`. |

## My bugs

| # | File | Line | Kind | What was wrong | How I fixed it |
|---|------|------|------|----------------|----------------|
| 1 |`Services/IpilotService.cs` | 9 |Syntax | List was not capitalized| I capitalized List<> |
| 2 | `Services/PilotService.cs`| 49 | Runtime | Missing a return false, if pilot is null | Add an if(pilot is null) statement |
| 3 |`Services/ShipService.cs` | 10 | Syntax | Missing a comma after Iron comet | Added a comma |
| 4 | `Models/Ship.cs` | 6 | Syntax | Missing a statement terminator | Added the missing statement terminator|
| 5 | `Program.cs` | 8 | Logic | IShipService is linked to ShipService twice, and PilotService is not | changed AddScoped<IShipService, ShipService>() to IpilotService, PilotService |
| 6 |`Controllers/PilotsController.cs` |13 | Syntax | PilotsController is missing the s | changed PilotController to PilotsController|
| 7 |`Services/ShipService.cs` | 21 | logic | called .First | Changed it to .FirstOrDefault|
| 8 |`Controllers/ShipsController` | 37| logic | ship != null causes program to output the wrong thing | changed it to ship == null |
| 9 |`Controllers/ShipsController.cs` | 32 | Syntax | Missing a closing bracket | added a closing bracket|
| 10 | `Services/ShipService.cs`| 54 | Logic | We where adding 100 to the already existing fuel value| changed += to =|
| 11 |`Controllers/ShipsController.cs` | 62 |Runtime  |the foreach loop would not execute properly because a piece was getting removed | changed the foreach loop to a for loop |
| 12 |`Controllers/PilotsController.cs` | 18 | Runtime | The url does not work because "GetAll" has a different name | fixed the name  |
| 13 | `Services/PilotService.cs`|53 | Logic| was setting flightHours equal to hours | changed = to += |
| 14 |`Controllers/PilotsController.cs` |62 | Logic | The if statement did not include 0| changed < to <= |
| 15 |`Controllers/PilotsController.cs` | 52| Runtime| The name does not match the url call | fixed the name |



## Tally

| Kind | Found |
|------|-------|
| Syntax | _5__ / 5 |
| Runtime | __4_ / 4 |
| Logic | _6__ / 6 |

## Reflection

Answer each in 2–3 sentences.

1. Which bug took you the longest to find? What finally led you to it?
2. Pick one **runtime** error. What exception did it throw, and how did the error message help
   you find the line?
3. `DELETE /api/ships/3` crashed with `Collection was modified`. Why can't a `foreach` loop keep
   going after you remove something from the list it's looping over?
4. Every `/api/pilots` request crashed until you fixed one line in `Program.cs`. Explain what
   dependency injection was trying to do and why it failed.
5. Several logic bugs were a single character, like `!=` versus `==`, `<` versus `<=`, or
   `=` versus `+=`. Why doesn't the compiler catch these?
6. Some bugs hid until you fixed a different one. Give one example.

+ The bug that took me the longest to find was the foreach loop that needed to be a for loop. Bug number 11 for me. I knew that something was wrong with the delete, because it was returning 500, but I did not know what exactly was wrong. The ships where being deleted, but it was throwing an error. 
+ For bug 11 it threw the runtime error 500, internal server error. The error message honestly did not help me find the error, but because it was only showing up when I ran my delete I know the error must have been because of my Delete method. 
+ A `foreach` loop cannot keep going after you remove something from the list its looping over because the list shifts and it gets confused. The bounds of the list change and it causes it to crash. 
+ Dependency injection was trying to allow the Controller to call apon the methods that we created in the services. It failed because we did not properly set the scope of IPilotService and PilotService. Due to this issue, we could not properly create our constructor at the start of the controller. 
+ The compiler does not catch operator bugs because it is only running the logic you give it. Logic errors do not cause the code to break, they only cause incorrect outputs. 
+ A bug that hid until I fixed a different one where the logic errors hiding behind syntax errors. I would finally get the program to run, only to realize the correct information wasn't being output. This happened most notably with my bug 8 and 9. Adding the bracket got the program to run, but it was outputting "No Ship with Id" every single time. I had to then go back in and figure out what was wrong with the logic. (Note: the bugs where found out of order, because I had to go back and delete bugs that turned out not to be bugs). 