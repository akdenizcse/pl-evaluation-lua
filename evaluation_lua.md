# Lua Evaluation
Lua evaluation homework for Programming Languages course Akdeniz University Computer Sciences Department. Ege Yıldır - April 2020

Lua is a powerful, efficient, lightweight, embeddable scripting language. It supports many paradigms: procedural programming, object-oriented programming, functional programming, data-driven programming, and data description.

It has built on top of C programming language. Lua has its value across multiple platforms ranging from large server systems to small mobile applications.

## Lua History

Lua is an extensible, lightweight programming language written in C. It started as a house project in 1993 by Roberto Ierusalimschy, Luiz Henrique de Figueiredo, and Waldemar Celes. Lua was born and raised in Tecgraf, formerly the Computer Graphics Technology Group of PUC-Rio. Lua is now housed at LabLua, a laboratory of the Department of Computer Science of PUC-Rio.

## Authors

- **Roberto Ierusalimschy** : 
Professor in the Department of Computer Science at PUC-Rio.
Head of LabLua.
- **Waldemar Celes** : Professor in the Department of Computer Science at PUC-Rio.
Researcher at Tecgraf.
- **Luiz Henrique de Figueiredo** : Researcher at IMPA. Former consultant at Tecgraf.

## What Lua Means

"Lua" means "Moon" in Portuguese. It is not an acronym nor an abbreviation, but a noun. To be specific, "Lua" is a name, the name of the Earth's moon (like "Luna") and the name of the language. Like most names, it should be written in lower case with an initial capital, that is, "Lua". Writing "LUA" is ugly and can lead confusion.

## Why Lua
Lua is an academic project and differs from the other languages with this property. It has different pressures compared to other projects. This creating a disadvantage of not having live feedback, but also led to an elegant well working small and fast language.

### Lua is a proven, robust language
Lua has been used in many industrial applications (e.g., Adobe's Photoshop Lightroom), with an emphasis on embedded systems (e.g., the Ginga middleware for digital TV in Brazil) and games (e.g., World of Warcraft and Angry Birds). Lua is one of the best languages for game development. Lua has a solid reference manual and there are several books about it. Several versions of Lua have been released and used in real applications since its creation in 1993. Lua won the Front Line Award 2011 from the Game Developers Magazine.

### Lua is fast
Lua has a deserved reputation for performance. To claim to be "as fast as Lua" is an aspiration of other scripting languages. Several benchmarks show Lua as the fastest language in the realm of interpreted scripting languages. Lua is fast in fine-tuned benchmark programs and real life both. Substantial fractions of large applications have been written in Lua.

### Lua is portable
Lua is distributed in a small package and builds out-of-the-box in all platforms that have a standard C compiler. Lua runs on all flavors of Unix and Windows, on mobile devices (running Android, iOS, BREW, Symbian, Windows Phone), on embedded microprocessors (such as ARM and Rabbit, for applications like Lego MindStorms), on IBM mainframes, etc.

### Lua is embeddable
Lua is a fast language engine with small footprint that you can embed easily into your application. Lua has a simple and well documented API that allows strong integration with code written in other languages. It is easy to extend Lua with libraries written in other languages. It is also easy to extend programs written in other languages with Lua. Lua has compatibility between C and C++, Java, C#, Smalltalk, Fortran, Ada, Erlang, and even in other scripting languages, such as Perl and Ruby.

### Lua is powerful
A fundamental concept in the design of Lua is to provide meta-mechanisms for implementing features, instead of providing a host of features directly in the language. For example, although Lua is not a pure object-oriented language, it does provide meta-mechanisms for implementing classes and inheritance. Lua's meta-mechanisms bring an economy of concepts and keep the language small, while allowing the semantics to be extended in unconventional ways.

### Lua is small
Adding Lua to an application does not bloat it. The tarball for Lua 5.3.5, which contains source code and documentation, takes 297K compressed and 1.2M uncompressed. Being that compact, Lua finds a place for itself anywhere.

### Lua is free
Lua is free open-source software, distributed under MIT license. It may be used for any purpose, including commercial purposes, at absolutely no cost.

## Setting Up Lua
Lua has an online demo if you just want to try it. Visit https://www.lua.org/demo.html . To run Lua on your computer, you have to download Lua interpreter. You may want ZeroBrane Studio as an IDE but you can use your favorite text editor also. 

If you use Windows, you can use LuaDist.

If you use Mac or Linux, you may already have Lua or there is a package for it.

### Building Lua
Lua is easy to build, try this if you use Linux:

```
curl -R -O http://www.lua.org/ftp/lua-5.3.5.tar.gz
tar zxf lua-5.3.5.tar.gz
cd lua-5.3.5
make linux test
```

If you are on MacOS you may go with this:
```
make macosx test
```

If you are on Windows just download a Linux subsystem and you will have 8 more hours to spend with your family or to just play games.

## Examples
- Simple Hello World
```
print("Hello World")
```
- Factorial
```
function fact (n)
      if n == 0 then
        return 1
      else
        return n * fact(n-1)
      end
    end
    
print("enter a number:")
a = io.read("*number")        -- read a number
print(fact(a))
```
- Writing page header
```
function BEGIN()
    io.write([[
        <HTML>
        <HEAD><TITLE>Projects using Lua</TITLE></HEAD>
        <BODY BGCOLOR="#FFFFFF">
        Here are some brief examples 
        <A HREF="home.html">Lua</A>.
        <BR>
    ]])
end
```

- Markov Chain Algorithm
```
function allwords ()
    local line = io.read()    -- current line
    local pos = 1             -- current position in line
    return function ()        -- iterator function
        while line do           -- repeat while there are line
            local s, e = string.find(line, "%w+", pos)
            if s then      -- found a word?
                pos = e + 1  -- update next position
                return string.sub(line, s, e)   -- return the word
            else
                line = io.read()    -- word not found; try next line
                pos = 1             -- restart from first position
            end
        end
        return nil            -- no more lines: end of traversal
    end
end
    
function prefix (w1, w2)
    return w1 .. ' ' .. w2
end
    
local statetab
    
function insert (index, value)
    if not statetab[index] then
        statetab[index] = {n=0}
    end
    table.insert(statetab[index], value)
end
    
local N  = 2
local MAXGEN = 10000
local NOWORD = "\n"
    
    -- build table
statetab = {}
local w1, w2 = NOWORD, NOWORD
for w in allwords() do
    insert(prefix(w1, w2), w)
    w1 = w2; w2 = w;
end
insert(prefix(w1, w2), NOWORD)
    -- generate text
w1 = NOWORD; w2 = NOWORD     -- reinitialize
for i=1,MAXGEN do
    local list = statetab[prefix(w1, w2)]
    -- choose a random item from list
    local r = math.random(table.getn(list))
    local nextword = list[r]
    if nextword == NOWORD then return end
    io.write(nextword, " ")
    w1 = w2; w2 = nextword
end
```