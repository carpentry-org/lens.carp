# lens

A simple Lens and Prism library for Carp.

The implementation of lenses and prisms is too general and does not follow
the laws (i.e. you can construct lenses and prisms that shouldn’t work), but I
think this is useful anyway.

## Usage

```clojure
(load "git@github.com:hellerve/lens.carp@master")

(deftype Address [city String street (Pair Int String)])

(defn main []
  (let-do [addr (Lens.for Address street)
           stre (Lens.for Pair b)
           lens (Lens.compose &addr &stre)
           data (Address.init @"Berlin" (Pair.init 10 @"Paul-Lincke-Ufer"))]
    (println* &(Lens.get &lens &data))
    (println* &(Lens.set &lens @&data @"no"))
    (println* &(Lens.over &lens @&data &(fn [a] (reverse &a))))
  )
)
```

It also provides you with helpers to construct `Prism`s for `Array` and `Map`
types, using:

```clojure
; will construct a prism for the second element of an array
(Prism.Array.for 1)

; will construct a prism for the map key "hello"
(Prism.Map.for "hello")
```

<hr/>

Have fun!
