| decimal Value | Binary |  4  |  2  |  1  | Description             | Usefulness                                     |
| :-----------: | :----: | :-: | :-: | :-: | :---------------------- | ---------------------------------------------- |
|       0       |  000   |  -  |  -  |  -  | no permissions          | Very Useful !  <br>for denying access          |
|       1       |  001   |  -  |  -  |  x  | only execute            | Okay, But never seen it used really.           |
|       2       |  010   |  -  |  w  |  -  | only write              | What? doesn't make sense - never seen it used! |
|       3       |  011   |  -  |  w  |  x  | write and execute       | What?  doesn't make sense. Never seen it used! |
|       4       |  100   |  r  |  -  |  -  | only read               | Very Useful !                                  |
|       5       |  101   |  r  |  -  |  x  | read and execute        | Very Useful !                                  |
|       6       |  110   |  r  |  w  |  -  | read and write          | Very Useful !                                  |
|       7       |  111   |  r  |  w  |  x  | read, write and execute | Very Useful !                                  |
