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



