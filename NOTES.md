# HW1 notes

Answer each question in a few sentences. Be specific: name the function, the error or the command.

## What did you try?

I ran `python -m pytest` first to see what the tests expect, then filled in `delivery.py` In `MenuItem.__init__` the price is set with `self.price = price`, so it goes through the setter, and the setter raises `ValueError` when the value is 0 or less before it touches `self._price`, which keeps the old price. `__repr__` uses `type(self).__name__` so a `PromoItem` prints its own class name, and `__eq__` returns `NotImplemented` when the other object is not a `MenuItem`. `PromoItem.cost` takes `quantity // 3` as the free items and asks `super().cost()` for the rest. `Order.__init__` stores `list(lines)` so it never shares the caller's list, `total` sums `item.cost(quantity)` and adds the 30 baht fee only below 300, and `cheapest` uses `min` with `total()` as the key.

## What broke, and how did you fix it?

On the first run all 14 tests failed with `NotImplementedError`. Most of them stopped at the same place, `MenuItem.__init__` in `delivery.py` line 10, because almost every test creates a `MenuItem` first. That showed me `MenuItem` had to be done before anything else. After all the functions were filled in, `python -m pytest` showed `14 passed`.

## What would you do differently next time?

I would write one function at a time and run `python -m pytest` after each one, like the README says, instead of filling in the whole file and running the tests once. I would also add my own small checks for the edges, for example food that costs exactly 300 baht or a `PromoItem` with a quantity of 3. I want to practise `PromoItem.cost` and `Order.__init__` again without help until I can explain them myself.