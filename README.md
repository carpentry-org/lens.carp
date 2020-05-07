# lens

A simple Lens and Prism library for Carp.

The implementation of lenses and prisms is too general and does not follow
the laws (i.e. you can construct lenses and prisms that shouldn’t work), but I
think this is useful anyway.

## Usage

```clojure
(load "git@github.com:hellerve/lens.carp@master")

(deftype Address [city String street (Pair String Int)])

(defn main []
  (let-do [addr (Lens.for Address street)
           stre (Lens.for Pair a)
           comp (Lens.compose &addr &stre)
           data (Address.init @"Berlin" (Street.init 10 @"Paul-Lincke-Ufer"))]
    (println* &(~(Lens.get &comp) &data))
    (println* &(~(Lens.set &comp) @&data @"no"))
    (println* &(Lens.over &comp @&data &(fn [a] (reverse &a))))
  )
)
```

<hr/>

Have fun!
