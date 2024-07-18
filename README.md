# Python3 Code Development Programming Conventions

> 🎉 What makes code good? How to review others' code?

Generally, good code can be judged from the following 3 aspects:

1. **Readability**

   Throughout a code's lifecycle, it's mostly being read. Good code should be easily understood by others without extensive explanations or comments, **serving as its own documentation**.

   When writing code, consider not just how it feels to write, but **more importantly, how it feels for others to read**.

   **Readability enhances code maintainability**.

2. **Extensibility**

   Code should be updatable or modifiable to meet different requirements without breaking existing functionality. Extensibility helps maintain code usability amidst changing needs.

3. **Robustness**

   Code should work properly in various situations and handle exceptions (throwing exceptions is allowed, but unexplained crashes are not). Robust code helps prevent program crashes and data loss.

**Programming standards aim to promote higher quality code in these aspects.**

***

Based on constraint strength, this convention categorizes constraints as **[Mandatory]**, **[Recommended]**, and **[Reference]**. Each convention's explanation provides appropriate extension and interpretation. Positive examples show encouraged usage, while negative examples show usage to avoid.

For aspects that can be automatically formatted using tools like [Pylint](https://pylint.readthedocs.io/en/latest/), such as spaces around the assignment operator =, this convention doesn't mention them.

| There are only two hard things in Computer Science: cache invalidation and naming things. -- Phil Karlton |
| --- |

## I. Coding Conventions

1. **[Mandatory]** Code readability is crucial. During a code's lifecycle, it's mostly being read. Therefore, when multiple considerations conflict, please **prioritize** readability.

2. **[Mandatory]** Each line should not exceed 120 characters.
   * Explanation: Overly long lines cause reading barriers and make indentation ineffective.
   * Consider usage scenarios like horizontal screens, vertical screens, and git diff comparisons when determining characters per line.

3. **[Mandatory]** Leave 2 blank lines between top-level functions and class definitions in a module, 1 blank line between function definitions within a class, and only 1 blank line at the module's end.

4. **[Mandatory]** Use "is not" in conditional judgments instead of "not ... is".
   * Correct: if foo is not None:
   * Incorrect: if not foo is None:

5. **[Mandatory]** In function parameters, don't use mutable types as default values.
   * Correct:

    ```py
    def f(x=0, y=None, z=None):
        if y is None:
            y = []
        if z is None:
            z = {}
    ```
   * Incorrect:

    ```py
    def f(x=0, y=[], z={}):
        pass

    def f(a, b=time.time()):
        pass
    ```

6. **[Mandatory]** Don't define unused variables.

7. **[Mandatory]** A single function should not exceed 35 lines.
   * Explanation: Human reading memory is limited. Research shows short-term memory can only remember about 10 names simultaneously. When a function is too long (generally, longer than one screen), split it into smaller functions promptly.

8. **[Mandatory]** Don't use more than 2 for statements or filter expressions; use traditional for loop statements instead.
    * Explanation: When two for statements' list comprehension is complex, use traditional for loop statements.
    * Correct:

    ```py
    number_list = [1, 2, 3, 10, 20, 55]
    odd = [i for i in number_list if i % 2 == 1]

    result = []
    for x in range(10):
        for y in range(5):
            if x * y > 10:
                result.append((x, y))
    ```

    * Incorrect:

    ```py
    result = [(x, y) for x in range(10) for y in range(5) if x * y > 10]  
    ```

9. **[Mandatory]** List comprehensions are for simple scenarios. If the statement is too long, don't use list comprehensions.

    * Correct:

    ```py
    fizzbuzz = []
    for n in range(100):
        if n % 3 == 0 and n % 5 == 0:
            fizzbuzz.append(f'fizzbuzz {n}')
        elif n % 3 == 0:
            fizzbuzz.append(f'fizz {n}')
        elif n % 5 == 0:
            fizzbuzz.append(f'buzz {n}')
        else:
            fizzbuzz.append(n)
    ```

    * Incorrect:

    ```py
    # Conditions too complex, should use for statement
    fizzbuzz = [
        f'fizzbuzz {n}' if n % 3 == 0 and n % 5 == 0
        else f'fizz {n}' if n % 3 == 0
        else f'buzz {n}' if n % 5 == 0
        else n
        for n in range(100)
    ]
    ```

10. **[Mandatory]** Try to avoid using `from x import *`.

***

11. **[Recommended]** Variable names should be descriptive, not too broad. Good variable names greatly improve overall code readability.

    * Explanation: Within an **acceptable length**, the more precisely a variable name describes its content, the better. Avoid overly broad words as variable names.

    * Incorrect: day, host, cards, temp
    * Correct: day_of_week, hosts_to_reboot, expired_cards

12. **[Recommended]** Variable names should allow type guessing.

    * Explanation: Even after [PEP 484](https://www.python.org/dev/peps/pep-0484/), appropriate naming can help readers know variable types.

    * For boolean variables, use names modified by words like is, has, etc.

    * Correct: is_superuser, has_error, allow_vip, use_msgpack, debug [conventional]

    * Readers assume int or float types for number-related nouns.

    * Correct: Words interpreted as numbers: port, age, radius

    * Correct: Words starting/ending with length, count: length_of_username, max_length. Don't use simple plurals for int variables; use number_of_apples, trips_count instead of apples, trips.

13. **[Recommended]** Variable names shouldn't be too long or short; 1-5 words is appropriate.

    * Explanation: Generally, **avoid using** short names with only one or two letters. For array indices i, j, k, using names like person_index is always better.

14. **[Recommended]** Don't use variable names with negative meanings.

    * Correct: is_special
    * Incorrect: is_not_normal

15. **[Recommended]** Maintain consistent variable usage.

    * Explanation: If you call an image variable photo in one method, don't change it to image elsewhere. This confuses code readers: are image and photo the same thing?

16. **[Recommended]** Define variables close to their usage.

    * Explanation: Many beginners write all variable definitions together at the function/method start. This only makes code "look neat" without improving readability.

    * Better approach: **Define variables close to usage**. This helps readers understand code logic better, rather than struggling to figure out what a variable is and where it's defined.

17. **[Recommended]** Define temporary variables reasonably to improve readability.

    * Explanation: Clarify complex expressions by adding temporary variables.

    * Incorrect:

    ```py
    # Give 10000 coins to active female users or those with level > 3
    if user.is_active and (user.sex == 'female' or user.level > 3):
        user.add_coins(10000)
        return
    ```

    * Correct:

    ```py
    # Give 10000 coins to active female users or those with level > 3
    user_is_eligible = user.is_active and (user.sex == 'female' or user.level > 3):

    if user_is_eligible:
        user.add_coins(10000)
        return
    ```

    * Incorrect:

    ```py
    def get_best_trip_by_user_id(user_id):
        # Thinking: "This value might be modified/reused later", let's define it as a variable!
        user = get_user(user_id)
        trip = get_best_trip(user_id)
        result = {
            'user': user,
            'trip': trip
        }
        return result
    ```

    * Correct:

    The "future" you imagine never comes. Remove the three temporary variables:

    ```py
    def get_best_trip_by_user_id(user_id):
        return {
            'user': get_user(user_id),
            'trip': get_best_trip(user_id)
        }
    ```

18. **[Recommended]** Unless necessary, don't use `globals()`, `locals()`.

    * Explanation: You might be excited when discovering `globals()`, `locals()` and write extremely "concise" code:

    * Incorrect:

    ```py
    def render_trip_page(request, user_id, trip_id):
        user = User.objects.get(id=user_id)
        trip = get_object_or_404(Trip, pk=trip_id)
        is_suggested = judg_is_suggested(user, trip)
        # Using locals() saved three lines, I'm a genius!
        return render(request, 'trip.html', locals())
    ```

    * Never do this. It makes readers (including yourself in three months) hate you.

    * They need to remember all variables defined in this function, and locals() passes unnecessary variables.

    * [The Zen of Python](https://www.python.org/dev/peps/pep-0020/) says: **Explicit is better than implicit.** Therefore, recommend:

    * Correct:

    ```py
    return render(request, 'trip.html', {
            'user': user,
            'trip': trip,
            'is_suggested': is_suggested
        })
    ```

19. **[Recommended]** Avoid multi-level branch nesting.

    * Explanation: Try to avoid branch nesting. **Early termination** can optimize many branch nesting problems.

    * Incorrect:

    ```py
    def buy_fruit(nerd, store):
        """Go to fruit store to buy apples
        
        - First check if store is open
        - If apples available, buy 1
        - If not enough money, go home, get money, return
        """
        if store.is_open():
            if store.has_stocks("apple"):
                if nerd.can_afford(store.price("apple", amount=1)):
                    nerd.buy(store, "apple", amount=1)
                    return
                else:
                    nerd.go_home_and_get_money()
                    return buy_fruit(nerd, store)
            else:
                raise MadAtNoFruit("no apple in store!")
        else:
            raise MadAtNoFruit("store is closed!")
    ```

    * Correct:

    ```py
    def buy_fruit(nerd, store):
        if not store.is_open():
            raise MadAtNoFruit("store is closed!")

        if not store.has_stocks("apple"):
            raise MadAtNoFruit("no apple in store!")

        if nerd.can_afford(store.price("apple", amount=1)):
            nerd.buy(store, "apple", amount=1)
            return
        else:
            nerd.go_home_and_get_money()
            return buy_fruit(nerd, store)
    ```

20. **[Recommended]** Encapsulate overly complex logical judgments.

    * Explanation: If conditional branch expressions are too complex with many not, and, or, code readability greatly decreases.

    * Incorrect:

    ```py
    # If activity is open, remaining spots > 10, give 10000 coins to active female users or those with level > 3
    if activity.is_active and activity.remaining > 10 and \
            user.is_active and (user.sex == 'female' or user.level > 3):
        user.add_coins(10000)
        return
    ```

21. **[Recommended]** Always notice duplicate code under different branches.

    * Explanation: Duplicate code is the enemy of code quality, and conditional branches easily become hotspots for duplicate code. When writing conditional branches, pay special attention to **not producing** unnecessary duplicate code.

    * Incorrect:

    ```py
    # For new users, create new profile, otherwise update old profile
    if user.no_profile_exists:
        create_user_profile(
            username=user.username,
            email=user.email,
            age=user.age,
            address=user.address,
            # For new users, set points to 0
            points=0,
            created=now(),
        )
    else:
        update_user_profile(
            username=user.username,
            email=user.email,
            age=user.age,
            address=user.address,
            updated=now(),
        )
    ```

    * Correct:

    ```py
    if user.no_profile_exists:
        profile_func = create_user_profile
        extra_args = {'points': 0, 'created': now()}
    else:
        profile_func = update_user_profile
        extra_args = {'updated': now()}

    profile_func(
        username=user.username,
        email=user.email,
        age=user.age,
        address=user.address,
        **extra_args
    )
    ```

22. **[Recommended]** Multiple condition judgments: put more likely true conditions first in or expressions, and put and conditions at the end.

    ```py
    abbreviations = ["cf.", "e.g.", "ex.", "etc.", "flg."]

    for w in ("Mr.", "Hat", "is", "chasing", "."):
        if w in abbreviations and w[-1]=='.': # Poor performance
        # if w[-1] == '.' and w in abbreviations: # Better performance
            pass
    ```

23. **[Recommended]** Use De Morgan's law: not A or not B is equivalent to not (A and B), recommend using the former.

    * Explanation: Human thinking isn't good at handling many [negations] and [or] logical relationships.

    * Correct:

    ```py
    # If user not logged in or not using chrome, refuse service
    if not user.has_logged_in or not user.is_from_chrome:
        return "our service is only available for chrome logged in users"
    ```

    * Incorrect:

    ```py
    if not (user.has_logged_in and user.is_from_chrome):
        return "our service is only available for chrome logged in users"
    ```

24. **[Recommended]** Ask forgiveness, not permission.

    * Explanation: If code execution rarely produces exceptions, use try/except instead of pre-condition checks.

25. **[Recommended]** Use built-in all and any functions in judgment conditions for concise, efficient code.

26. **[Recommended]** For sequence (string, list, tuple) emptiness checks, don't use len function.
    * Correct:

    ```py
    if not seq:
       pass

    if seq:
       pass
     ```

    * Incorrect:

    ```py
    if len(seq):
       pass

    if not len(seq):
       pass
     ```

27. **[Recommended]** Use def to define short functions instead of lambda anonymous functions.
    * Explanation: Using def helps print effective type information in tracebacks.
    * Python once wanted to [remove](https://www.artima.com/weblogs/viewpost.jsp?thread=98196) [Lambda](https://www.artima.com/weblogs/viewpost.jsp?thread=98196), but compromised, [reference here](https://www.quora.com/Why-did-Guido-van-Rossum-want-to-remove-lambda-from-Python-3).


28. **[Recommended]** For frequently modified list definitions, dictionary definitions, and function parameters, it's recommended to place each element on a separate line and add a comma at the end of each line.
    * Correct example:

    ```py
    yes = ('y', 'Y', 'yes', 'TRUE', 'True', 'true', 'On', 'on', '1')  # Unlikely to change

    kwlist = [
        'False',
        ...
        'yield',  # Add a comma after the last element for easier future diffs
    ]

    person = {
        'name': 'bob',
        'age': 12,      # Might frequently add fields
        }
     ```

    * Incorrect example:

    ```py
    kwlist = ['False', 'None', 'True', 'and', 'as',
              'assert', 'async', ...
    ]

    person = {'name': 'bob', 'age': 12} # Frequently adding fields, not conducive for git diff
    ```

29. **[Recommended]** For long calculation expressions, operators should appear after the line break.
    * Correct example:

    ```py
    # YES: Easy to match operators with operands, improves readability
    income = (gross_wages
              + taxable_interest
              + (dividends - qualified_dividends)
              - ira_deduction
              - student_loan_interest)
     ```

    * Incorrect example:

    ```py
    # No: Operators are far from their operands
    income = (gross_wages +
              taxable_interest +
              (dividends - qualified_dividends) -
              ira_deduction -
              student_loan_interest)
    ```

30. **[Recommended]** Public functions, classes, and modules should include docstrings. For internally used functions, if the function name doesn't clearly indicate its purpose, comments should be provided.
    * Note: If a function is designed to be directly used by other developers, provide detailed documentation clarifying its meaning, inputs, outputs, and exceptions.

31. **[Recommended]** Docstrings must use triple double quotes """.

32. **[Recommended]** When using docstrings, it's recommended to use the reStructuredText style.

    * The opening triple quotes should not be followed by a line break. They should be immediately followed by a concise explanation of the module, function, class, or method's purpose, then an empty line before detailed explanations. The closing triple quotes should be on a separate line.

    * For function docstrings, the recommended general order is: overview, detailed description, parameters, return value, exceptions.

    * Generally, there's no need to describe implementation details unless they involve very complex algorithms.

    * Example:

    ```py
    def fetch_bigtable_rows(big_table: Table, keys: list[str], other_silly_variable: bool=None)->dict[str,Any]:
            """Fetches rows from a Bigtable.

            Retrieves rows pertaining to the given keys from the Table instance
            represented by big_table.  Silly things may happen if
            other_silly_variable is not None.

            :param big_table: An open Bigtable Table instance.
            :param keys: A sequence of strings representing the key of each table row
                to fetch.
            :param other_silly_variable: Another optional variable, that has a much
                longer name than the other args, and which does nothing.

            :return: A dict mapping keys to the corresponding table row data
                fetched. Each row is represented as a tuple of strings. For
                example:

                {'Serak': ('Rigel VII', 'Preparer'),
                'Zim': ('Irk', 'Invader'),
                'Lrrr': ('Omicron Persei 8', 'Emperor')}

                If a key from the keys argument is missing from the dictionary,
                then that row was not found in the table.

            :raises ValueError: if `keys` is empty.
            :raises IOError: An error occurred accessing the bigtable.Table object.
            """
            pass
    ```

33. **[Recommended]** When re-raising an existing exception in an except clause, use `raise` instead of `raise ex`.

     * Correct example:

    ```py
     try:
           int("hello")
       except ValueError:
           raise # Can preserve the original traceback
            
     Traceback (most recent call last):
     File "～/temp.py", line 2, in <module>
         int("hello")
     ValueError: invalid literal for int() with base 10: 'hello'

       try:
           raise MyException()
       except MyException as ex:
           raise AnotherException(str(ex))  # Allowed: Recommended to preserve previous exception stack info for problem localization
      ```

     * Incorrect example:

    ```py
     try:
           int("hello")
       except ValueError as e:
           raise e # Exception stack info starts from here
     Traceback (most recent call last):
       File "～/temp.py", line 2, in <module>
         raise e
       File "～/temp.py", line 2, in <module>
         int("hello")
     ValueError: invalid literal for int() with base 10: 'hello'
      ```

34. **[Recommended]** The code in all try/except clauses should be as minimal as possible to avoid masking other errors.

    ```py
    try:
        value = collection[key]
    except KeyError:
        return key_not_found(key)
    else:
        return handle_value(value)
    
    # Incorrect example
    try:
        # Too broad scope
        return handle_value(collection[key])
    except KeyError:
        # Will catch KeyError in handle_value() as well
        return key_not_found(key)
    ```

35. **[Recommended]** Functions should have a single return type, not different types [allowing None].

    * Correct example:

    ```py
    def add(a, b):
        if isinstance(a, int) and isinstance(b, int):
            return a + b
        else:
            raise Exception("Only int are allowed")
    ```

    * Incorrect example:

    ```py
    def add(a, b):
        if isinstance(a, int) and isinstance(b, int):
            return a + b
        else:
            return str(a) + str(b)
    ```

36. **[Recommended]** For unknown condition branches or branches that shouldn't be entered, exceptions should be raised rather than returning a value [like None, False].

    * Correct example:

    ```py
    def foo(x):
        if x in ('SUCCESS',):
            return True
        else:
            # If a condition that should never be reached, add an exception to prevent future unknown statements from executing.
            raise Exception() 
     ```

    * Incorrect example:

    ```py
    def foo(x):
        if x in ('SUCCESS',):
            return True
        return None
     ```

37. **[Reference]** Python syntax should be fully utilized, but avoid overusing Python's tricks.

    * Note: For example, Python's Slice syntax

    * Correct example:

    ```py
    a = [1, 2, 3, 4]
    c = 'abcdef'
    print(list(reversed(a)))
    print(list(reversed(c)))
     ```

    * Incorrect example:

    ```py
    a = [1, 2, 3, 4]
    c = 'abcdef'
    print(a[::-1])
    print(c[::-1])
     ```

38. **[Reference]** Use dict to return multiple values.

    ```py
    # A function returning multiple values
    def latlon_to_address(lat, lon):
        return country, province, city

    # However, this usage can create a small problem:
    # What if one day, the latlon_to_address function needs to add a return for "District"?
    # If written like above, you'd need to find all places calling latlon_to_address,
    # add this extra variable, otherwise it will raise a ValueError: too many values to unpack exception.
    ```

    * For such multi-return value functions that might change, using dict would be more convenient. When you add new return values, it won't cause any breaking changes to previous function calls.

    ```py
    def latlon_to_address(lat, lon):
        return {
            'country': country,
            'province': province,
            'city': city
        }

    addr_dict = latlon_to_address(lat, lon)
    ```

39. **[Reference]** Refer to the standard library more often, as it contains many good features. Such as `operator.methodcaller()`, etc.

40. **[Reference]** Use `[]`, `{}` instead of `list`, `dict` (faster speed).

41. **[Reference]** Use for/else to simplify exception handling.

    * The following two code snippets are equivalent

    * We used a flag `found` to determine if the loop ended due to a break statement

    ```py
    def find_index(nums: list[int], target: int) -> None:
        found = False
        for index, num in enumerate(nums):
            if num == target:
                found = True
                break

        if found:
            print("not find {target}")
        else:
            print("find {target} at index {index}")
    ```

    ```py
    def find_index(nums: list[int], target: int) -> None:
        for index, num in enumerate(nums):
            if num == target:
                print("find {target} at index {index}")
                break
        else:
            print("not find {target}")
    ```

## II. Coding Principles

This section provides some coding guidance, especially on how to make decisions when multiple syntactically correct ways of writing exist.

1. **[Recommended]** Offensive implementation, defensive calling

   * For implementation: No one can guarantee their code will "perfectly" handle all cases.

   * For calling: There's no error-free code, but no one wants their system to crash due to someone else's carelessness (assuming external systems are unstable).

2. **[Recommended]** Don't be correct for the sake of being correct, hiding errors

   * For a dictionary `my_dict`, if the key `my_key` is a necessary key. Never write `my_dict.get(my_key)`. Such programs only **mysteriously** **work**. According to Murphy's Law, someday this code will trip up the entire team.

   * When necessary, use exceptions to notify upper layers of unpredictable errors. Exceptions need to carry necessary information to help quickly locate the problem.

   * Incorrect example:

    ```py
   value = my_dict.get(my_key)
    ```

   * Correct example:

    ```py
    value = my_dict[my_key] # my_key must exist

    # or
    if my_key not in my_dict:
        raise KeyError
    ```

3. **[Recommended]** Don't amplify errors

   * `raise` is not used to shift responsibility. Reasonable `assert`, `raise` only declares to the outside: my code has encountered an error that cannot be ignored. The caller of the code must be responsible for handling this error (because I declared it cannot be ignored).

   * Maintainer: `raise` is not shifting responsibility, maintainers have the obligation to throw and only throw cases that are considered incorrect.

   * Caller: When calling someone else's function, you should follow their specifications. The caller needs to judge whether to continue to `raise` to the upper layer.

4. **[Recommended]** Strictly investigate infinite loops

   * No matter how small a `while true` loop is, when the break condition cannot be triggered (due to various bugs), our service will die.

5. **[Recommended]** Handle exceptions reasonably

    * Code can't never go wrong, reasonable error handling can improve code robustness. For error handling situations, they can be roughly divided into three categories.

    * Exceptions the caller doesn't care about: Replace with a degraded function (ensure the degraded function won't go wrong)

    * Critical functionality exceptions: Use `raise` to throw

    * Important but shouldn't affect the main process exceptions: Degraded function + log alarm

6. **[Recommended]** Uniform interface return types

    * Try to keep interface return types uniform, reduce returning None values.

    ```py
    def get_number_list(num: int):
        if num < 10:
            return 0
        elif 10 <= num < 100:
            return [10 for i in range(10)]
        else:
            return None
    ```

   * A function named `get_number_list` should always return an array or throw an exception.

7. **[Recommended]** Only do what you're supposed to do

    ```py
    def pickup_slotcard(feeds):
        ...
        for feed in feeds:
            if feed.type == slot_card:
                return format_feed(slot_card)
        return None
    ```

   * `pickup_slotcard`: Find the slot card in the feed, just be responsible for finding, don't do other things.

   * `format_feed` doesn't need to be done.

8. **[Recommended]** Try to avoid default parameters

    * Default means the parameter can be not passed, which can easily confuse the caller: should it be passed or not?

    * Irresponsible caller: Just don't pass it.

    * Responsible caller: Look at the documentation, code to know how to pass.

    * Code maintainer: If the default value is modified, all calling places must be checked.

9. **[Recommended]** Reasonable layering, judging whether parameters are reasonable

   * For those parameters that are just for controlling the calling process, consider splitting into separate functions.

    ```py
    def func(control, a, b ,c):
        if control == 1:
            pass
        elif control == 2:
            pass
        else:
            pass
    return

    # Only implement functional logic, calling manages business logic
    def f_control_1(a, b, c): 
        ...
    def f_control_2(a, b, c):
        ...
    def f_control_3(a, b, c):
        ...
    ```

10. **[Recommended]** Class design, use less inheritance, more composition.

    * Too deep inheritance chains will lead to exponential increase in code maintenance costs.

11. **[Recommended]** Compress class attributes.

    * If a class has many interrelated attributes, some of which are derived from other attributes. Then such attributes should be removed, instead using `get_xx` methods to obtain, or using `property`.

    * Without derived attributes, the class's `__init__` becomes simple, the testability of the code is improved, and maintainability is improved.

    ```py
    class Sample:

        def __init__(self, price: float, amount: int):
            self.price = price
            self.amount = amount

        @property
        def profit(self):
            return self.price * self.amount
    ```

12. **[Recommended]** Prohibit changing function signatures [Liskov Substitution Principle]

    * All places where parent class methods are used can be replaced with subclasses without producing code syntax errors or type errors.

    ```py
    class Base:
        def func(self, a: int):
            raise NotImplementedError()


    class ClassA(Base):
        def func(self, a: int):
            pass


    class ClassB(Base):
        def func(self, a: int):
            pass


    class ClassC(Base):
        def func(self, b: list[str]):  # The author feels the parameter is not satisfactory
            pass
            
    # Code caller
    ClassA().func(a)   # no bug
    ClassB().func(a)   # no bug
    ClassC().func(a)   # bug?  why?  How did it crash??? Did the code maintainer's brain short-circuit?
    ```

13. **[Recommended]** Consider the user's feelings

    * **When writing code, [considering how to write or how to use]** is an important indicator to distinguish whether it's an excellent engineer. Code that is only friendly to the author can definitely not be called excellent code. Oriented to engineering, oriented to cooperation, make the user comfortable, make the user's **psychological cost low.**

14. **[Recommended]** Later equals never [LeBlanc's Law]

   * If the old architecture can't meet new requirements, then it needs to be adjusted, and adjusted as soon as possible.

   * Reasonable refactoring at reasonable times can keep the architecture vibrant enough, rather than "next time". All new features should be

# Python Coding Standards and Best Practices

## I. Design Principles

15. **[Recommended]** Strive for stateless design

    * Stateful code significantly reduces maintainability and testability. When testing code, maintainers need to painfully construct context, and debugging scenarios are difficult to reproduce.

16. **[Recommended]** Delete unused code (YAGNI principle)

   * You Ain't Gonna Need It, benefits:

   * Saves engineering costs, avoids writing unnecessary code, and eliminates the need to maintain such code.

   * Improves code quality by preventing temporarily or permanently useless code from polluting the project.

   * Developers should not write useless logic, nor should they allow the existence of useless logic. All offline logic (commented-out code, uncalled functions, conditions that are always False) must be removed!

   * If needed in the future, you can rely on git version control, repository tagging, documentation maintenance of commit nodes, etc. There are countless more efficient solutions than commenting out code.

17. **[Recommended]** Good code is better than comments [Code itself is documentation]

   * Good variable and function naming is the best form of documentation.

   * Because comments have no mechanism to ensure forced updates, outdated comments can easily cause more confusion in understanding for others. Code that relies on comments may deteriorate from "engineering-oriented" to "documentation-oriented". The codebase becomes filled with explanations of what a hundreds-line function does, yet no one can understand it.

18. **[Recommended]** Reduce variables, keep variables as local as possible

   * Intermediate assignments and logic writing for variables are often the fuse for bizarre bugs in code. Restrict the use of variables to the smallest possible scope.

   * You can use sub-functions, code blocks, and other means to reduce the situation of variables flying everywhere.

19. **[Recommended]** Interface Segregation Principle

   * A class or method should not depend on interfaces it doesn't need (similar to the Single Responsibility Principle).

20. **[Recommended]** Dependence Inversion Principle

   * High-level methods should not depend on low-level methods; both should depend on abstractions.

## II. Type Annotations

**Why are Python type annotations (Type Annotation) becoming increasingly important and widely used?**

1. Improves code readability: Type annotations make it easier for developers to understand the expected inputs and outputs of functions, classes, and methods, greatly improving code readability and making it easier for others to maintain and extend the code.

2. Better documentation: Type annotations provide clear explanations about the input and output types of functions without the need for additional comments (code as documentation).

3. Tool support: Many IDE tools and linters can provide code improvement suggestions, error checking, and refactoring support based on type annotations.

4. Improves code quality: Type annotations can help developers detect potential errors early in the development process, as type mismatches can be detected at compile time.

5. Better performance: Type annotations can also be used by tools to generate optimized code, resulting in faster and more efficient programs.

6. Related documentation: [Reference 1](https://yothinix.medium.com/python-type-annotation-and-why-we-need-it-91820a708170), [Reference 2](https://bernat.tech/posts/the-state-of-type-hints-in-python/), [Reference 3](https://medium.com/python-supply/advantages-of-type-annotations-6c6eb70fa631), [Reference 4](https://towardsdatascience.com/python-type-annotations-and-why-you-should-use-them-6f647c6b4e9c), [Reference 5](https://florimond.dev/en/posts/2018/07/why-i-started-using-python-type-annotations-and-why-you-should-too/), [PEP 484](https://peps.python.org/pep-0484/)

Therefore, it is **strongly recommended to use type annotations** during Python programming. Starting from Python 3.5, Python introduced typing as a standard library.

## III. Code Review

> **The purpose of requesting others to review code when submitting a PR**

1. Discover unreasonable code structure design, improve code quality, readability, maintainability, and testability.

2. Reduce communication costs between developers, encourage developers to help each other learn.

3. Code Review is not about finding fault. Don't deliberately look for bugs, don't nitpick, don't turn code review into a criticism session.

4. When encountering unreasonable situations, first understand the project background; it may be due to an unreasonable existing architecture. Aim to **not compromise, not be stubborn, and jointly improve the framework**.

5. Controversial issues can be temporarily set aside [note down the problem, organize thoughts, discuss in a meeting].

> **When reviewing code, you can grade the Code Review**

1. [request] xxxxxxx　　　　　　　The code in this comment **must** be modified for approval

2. [advise] xxxxxxxx　　　　　　　It is **recommended** to modify the code in this comment, but it can be approved without modification

3. [question] xxxxxx　　　　　　　There are questions about the code in this comment, requiring further explanation from the code submitter

## IV. Further Reading

Some Python specification documents and inspection tools:

1. [Python Enhancement Proposals](https://peps.python.org/pep-0008/)
2. [The Zen of Python](https://peps.python.org/pep-0020/)
3. [PreCommit](https://ljvmiranda921.github.io/notebook/2018/06/21/precommits-using-black-and-flake8/)
4. [Pylint](https://pylint.readthedocs.io/en/latest/)
5. [Pyright](https://github.com/microsoft/pyright)
6. [Mypy](https://mypy.readthedocs.io/en/stable/command_line.html)
