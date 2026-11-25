# Interface Design for Testability

Good interfaces make testing natural:

1. **Accept dependencies, don't create them**

   ```kotlin
   // Testable
   fun processOrder(order: Order, paymentGateway: PaymentGateway) {}

   // Hard to test
   fun processOrder(order: Order) {
     val gateway = StripeGateway()
   }
   ```

2. **Return results, don't produce side effects**

   ```kotlin
   // Testable
   fun calculateDiscount(cart: Cart): Discount {}

   // Hard to test
   fun applyDiscount(cart: Cart) {
     cart.total -= discount
   }
   ```

3. **Small surface area**
   - Fewer methods = fewer tests needed
   - Fewer params = simpler test setup
