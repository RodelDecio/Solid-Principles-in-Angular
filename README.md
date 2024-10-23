# Activity 25: SOLID Principles in Angular

## Understanding SOLID Principles and Their Application in Angular

In software development, **SOLID** principles are a set of design principles that make code more maintainable, scalable, and flexible. They guide developers in building robust systems by promoting modularity and reducing complexity. Angular, being a popular framework for building client-side applications, benefits greatly from these principles. In this article, we will explore the **SOLID** principles, how they apply to Angular, and include real-world examples and code snippets to clarify each concept.

---

## S - Single Responsibility Principle (SRP)

The **Single Responsibility Principle** states that a class should have one, and only one, reason to change. This means that a class should only perform one task or responsibility.

### Example in Angular

In Angular, services are used to handle business logic separately from components, promoting SRP.

```typescript
// Bad Practice: Component handling multiple responsibilities
@Component({
  selector: 'app-user',
  templateUrl: './user.component.html',
})
export class UserComponent {
  user = { name: 'John', age: 22 };

  // Handles both user data and logging responsibility
  logUserInfo() {
    console.log('User Info:', this.user);
  }
}
```

### Refactor using SRP:

```typescript
// Good Practice: Separate responsibility into a service
@Injectable({
  providedIn: 'root',
})
export class LoggerService {
  log(message: string) {
    console.log(message);
  }
}

@Component({
  selector: 'app-user',
  templateUrl: './user.component.html',
})
export class UserComponent {
  user = { name: 'John', age: 22 };

  constructor(private logger: LoggerService) {}

  logUserInfo() {
    this.logger.log(`User Info: ${this.user.name}, Age: ${this.user.age}`);
  }
}
```

By applying SRP, you can separate the business logic into services, making the components lighter and easier to maintain.

---

## O - Open/Closed Principle (OCP)

The **Open/Closed Principle** states that a class should be open for extension but closed for modification. This means that you should be able to extend a class’s behavior without modifying its existing code.

### Example in Angular

In Angular, you can extend components or services through inheritance, or by using strategies like dependency injection.

```typescript
// Bad Practice: Directly modifying an existing class
@Injectable({
  providedIn: 'root',
})
export class PaymentService {
  processPayment() {
    console.log('Processing payment');
  }
}
```

### Refactor using OCP:

```typescript
// Good Practice: Extend functionality without modifying existing class
@Injectable({
  providedIn: 'root',
})
export class PaymentService {
  processPayment() {
    console.log('Processing payment');
  }
}

@Injectable({
  providedIn: 'root',
})
export class CreditCardPaymentService extends PaymentService {
  processPayment() {
    console.log('Processing credit card payment');
  }
}
```

Instead of modifying the `PaymentService` each time, you can extend it, adhering to the OCP principle.

---

## L - Liskov Substitution Principle (LSP)

The **Liskov Substitution Principle** states that objects of a superclass should be replaceable with objects of a subclass without affecting the functionality of a program.

### Example in Angular

You can create services that can be replaced or substituted easily in different parts of the app.

```typescript
// Base Service
@Injectable({
  providedIn: 'root',
})
export class PaymentService {
  processPayment() {
    console.log('Processing payment');
  }
}

// Substitutable Service
@Injectable({
  providedIn: 'root',
})
export class PaypalPaymentService extends PaymentService {
  processPayment() {
    console.log('Processing PayPal payment');
  }
}
```

When switching between different payment methods, you can substitute one payment service for another without changing the dependent components, preserving LSP.

---

## I - Interface Segregation Principle (ISP)

The **Interface Segregation Principle** suggests that clients should not be forced to implement interfaces they do not use. Instead, multiple small, specific interfaces are preferred over a large, generalized one.

### Example in Angular

You can define multiple small interfaces and implement only what is needed in the services or components.

```typescript
// Bad Practice: Large interface with unnecessary methods
interface AuthService {
  login(): void;
  logout(): void;
  register(): void;
  resetPassword(): void;
}

// Good Practice: Split interface into smaller, focused ones
interface LoginService {
  login(): void;
}

interface LogoutService {
  logout(): void;
}

@Injectable({
  providedIn: 'root',
})
export class UserService implements LoginService, LogoutService {
  login() {
    console.log('User logged in');
  }

  logout() {
    console.log('User logged out');
  }
}
```

By applying only the required interfaces, you can make your classes more flexible, adhering to ISP.

---

## D - Dependency Inversion Principle (DIP)

The **Dependency Inversion Principle** states that high-level modules should not depend on low-level modules. Both should depend on abstractions.

### Example in Angular

In Angular, services are injected into components, adhering to DIP by decoupling the high-level logic from low-level implementations.

```typescript
// Bad Practice: Direct dependency on a low-level service
@Component({
  selector: 'app-payment',
  templateUrl: './payment.component.html',
})
export class PaymentComponent {
  paymentService = new PaypalPaymentService();

  processPayment() {
    this.paymentService.processPayment();
  }
}
```

### Refactor using DIP:

```typescript
// Good Practice: Depend on abstraction (interface or token)
@Component({
  selector: 'app-payment',
  templateUrl: './payment.component.html',
})
export class PaymentComponent {
  constructor(private paymentService: PaymentService) {}

  processPayment() {
    this.paymentService.processPayment();
  }
}
```

By injecting services through dependency injection, you can easily switch between different implementations without modifying the components.

---

## Hashnode Link:
 [Activity 25: SOLID Principles in Angular](https://activity4gitfundamentalsdocumentation.hashnode.dev/activity-25-solid-principles-in-angular)
```

