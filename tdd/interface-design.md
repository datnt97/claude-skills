# Interface Design for Testability

Good interfaces make testing natural:

1. **Accept dependencies, don't create them**

   ```cs
   // Testable — inject the dependency
    public decimal ProcessOrder(Order order, IPaymentGateway paymentGateway)
    {
        return paymentGateway.Charge(order.Total);
    }

    // Hard to test — creates its own dependency
    public decimal ProcessOrder(Order order)
    {
        var gateway = new StripeGateway(); // tightly coupled
        return gateway.Charge(order.Total);
    }
   ```

2. **Return results, don't produce side effects**

   ```typescript
   // Testable — pure function, returns a value
    public Discount CalculateDiscount(Cart cart)
    {
        var amount = cart.Total > 100 ? cart.Total * 0.1m : 0m;
        return new Discount(amount);
    }

    // Hard to test — mutates state, returns void
    public void ApplyDiscount(Cart cart)
    {
        cart.Total -= cart.Total * 0.1m; // side effect
    }
   ```

3. **Small surface area**
   - Fewer methods = fewer tests needed
   - Fewer params = simpler test setup
