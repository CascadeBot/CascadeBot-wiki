This project follows a set code style across all of the projects. In general, we adhere to the [Google code style for Java](https://google.github.io/styleguide/javaguide.html) but in some cases we have our own additions or modifications.

1. All files have a copyright statement at the top: 
    ```
    /*
     * Copyright (c) {year} CascadeBot. All rights reserved.
     * Licensed under the MIT license.
     */
     ```
     If you use IntelliJ, you can [setup a copyright template](https://www.jetbrains.com/help/webstorm/generating-and-updating-copyright-notice.html) using the placeholder `$today.year` for the year. This will automatically preface new files with the right copyright notice.
2. In contrast to [4.1.1](https://google.github.io/styleguide/javaguide.html#s4.1.1-braces-always-used), we allow the use of single line `if` statements as long as they are not part of a multi-block statement. If the statement consists of multiple `if` branches or an `else` block then braces are used.
3. We're not savages so, for that reason, we use four spaces instead of two. In reference to [4.2](https://google.github.io/styleguide/javaguide.html#s4.2-block-indentation).
4. As per [2.3.3](https://google.github.io/styleguide/javaguide.html#s2.3.3-non-ascii-characters), we use unicode escapes coupled with a explanatory comment.
5. We add an additional blank line after the class header for clarity i.e. a line after `public class ClassName {`.
6. We also add a blank line before the closing brace of a class.
7. As per [3.1.1](https://google.github.io/styleguide/javaguide.html#s3.3.1-wildcard-imports), wildcard imports **are not** used.
8. While we adhere to [4.1.3](https://google.github.io/styleguide/javaguide.html#s4.1.3-braces-empty-blocks), empty blocks are **not** to be used without good reason. With any empty block, an appropriate comment explaining why the block is empty is required.
9. In contrast to [4.4](https://google.github.io/styleguide/javaguide.html#s4.4-column-limit), we do not have a mandatory line limit. We ask that code-writers use their common sense to determine when a line is too long. Lines over 120-130 characters long should be reviewed to see if they can be line-wrapped. As stated before however, this is not required. 
   1. Use the guidelines at [4.5](https://google.github.io/styleguide/javaguide.html#s4.5-line-wrapping) to determine how to line-wrap.
10. Variables, fields and parameters should **all** be given explanatory names. Having nonsensical names is not allowed!

## Example
### Good
```java
/*
 * Copyright (c) 2019 CascadeBot. All rights reserved.
 * Licensed under the MIT license.
 */

package com.cascadebot.cascadebot.commands.developer;

import com.cascadebot.cascadebot.commandmeta.CommandContext;
import com.cascadebot.cascadebot.commandmeta.ICommandRestricted;
import com.cascadebot.cascadebot.commandmeta.Module;
import net.dv8tion.jda.core.entities.Member;

import java.util.Arrays;

public class TestCommand implements ICommandRestricted {

    @Override
    public void onCommand(Member sender, CommandContext context) {
        // Command content
    }

    @Override
    public String command() {
        return "test";
    }

    @Override
    public String description() {
        return "Command that developers change when testing stuff";
    }

    @Override
    public Module getModule() {
        return Module.DEVELOPER;
    }

}
```
### Bad
```java
package com.cascadebot.cascadebot.commands.developer;

import com.cascadebot.cascadebot.commandmeta.*;
import net.dv8tion.jda.core.entities.Member;

import java.util.Arrays;

public class testcommand implements ICommandRestricted {
  public void onCommand(Member s,CommandContext c) 
  {
    //Command content
  }

  public String command( ) 
  {
    return "test";
  }

  public String description( ) 
  {
    return "Command that developers change when testing stuff";
  }
  public Module getModule( ) 
  {
    return Module.DEVELOPER;
  }
}
```