# ChangePrecision

[![Build Status](https://travis-ci.org/stevengj/ChangePrecision.jl.svg?branch=master)](https://travis-ci.org/stevengj/ChangePrecision.jl)
[![Build status](https://ci.appveyor.com/api/projects/status/erbe16srnav0wrfu?svg=true)](https://ci.appveyor.com/project/StevenGJohnson/changeprecision-jl)

This package makes it easy to change the "default" precision of a large body of Julia code, simply by prefixing it with the `@changeprecision T expression` macro, for example:

```julia
@changeprecision Float32 begin
    x = 7.3
    y = 1/3
    z = rand() .+ ones(3,4)
end
```

In particular, floating-point literals like `7.3` are reinterpreted as the requested type `Float32`, operations like `/` that convert integer arguments to `Float64` instead convert to `Float32`, and random-number or matrix constructors like `rand` and `ones` default to `Float32` instead of `Float64`.

Code that explicitly specifies a type, e.g. `rand(Float64)`, is unaffected by `@changeprecision`.
