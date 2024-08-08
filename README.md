# 07.08.2024-Java

MyUserController.java
```java
package com.datorium.Datorium.API.Controllers;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
@RequestMapping("/user")
public class MyUserController {
    //CRUD
    //AddUser
    //UpdateUser
    //GetUser
    //DeleteUser

    @GetMapping("/test") //localhost:8080/test -> localhost:8080/user/test
    public String test(){
        return "testy testy";
    }
}
```

Book.java
```java
package com.datorium.Datorium.API.DTOs;

public class Book {
    public String author;
    public String title;
}
```

Credentials.java
```java
package com.datorium.Datorium.API.DTOs;

public class Credentials {
    public String username;
    public String password;
}
```

Food.java
```java
package com.datorium.Datorium.API.DTOs;

public class Food {
    public String dish;
}
```

Ingredients.java
```java
package com.datorium.Datorium.API.DTOs;

public class Ingredients {
    public String pasta;
    public String sauce;
}

```

User.java
```java
package com.datorium.Datorium.API.DTOs;

public class User {
    public String name;
}
```

Datorium.Api.Application.java
```java
package com.datorium.Datorium.API;

import com.datorium.Datorium.API.DTOs.*;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.web.bind.annotation.*;

@SpringBootApplication
@RestController
@CrossOrigin
public class DatoriumApiApplication {

	public static void main(String[] args) {
		System.out.println("asd");
		SpringApplication.run(DatoriumApiApplication.class, args);
	}

	@GetMapping("/ping")
	public String ping() {
		return "pong";
	}

	@GetMapping("/hello")
	public String hello(@RequestParam(value = "name", defaultValue = "World") String name) {
		return String.format("Hello %s!", name); // "Hello " + name;
	}

	@GetMapping("/getbook")
	public Book getBook(){
		var book = new Book();
		book.title = "book title";
		book.author = "author";

		return book;
	}

	@PostMapping("/postexample")
	public Book addBook(@RequestBody Book book){
		book.title = book.title.toUpperCase();
		return book;
	}

	@PostMapping("/authorize")
	public User authorize(@RequestBody Credentials credentials){ // username + password
		if(credentials.username.equals("okklv") && credentials.password.equals("Password123")){
			var user = new User();
			user.name = "Oskars";
			return user;
		}

		return null;
	}

	@PostMapping("/recipe")
	public Food recipe(@RequestBody Ingredients ingredients){
		if(ingredients.pasta.equals("spaghetti") && ingredients.sauce.equals("pesto")){
			var food = new Food();
			food.dish = "Pesto pasta";
			return food;
		}else if (ingredients.pasta.equals("macaroni") && ingredients.sauce.equals("creamy cheese")) {
			var food = new Food();
			food.dish = "Mac and cheese";
			return food;
		}

		return null;
	}

}
```


![image](https://github.com/user-attachments/assets/dacccde0-828e-4e9a-b7ea-444846bdb91a)


The fact that your code works when you change the class name from UserController to TestController suggests that there might be some issue related to the naming of the class or a conflict with the UserController class in your application.

Here are some possible reasons:

1. Naming Conflict or Duplicate Class:
There could be another UserController class somewhere in your project, or in the libraries you are using, which could cause a conflict. If there are two classes with the same name, Spring might get confused about which one to instantiate, leading to unexpected behavior.
You can search your entire project for UserController to ensure there is no other class with the same name.
2. Caching or Build Issue:
Sometimes, IntelliJ or your build system might cache certain configurations or classes. When you change the class name, it might force a fresh build or bypass the cached state, which can resolve the issue.
Rebuilding your project and clearing any caches (File > Invalidate Caches / Restart in IntelliJ) might help.
3. Specific Issue with the UserController Name:
While uncommon, there could be a specific issue with the name UserController if it’s being used by another part of your codebase or a library you are using.
Renaming the controller to something unique like MyUserController could help avoid any conflicts.
4. Component Scanning Issue:
If you have custom component scanning configured (e.g., using @ComponentScan), make sure that it is correctly configured to include the UserController class.
Ensure that there are no exclusions or filters in place that might skip the UserController.
5. Spring Security or Another Filter:
If you are using Spring Security or another filter that might be configured to restrict access to certain URLs or classes, it could potentially be blocking access to the UserController endpoints.
Check your security configurations to ensure there are no rules specifically blocking paths associated with UserController.
What to Do Next:
Search for Duplicate Classes: Make sure there are no other classes named UserController in your project.
Clear Caches and Rebuild: Try clearing IntelliJ’s caches (File > Invalidate Caches / Restart) and rebuilding your project.
Check for Other Configurations: Look for any configurations, such as @ComponentScan or Spring Security, that might interfere with the class being recognized or accessible.
By addressing these potential issues, you should be able to use the UserController name without encountering a 404 error.
