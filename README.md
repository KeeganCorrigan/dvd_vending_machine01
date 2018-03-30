## DVD Vending Machine
Using Test Driven Development, build a program for managing a DVD Vending Machine.

## Submission instructions

1. Fork this [repo](https://github.com/charliecorrigan/dvd_vending_machine01)
2. Clone your fork
3. Push your solution to your fork
4. Use Github's interface to create a pull request

### Iteration 0 - Customers

Customers have names and rentals. They start with no rentals, but rentals can be added and removed. Customers should follow this interaction pattern:

```ruby
bob = Customer.new("Bob")
#=> #<Patron:0x00007fdf16ba6128 @rentals=[], @name="Bob">
> bob.name
#=> "Bob"
> bob.rentals
#=> []
> bob.add_rental("Kill Bill Vol. 1")
> bob.add_rental("Ghostbusters")
> bob.rentals
#=> ["Kill Bill Vol. 1", "Ghostbusters"]
> bob.return_rental("Ghostbusters")
> bob.rentals
#=> ["Kill Bill Vol. 1"]
```

### Iteration 1 - VendingMachine

A VendingMachine has a location and DVDs. Each DVD has a cost. A VendingMachine starts with no DVDs, but DVDs can be added. When we add a DVD, we must specify the DVD title and the DVD cost. VendingMachines should follow this interaction pattern:

```ruby
> vendor = VendingMachine.new("17th and Market")
> vendor.location
#=> "17th and Market"
> vendor.add_dvd("Kill Bill Vol. 1", 2)
> vendor.add_dvd("Ghostbusters", 1)
```

### Iteration 2 - Customer Memberships and Revenue

VendingMachines allow customers to become members. When a Customer becomes a member, the VendingMachine gets 10 dollars for general membership the first time a customer rents a dvd, plus revenue for each DVD the customer rents. Follow this interaction pattern:

```ruby
> vendor = VendingMachine.new("17th and Market")
> vendor.add_dvd("Kill Bill Vol. 1", 3)
> vendor.add_dvd("Ghostbusters", 1)
> vendor.add_dvd("Little Shop of Horrors", 1)
>
> vendor.revenue
#=> 0
>
> bob = Customer.new("Bob")
>
> vendor.revenue
#=> 0
>
> bob.add_rental("Kill Bill Vol. 1")
> bob.add_rental("Ghostbusters")
>
> sally = Patron.new("Sally")
> sally.add_rental("Little Shop of Horrors")
>
> vendor.revenue
#=> 25
>
```

### Iteration 3 - DVD Tracking

DVDs should have a property called `checked_out` and its value should be a boolean. Its default value is `false`. When a customer rents a DVD, it should change the value of `checked_out` to `true`

Add the following methods to your `VendingMachine` class:

* `circulation_of(dvd)` - this method returns the number of times a dvd has been rented.

* `dvds_by_circulation` - this method returns an array of DVDs sorted from most times rented to the least times rented.

* `remove_unpopular_dvds(threshold)` - this method will remove any dvd where the number of times it has circulated is less than the threshold.

### Iteration 4 - Other Stuff

If a customer tries to rent a DVD that does not exist in the vending machine, that DVD should NOT be added to their rentals.

DVDs should only be able to be checked out by one customer at a time. If a customer tries to checkout a DVD that is already rented by someone else, that DVD should NOT be added to their rentals.