# When to use test-doubles

Use test doubles at **system boundaries** only:

- External APIs (payment, email, etc.)
- Databases (prefer InMemory DB)
- Time/randomness
- File system

Don't mock:

- Your own classes/modules
- Internal collaborators
- Anything you control

## Designing for Mockability

At system boundaries, design interfaces that are easy to mock:

**1. Use dependency injection**

Pass external dependencies in rather than creating them internally:

```kotlin
// Easy to fake
fun processPayment(order: Order, paymentClient: PaymentClient): Amount {
  return paymentClient.charge(order.total)
}

// Hard to fake
fun processPayment(order: Order): Amount {
  val client = StripeClient(STRIPE_KEY)
  return client.charge(order.total)
}
```

**2. Prefer SDK-style interfaces over generic fetchers**

Create specific functions for each external operation instead of one generic function with conditional logic:

```kotlin
// GOOD: Each function is independently mockable
interface Api {
  fun getUser(id: String): UserResponse
  fun getOrders(userId: String): List<Orders>
  fun createOrder(data: Data): OrderResponse
}

// BAD: Mocking requires conditional logic inside the test-double
interface Api {
  fun fetch(endpoint: Endpoint, options: Options): Response
}
```

The SDK approach means:
- Each mock returns one specific shape
- No conditional logic in test setup
- Easier to see which endpoints a test exercises
- Type safety per endpoint (concrete serializable responses)
