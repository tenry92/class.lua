# class.lua

This repository provides a code snippet that allows you to write classes in the
Lua scripting language, compatible with Lua 5.3.


# Features

 - Constructor and destructor (`construct` and `destruct` methods)
 - Inheritance (`Class(BaseClass)`, `SubClass.super`)
 - Getters and setters (`getXxx` and `setXxx` methods and use `xxx` as the
   virtual properties)


# Usage

Just load the `class.lua` file in your Lua runtime environment and a function
named `Class` is available. If you prefer another name, or want to `require`
the file and return the function instead of creating a new global, feel free to
modify the source code.


~~~Lua
-- load `Class` into the global environment
require('class')

-- create a new class, named `BaseClass`
local BaseClass = Class()

-- constructor function must be named `construct`
function BaseClass:construct(text)
  print('Constructing BaseClass:', self)
  self.text = text
end

-- if this instance is being garbage collected, this is called
function BaseClass:destruct()
  print('Destructing BaseClass:', self)
end

-- regular method
function BaseClass:sayIt()
  print(self.text)
end

-- setter method must have the form `setXxx`
function BaseClass:setFoobar(value)
  print('Set foobar to:', value)
end

-- getter method must have the form `getXxx`
function BaseClass:getFoobar()
  print('Get foobar')
  return 27
end

local instance = BaseClass('Welcome class.lua!')
instance:sayIt() -- call regular method
instance.text = 'modified' -- modify regular property
instance.foobar = 'setting' -- uses setFoobar()
print(instance.foobar) -- uses getFoobar()


local SubClass = Class(BaseClass)

function SubClass:construct()
  SubClass.super.construct(self, 'lorem ipsum dolor')
  -- or: BaseClass.construct(self, 'lorem ipsum dolor')
end
~~~


## License

It's licensed under the MIT License.