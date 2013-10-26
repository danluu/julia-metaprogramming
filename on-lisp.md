# Notes from On Lisp

## 2.2 Defining functions
In lisp we can #' to get the definition of a function
> (defun double (x) (* x 2))
> #’double
#<Interpreted-Function C66ACE>

In julia,
> function double(x) x*2 end
> double
double (generic function with 1 method)
> code_typed(double,(Int,))                                                                                                    
1-element Array{Any,1}:
 :($(Expr(:lambda, {:x}, {{},{{:x,Int64,0}},{}}, quote  # none, line 1:
        return top(box)(Int64,top(mul_int)(x::Int64,2))::Int64
    end)))

## 2.3 Functional Arguments
Has apply, just like lisp. Unlike CL, you don't even have to quote symbols!
> apply(+, 1, 2)
3

Functions can take functions
> sort([1,2,3,-1,-2], by=abs)

If filter didn't exist, we'd have to write it
function filter(f::Function, a::Vector)
    r = Array(eltype(a), 0)
    for i = 1:length(a)
        if f(a[i])
            push!(r, a[i])
        end
    end
    return r
end

## 2.4 Functions as Properties
Multiple dispatch example here???

## 2.5 Scope
julia> y = 7
7

julia> function plusy(x)
         x + y
       end
plusy (generic function with 1 method)

julia> plusy(0)
7

julia> y = 10
10

julia> plusy(0)
10