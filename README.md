1)  How many users are there?

    51, User.count

2)  What are the 5 most expensive items?

    Item.order("price").last(5)

    title: "Ergonomic Steel Car",
    price: 9341>,

    title: "Sleek Wooden Hat",
    price: 9390>,

    title: "Awesome Granite Pants",
    price: 9790>,

    title: "Small Wooden Computer",
    price: 9859>,

    title: "Small Cotton Gloves",
    price: 9984>]


3)  What’s the cheapest book?

    Item.where("category LIKE ?", "%book%").order("price").first

    title: "Ergonomic Granite Chair",
    category: "Books",
    price: 1496>

4)  Who lives at “6439 Zetta Hills, Willmouth, WY”? Do they have another address?

    step 1) Address.find_by street: "6439 Zetta Hills"
    step 2) User.find_by id: "40"
    step 3) Address.where(user_id: "40")

    id: 40,
    first_name: "Corrine",
    last_name: "Little",
    email: "rubie_kovacek@grimes.net">

    Yes, she has 2 addresses:

    => [#<Address:0x007f80d93dba88
      id: 43,
      user_id: 40,
      street: "6439 Zetta Hills",
      city: "Willmouth",
      state: "WY",
      zip: 15029>,
     #<Address:0x007f80d93db920
      id: 44,
      user_id: 40,
      street: "54369 Wolff Forges",
      city: "Lake Bryon",
      state: "CA",
      zip: 31587>]

5)  Correct Virginie Mitchell’s address to “New York, NY, 10108”.

    Address.update(41, city: "New York", zip: 10108)

    Address.where(user_id: 39).update_all(city: "New York", zip :10108)



6)  How much would it cost to buy one of each tool?

    $46,477

    Item.where("category LIKE ?", "%tool%").sum("price")

7)  How many total items did we sell?

    2,127

    Order.sum("quantity")

8)  How much was spent on books?

    book_orders = Item.joins("JOIN orders ON orders.item_id = items.id").where(category:"Books")
    book_orders.sum("price * quantity")

9)  Simulate buying an item by inserting a User for yourself and an Order for that User.

    User.create(first_name: "Mike", last_name: "Pitre", email: "michaelepitre@gmail.com")
    Order.create(item_id: 30, quantity: 2)
