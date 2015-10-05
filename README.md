[work in progress, feedback welcome]

Note that while this should feel very informal, all of the reasoning should be correct. If you spot a mistake, please raise an issue or correct me using a pull request. English is not my native language, so if you find awkwardness, please open a pull request and correct me.

Instead of trying to learn, let's try to discover.


# Identity

Imagine we have some programming language where the following is a valid statement or expression:

```
x
```

This does not tell us anything about `x`. It might be a reference to a variable, the roman number for 10, the numeral multiplication symbol, the construction of a product or something totally different. What we can say is that `x` exist and that we can point at it by stating `x`. In other words, we can say that the identity of `x` is `x`:

```
identity(x) = x
```

If you are looking at this from a programmers perspective you might recognise this construction as a function. If you come from a programming language that has type variables you might even see it as types:

```
Identity[X] = X
```

Note that there is a subtle difference between `x` and `identity(x) = x`. When we say `x` we say: we have an `x`. When we say `identity(x) = x` we say: **if** we have an `x` it's identity would be an `x`.

We could look at the same statement from the math side of things while using programmers glasses, we might see:

```
identity(x) == x
```

This again is subtly different because we state that given an `x`, the identity of `x` is equal to `x`. It means that in this statement we have `x`, a way to determine it's identity and a way to compare the two.

So why did we invent the `identity` concept? It's actually not really an invention but rather a discovery. Take for example the following:


```
x
y
```

Knowing nothing more, we could apply the same reasoning as above and get to state this:

```
identity(x) = x
identity(y) = y
```

Note that, while knowing nothing about `x` and `y`, we have common ground for both: they both have an identity.

Please be aware that `identity(x)` could also be written as `x.identity`, intuitively (for me) there is a subtle difference:

- `identity(x)` - We can detemine the identity of `x`, the focus is on `identity`
- `x.identity` - `x` has an identity, the focus is on `x`


## Identity shape

It might be obvious, but in the previous section we have described the relation between something and its identity: we can go from `x` to `identity(x)` and from `identity(x)` to `x`. We can now say something about the shape of identity, once you apply it to `x` you will get `x`. If we generalize that we can say that once you apply it to something, you will get that something back. We can write the shape down as follows:

```
identity: x -> x
```

