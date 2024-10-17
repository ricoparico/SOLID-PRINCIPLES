# SOLID Principles
The SOLID principles are a set of five design principles intended to make software designs more understandable, flexible, and maintainable. Originally articulated by Robert C. Martin, these principles can significantly improve the architecture of Angular applications.

**1. Single Responsibility Principle (SRP)**
**Definition:**
A class should have one, and only one, reason to change. This means that a class should only have one job or responsibility.

**Application in Angular:**
In Angular, this can be applied to services and components. For example, a service that handles user authentication should not also manage user notifications.

**Code Snippet:**

// UserService.ts
@Injectable({
  providedIn: 'root',
})
export class UserService {
  login(user: User): Observable<User> {
    // Logic for user login
  }
}

// NotificationService.ts
@Injectable({
  providedIn: 'root',
})
export class NotificationService {
  sendNotification(message: string) {
    // Logic to send notifications
  }
}


**Real-World Use Case:**
If you need to update the notification logic, you can do so without affecting the user authentication logic. This makes your application easier to maintain and test.

**2. Open/Closed Principle (OCP)**
**Definition:**
Software entities should be open for extension but closed for modification. This means that you should be able to add new functionality without changing existing code.

**Application in Angular:**
Using interfaces and abstract classes helps achieve this principle. For instance, you can create a base service and extend it to create more specific services.

**Code Snippet:**

export abstract class Notification {
  abstract send(message: string): void;
}

@Injectable({
  providedIn: 'root',
})
export class EmailNotification extends Notification {
  send(message: string) {
    // Logic to send an email
  }
}

@Injectable({
  providedIn: 'root',
})
export class SMSNotification extends Notification {
  send(message: string) {
    // Logic to send an SMS
  }
}


**Real-World Use Case:**
If a new notification type is needed, like push notifications, you can simply create a new class that extends Notification without modifying existing code.

**3. Liskov Substitution Principle (LSP)**
**Definition:**
Subtypes must be substitutable for their base types without altering the correctness of the program. This ensures that a derived class can stand in for its base class.

**Application in Angular:**
When you create components that extend from a base component, they should work seamlessly wherever the base component is expected.

**Code Snippet:**

export class BaseComponent {
  display() {
    console.log('Display base component');
  }
}

export class DerivedComponent extends BaseComponent {
  display() {
    console.log('Display derived component');
  }
}


**Real-World Use Case:**
If you replace BaseComponent with DerivedComponent in your application, it should function correctly without breaking any functionality.

**4. Interface Segregation Principle (ISP)**
**Definition:**
Clients should not be forced to depend on interfaces they do not use. This promotes creating smaller, more specific interfaces.

**Application in Angular:**
Instead of creating a large service interface that includes many methods, break it down into smaller, more focused interfaces.

**Code Snippet:**

export interface UserService {
  login(user: User): Observable<User>;
}

export interface NotificationService {
  sendNotification(message: string): void;
}


**Real-World Use Case:**
If you only need the login functionality in a specific component, you can depend solely on the UserService interface without needing to implement unused methods.

**5. Dependency Inversion Principle (DIP)**
**Definition:**
High-level modules should not depend on low-level modules. Both should depend on abstractions. This helps in decoupling your components from their dependencies.

**Application in Angular:**
Using dependency injection in Angular allows you to inject services rather than hard-coding dependencies.

**Code Snippet:**


@Injectable({
  providedIn: 'root',
})
export class AppService {
  constructor(private notificationService: NotificationService) {}

  notifyUser(message: string) {
    this.notificationService.sendNotification(message);
  }
}


**Real-World Use Case:**
By injecting NotificationService, you can easily swap out implementations (e.g., email, SMS) without changing the AppService logic.
