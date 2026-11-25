# Good and Bad Tests

## Good Tests

**Integration-style**: Test through real interfaces, not mocks of internal parts.

```kotlin
// GOOD: Tests observable behavior
@Test
fun `user can checkout with valid cart`() = runTest {
  val cart = createValidCart(product)
  val viewModel = CheckoutViewModel(cart)

  viewModel.checkout(cart, paymentMethod)

  assertThat(viewModel.uiState.value).isEqualTo(UiState.Confirmed)
}
```

Characteristics:

- Tests behavior users/callers care about
- Uses public API only
- Survives internal refactors
- Describes WHAT, not HOW
- One logical assertion per test

## Bad Tests

**Implementation-detail tests**: Coupled to internal structure.

```kotlin
// BAD: Tests implementation details
@Test
fun `checkout calls paymentService process`() = runTest {
  val mockPayment = mockk<PaymentService>()
  val viewModel = PaymentViewModel(mockPayment)

  viewModel.checkout(cart, payment)

  verify { mockPayment.process(cart.total) }
}
```

Red flags:

- Mocking internal collaborators
- Testing private methods
- Asserting on call counts/order
- Test breaks when refactoring without behavior change
- Test name describes HOW not WHAT
- Verifying through external means instead of interface