As you can see, by discovering the concept of identity, we also discovered the arrow. Be aware that there is a difference between `x` and `x -> x`. In the first statement you have an `x` while in the second you have a way of identifying something (we could write it down as `y -> y` without changing it's meaning). You could say that `x -> x` is more general because you can use it for more. While `x` can be used only for `x`, `x -> x` can also be used to identify `y`. So if you want to talk about features or properties of something, without knowing anything about them, you can use `x -> x`. If something exists it will have an `x -> x` (or identity).

To make your brain hurt: we could state `identity(->) = ->`. This would give you some kind of chicken / egg problem: what came first, the fact that something can exist or the fact that something does exist? In my mind this is a very complex question, for me they were both there, we just discovered them.

For programmers it's tempting to say that the type of identity is a function from `x` to `x`. For most practical purposes it's great to do that, but remember that when you see it as a function you are making more assumptions than when you call it an arrow. Remember the analogy to types:

```
Identity[X] = X
```

The shape would be exactly the same:

```
Identity: X -> X
```

The difference here is that I am talking about types, from a naive perspective it looks as if I am saying: the type of the `Identity` type is `X -> X`. This makes my brain hurt because type of types takes me to that recursive realm which my brain can not handle very well. So let's just use the more general notions of arrows and shapes.

Let's write down some other arrows to see what we can find:

```
X -> Identity[X]
Identity[X] -> X
```

Let's try to give some meaning to these arrows. To do that we will write down a (fake) implementation.

- `X -> Identity[X]` - If you give me an `x` I will give you the identity of `x`.
- `Identity[X] -> X` - If you give me the identity of `x` I will give you `x`.

I wonder, what if I combine the two:

```
(X -> Identity[X]) -> (Identity[X] -> X)
(Identity[X] -> X) -> (X -> Identity[X])
```

If you give me something that goes from `x` to the identity of `x` I will give you something that goes from the identity of `x` to `x`. The other one is similar, but the other way around. What jumps out to me in these particular examples is that these are arrows between things that are themselves arrows.

## Identity lessons

Starting from the fact that something exists and discovering the hidden properties proves quite interesting.

By stating that the identity of `x` is `x` we get two things that are the same, but not exactly. Stricly 'the identity of `x`' is not the same as '`x`', but they are tied together in a statement tell us they are: 'the identity of `x` is `x`'. In the world of mathematics this subtle difference is recognised and in some circles they state things like: 'equivalence is equivalent to equality'. It seems that equality is a stronger version of equivalence.

The arrow we discovered moved from `x` to `x`. However, because `Identity[X] = X`, we could also have an arrow from `Identity[X]` to `X`. You could argue that that is the same as going from `X` to `Y` (where `Y` happens to be `Identity[X]`). For now we'll just say that the arrow can go from `A` to `B` if `A` and `B` are the same.

We also discovered there is a difference between having an `x` or knowing that an `x` could exist: `x` v.s. `x -> x`.


# Generalization

Remember the following arrows:

```
X -> Identity[X]
Identity[X] -> X
```

It seems we can generalize on `Identity` to allow for other things that follows the same pattern. That could be written down as follows:

```
X -> F[X]
F[X] -> X
```

While this seems harmless we are actually changing the meaning of the arrow we discovered. Because we do not know what `F` is, the above statements actually have the shape of `A -> B`. This effectively removes the restriction that both sides of the arrow must be the same. Turning it the other way around we can say that: if we have an arrow where `A` and `B` are the same, we are looking at the identity arrow.

Please note that the `A -> B` (as opposed to the `X -> X`) arrow is not an invention. Up until now we just assumed we had an `x`. This `x` had to come from somewhere which leads to the discovery of an arrow like `? -> x`, here the `?` is the magic land where `x`'s come from. As you can see, the shape of that arrow is `A -> B`. The `A -> B` arrow is actually more generic than the `X -> X` arrow. Combining an `A -> B` arrow with the notion that `A` and `B` must be the same gives us the concept of identity.

Going back to the generalized example:

```
X -> F[X]
F[X] -> X
```

This tells us that there are things (like identity) that say something about another thing. `F` in this case is something that tells us something about `X`. We don't know anything about `F` except that it exists (and thus has an identity). The statements above might be misleading, we simply substituted `Identity` for `F`, but we do not actually know if those specific arrows exist. But if they would exist, what would that tell us?

I like to think about the `F[_]` shape as being some kind of a context (or container). Putting the above shapes into words would lead me to something like:

- `X -> F[X]` - We can inject `X` into the context of `F`
- `F[X] -> X` - We can extract `X` from the context of `F`

Lets substitute `X` for `Identity[X]` (remember `Identity[X] = X`).

```
Identity[X] -> F[X]
F[X] -> Identity[X]
```

If we generalize this again it must be clear that `Identity[X]` is not the same as `F[X]` for the simple reason that we do no know what `F` is. So we get the following:

```
G[X] -> F[X]
F[X] -> G[X]
```

So with these arrows we could go from context `F` to context `G` and back.

Using our new arrows in the shape of `A -> B` we could try other shapes, for example arrows of arrows:

```
(X -> F[X]) -> (F[X] -> X)
```

Even more general:

```
(A -> B) -> (C -> D)
```

Let's write that down differently:

```
(->[A, B]) -> (->[C, D])
```

And even further:

```
->[->[A, B], ->[C, D]]
```

Now we generalize:

```
F[F[A, B], F[C, D]]
```

In this case `F` could be an arrow, but it could also be another context. What does this tell us? To me it seems the most important thing is that shapes can be combined to form other shapes. Identity gives us the shape `F[_]` while arrows give us the shape `F[_, _]`, together they can form shapes with an arbitrary number of things.

## Generalization lessons

Moving in a more generic direction gives us more freedom, we need to however carefully keep track what we give up to become more general. When we generalized on the identity arrow, we gained `A -> B` but also kept our identity arrow by adding a law for it: `A` must be the same as `B`. And now, if we see an arrow and notice `A` is the same as `B` we can recognise it as the identity arrow.

Shapes are interesting. Even if we do not know anything concrete about the thing it is, we can still say sensible things about it. If we find something that fits the shape `F[_]` we can say that `F` is some type of context.

Shapes are hiding in a lot of places. Using identity as a driver to get to new shapes can help. Even arrows introduced a new shape that gave rise to something that can be seen as composition.

Without any knowledge, just by playing with shapes and arrows you can discover really interesting patterns.


# Arrows

Let's start with two arrows:

```
a -> b
b -> c
```

What if we wanted to combine those two? As a result we would like to have `a -> c`. Intuitively this should be possible: if we have an `a` we can get a `b` and if we have a `b` we can get a `c`. Let's write that down using arrows:

```
(a -> b) -> ((b -> c) -> (a -> c))
```

Ok, that looks a bit complex. Let's simplify it to understand what's going on there:

```
f = a -> b
g = b -> c
h = a -> c

f -> (g -> h)
```

Now we can more clearly see that if we give an `f` (`a -> b`) we get an arrow (`g` -> `h`). And if we supply a `g` (`b -> c`) to this new arrow we get `h`, our new arrow `a -> c`. So, the question is, can we do that? Or put differently: is the combination of arrows something that we invented or something that was already there?

Maybe we find the answer if we write our simple example differently:

```
F[A] = B
G[B] = C

H[A] = G[F[A]]
```

Let's make that a bit more user friendly and use the `>>` symbols to combine arrows:

```
a -> c = (a -> b) >> (b -> c)
```

Let's combine some other arrows:

```
f = a -> b
g = b -> c
h = c -> d

(f >> g) >> h
f >> (g >> h)
```

As you can see in the last two lines there are two ways of combining three arrows. Either we combine `f` and `g` first and then combine the result with `h` or we combine `g` and `h` first and combine the result with `f`. There are situations where this does not matter, but there also might be situations where this would give you a different result. So we have the following situations:

- It does not matter which pair you combine first, the result is the same
- If you combine `f` with `g` first, the result is ...
- If you combine `g` with `h` first, the result is ...

There is one arrow for which we already know it does not make a difference how it is combined: the identity arrow.

```
f  = a -> b
1a = a -> a
1b = b -> b

(1a >> f) >> 1b  =  f  =  1a >> (f >> 1b)
```

## Arrow lessons

Arrows can be combined. We can say that an arrow `a -> c` is the same as the two arrows `a -> b` and `b -> c`.

When you combine arrows the order in which they are combined might have an influence on the outcome. This is a property of the combination: it either matters or it doesn't

# Category theory

This is a branch of mathematics that has leaked into a lot of programming languages. The problem, with most of the writing about it, is that it feels intimidating. With the knowledge we gained from the previous sections the definition of a category becomes quite simple:

- We have arrows
- We have objects (things) with an identity arrow
- Arrows can be combined, but only if the order of the combination does not matter

That's it.

Now the cool thing is that loads of people have identified mechanisms and properties of things they found in the wild. They have found certain shapes and figured out what they can and are used for. They even found that, if something has certain properties or a certain shape, you get other properties for free!

...
